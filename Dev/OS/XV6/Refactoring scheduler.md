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

### 3. 스케줄러 수정
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

	for(;;){
		sti();

		acquire(&ptable.lock);
		for(p = ptable.proc; p < &ptable.proc[NPROC]; p++){
			if(p->state == RUNNABLE && 
				(highest_priority_p == null || p->nice > highest_priority_p->nice)){
				highest_priority_p = p;
			}
		}
		

	}
}
```
### 4.



