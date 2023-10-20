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
