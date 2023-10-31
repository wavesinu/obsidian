### `swtch.S`

```c
# Context switch
#void swtch(struct context **old, struct context *new);
# Save the current registers on the stack, creating
# a struct context, and save its address in *old.
# Switch stacks to new and pop previously-saved registers.

•globl swich
swtch:
movl 4(%esp), %eax
movl 8(%esp), %edx

# Save old callee-saved registers
pushl %ebp
pushl %ebx
pushl %esi
pushl %edi

# Switch stacks
movl %esp, (%eax)
movl %edx, %esp

# Load new callee-saved registers
popl %edi
popl %esi
popl %ebx
popl %ebp
ret
```
### `proc.c`

```c
void
scheduler(void)
{
	struct proc *p;
	struct cpu *c = mycpu;
	
	for(::){
		// Enable interrupts on this processor.
		sti(); 
		// Loop over process table looking for process to run.
		acquire (&ptable. lock);
		for (p = ptable. proc; p < &ptable. proc[NPROCI; p+){
			if(p→state * RUNNABLE)
				continue;
		// Switch to chosen process. It is the process's job
		// to release ptable. lock and then reacquire it
		// before jumping back to us.
			c→›proc = p;
			switchuvm(p);
			p-state = RUNNING;
			
			swtch(&(c-scheduler), p→›context);
			switchkvm();
		
			// Process is done running for now.
			// It should have changed its p-state before coming back.
			c→proc = 0;
		}
		release (ptable. lock);
		
		}
	}
```
---
### 1. 
### 2. 프로세스 초기화
- `proc.c` 파일에서 `allocproc()` 함수를 수정
	- 새로 생성된 프로세스의 우선순위와 시간 할당량을 초기화
```c
91   p->nice = 20;       // 우선순위 설정
92   p->timeslice = p->nice; // 타임 슬라이스를 nice 값에 따라 초기화
```

### 3. 타이머 인터럽트 처리
```c
void
trap(struct trapframe *tf)
{
  if(tf->trapno == T_SYSCALL){
    if(myproc()->killed)
      exit();
    myproc()->tf = tf;
    syscall();
    if(myproc()->killed)
      exit();
    return;
  }

  switch(tf->trapno){
  case T_IRQ0 + IRQ_TIMER:
    if(cpuid() == 0){
      acquire(&tickslock);
      ticks++;
      wakeup(&ticks);
      release(&tickslock);
    }
	// 추가된 부분-begin
	if(myproc() && myproc()->state == RUNNING){
		myproc()->ticks++;

		if(myproc()->timeslice-- == 0){
			yield_if_timeslice_expired();
			myporc()->timeslice = TIMESLICE;
		}
	}

	for(struct proc *p = ptable.proc; p < &ptable.proc[NPROC]; p++){
		if(p->state == RUNNABLE){
			p->age++;
		}
	}
	// 추가된 부분-end
    lapiceoi();
    break;
  case T_IRQ0 + IRQ_IDE:
    ideintr();
    lapiceoi();
    break;
  case T_IRQ0 + IRQ_IDE+1:
    // Bochs generates spurious IDE1 interrupts.
    break;
  case T_IRQ0 + IRQ_KBD:
    kbdintr();
    lapiceoi();
    break;
  case T_IRQ0 + IRQ_COM1:
    uartintr();
    lapiceoi();
    break;
  case T_IRQ0 + 7:
  case T_IRQ0 + IRQ_SPURIOUS:
    cprintf("cpu%d: spurious interrupt at %x:%x\n",
            cpuid(), tf->cs, tf->eip);
    lapiceoi();
    break;

  //PAGEBREAK: 13
  default:
    if(myproc() == 0 || (tf->cs&3) == 0){
      // In kernel, it must be our mistake.
      cprintf("unexpected trap %d from cpu %d eip %x (cr2=0x%x)\n",
              tf->trapno, cpuid(), tf->eip, rcr2());
      panic("trap");
    }
    // In user space, assume process misbehaved.
    cprintf("pid %d %s: trap %d err %d on cpu %d "
            "eip 0x%x addr 0x%x--kill proc\n",
            myproc()->pid, myproc()->name, tf->trapno,
            tf->err, cpuid(), tf->eip, rcr2());
    myproc()->killed = 1;
  }

  // Force process exit if it has been killed and is in user space.
  // (If it is still executing in the kernel, let it keep running
  // until it gets to the regular system call return.)
  if(myproc() && myproc()->killed && (tf->cs&3) == DPL_USER)
    exit();

  // Force process to give up CPU on clock tick.
  // If interrupts were on while locks held, would need to check nlock.
  if(myproc() && myproc()->state == RUNNING &&
     tf->trapno == T_IRQ0+IRQ_TIMER)
	  if (myproc()->timeslice-- == 0) {
	    yield_if_timeslice_expired();
		myproc()->timeslice = TIMESLICE; // set a new timeslice
	  }

  // Check if the process has been killed since we yielded
  if(myproc() && myproc()->killed && (tf->cs&3) == DPL_USER)
    exit();
}
```
### 4. 스케줄러 수정
- 수정 전
```c
void
scheduler(void)

struct proc *p;
struct cpu *c = mycpu();

for(;;)){}
	// Enable interrupts on this processor.
	sti();
	
	// Loop over process table looking for process to run.
	acquire (&ptable. lock);
	for(p = ptable.proc; p < &ptable.proc[NPROC]; p++){
		if(p→state != RUNNABLE)
			continue;
		
		// Switch to chosen process. It is the process's job
		// to release ptable. lock and then reacquire it
		// before jumping back to us.
		c->proc = p;
		switchuvm(p);
		p->state = RUNNING;
		
		swtch (&(c->scheduler), p->ontext);
		switchkvm();
		
		// Process is done running for now.
		// It should have changed its p-state before coming back.
		c->proc = 0;
	}
	release(&ptable.lock);
	}
}
```
- 수정 후
```c
void
scheduler(void)
{
	struct proc *p;
	struct proc *highest_priority_p;
	struct cpu *c = mycpu();
	
	c->proc = null;	//프로세스를 실행하기 전 proc 포인터를 null로 초기화
	
	for(;;){
		sti();
		
		acquire(&ptable.lock);
		for(p = ptable.proc; p < &ptable.proc[NPROC]; p++){
			if(p->state == RUNNABLE && 
			(highest_priority_p == null || p->nice > highest_priority_p->nice))
			{
				highest_priority_p = p;
			}
		}
		if(highest_priority_p != null){
			p = highest_priority_p;
			/*implement code*/
			c->proc = p;
			switchuvm(p);
			p->state = RUNNING;
			
			swtch(&(c->scheduler), p->context);
			switchkvm();
			
			c->proc = 0;
			p->timeslice = o->nice;
		}
		release(&ptable.lock);
	}
}
```
- 우선순위를 기반으로 프로세스를 선택, timeslice를 관리하도록 `scheduler` 함수를 수정
	- `p->timeslice = p->nice` 코드를 통해, 프로세스가 실행될 때마다 시간 할당량을 다시 설정함.
### 4. 동적 우선순위 할당을 위한 새로운 시스템 콜 구현
### 5. timeslice 조정
```

```




