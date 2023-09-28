# How to add system call in xv6
```c
we need to modify following files :
1) syscall.c
2) syscall.h
3) sysproc.c
4) usys.S
5) user.h
```
1. **syscall.c**
2. **syscall.h**

XV6에서 시스템 호출은 [[Stack]]에 저장된 인자를 사용하여 호출된다. 따라서 시스템 호출 함수의 프로토타입은 인자를 직접 가져오지 않는다. 대신, 함수 내부에서 XV6 제공 함수를 사용하여 이 인자들을 가져온다.
- 이 함수들 중 하나가 `argint()`이다. `argint()`는 시스템 호출의 인자를 가져오기 위해 사용된다.
- 이 함수는 인자의 인덱스(예: 첫 번째 인자, 두 번째 인자 등)의 값을 저장할 변수의 주소를 받아, 해당 변수에 인자 값을 저장한다.

따라서, 시스템 호출 함수의 프로토타입에 void가 사용되는 이유는 함수가 직접적인 인자를 받지 않기 때문이다. 대신 함수 내부에서 필요한 인자들을 커널 스택에서 가져온다.
- `defs.h`에서 정의된 프로토타입 (예: `int getnice(int pid)`)은 사용자 프로그램이 해당 시스템 호출을 사용할 때의 인터페이스를 정의한다.
- `sysproc.c`에서의 구현 (예: `sys_getnice(void)`)는 실제 커널 내부에서 시스템 호출이 어떻게 동작하는지를 정의한다. 이 구현에서 인자들은 커널 스택에서 직접 가져온다.
___
For example, write a sys call getnp().

- this syscall returns the number of current process.

  

### Procedure

1. Add a new syscall number in syscall.h
2. Add a new syscall lib function in usys.S
3. Add a kernel syscall function in the syscall.c
4. Write a kernel syscall function : sys_getnp
	- sysproc.c : syscall related to the process management
		- write the kernel syscall function in sysproc.c
	- proc.c : kernel process management functions
		- write the real compute function in proc.c
5. The new functions added to proc.c must be defined in defs.h
6. Add the syscall function prototype user.h

___
1. `defs.h`에 함수 인터페이스 선언
```c
...
int getnice(int);
int setnice(int, int);
...
```
2. syscall.h( XV6의 모든 시스템 콜이 선언되어 있음.)에 SYS_getnice, SYS_setnice 함수 선언
3. syscall.c에 시스템 콜 포인터를 선언해야 함.
```c
/*syscall.c*/
[SYS_getnice] sys_getnice,
[SYS_setnice] sys_setnice,
```
4. getnice, setnice 함수의 프로토 타입을 선언
```c
/*syscall.c*/
extern int sys_getnice(void);
extern int sys_setnice(void);
```

- 하지만 `syscall.c` 파일 안에서 이 함수들을 직접 구현하지 않는다
	- 대신, `syscall.c`에서는 함수의 프로토타입만 추가하게 된다. 실제 함수의 구현은 `sysproc.c`에서 구현함.


---
##### `proc.h`
```c
 37 // Per-process state
 38 struct proc {
 39   uint sz;                     // Size of process memory (bytes)
 40   pde_t* pgdir;                // Page table
 41   char *kstack;                // Bottom of kernel stack for this process
 42   enum procstate state;        // Process state
 43   int pid;                     // Process ID
 44   struct proc *parent;         // Parent process
 45   struct trapframe *tf;        // Trap frame for current syscall
 46   struct context *context;     // swtch() here to run process
 47   void *chan;                  // If non-zero, sleeping on chan
 48   int killed;                  // If non-zero, have been killed
 49   struct file *ofile[NOFILE];  // Open files
 50   struct inode *cwd;           // Current directory
 51   char name[16];
 52   int nice;                    // nice value for assginment
 53 };
```
- `proc.h`에 `nice` 변수 추가

##### `syscall.h`
```c
#define SYS_getnice 24
#define SYS_setnice 25
```
- `geetnice`, `setnice`의 system call 번호 선언
```c
```
##### `usys.S`
```c
SYSCALL(getnice)
SYSCALL(setnice)
```
- 시스템콜 래퍼([[System Call Wrapper]]) 선언
##### `sysproc.c`
```c
```
##### `proc.c`
```c
```

##### `user.h`
```c
// system calls
...
int getnice(int pid);
int setnice(int pid, int value);
```


- `getnice.c`, `setnice.c` 구현
- `getnice.c`
```c
#include "types.h"
#include "stat.h"
#include "user.h"

int
main(int argc, char **argv)
{

	if(argc != 2){
		printf(2, "usage: getnice pid...\n");
		exit();
	}

	printf(1, "%d\n", getnice(atoi(argv[1])));
	exit();
}
```
- `setnice.c`
```c
#include "types.h"
#include "stat.h"
#include "user.h"

int
main(int argc, char **argv)
{
  if(argc != 3){
    printf(2, "usage: setnice pid nice...\n");
    exit();
  }

  setnice(atoi(argv[1]), atoi(argv[2]));
  exit();
}
```

##### `defs.h`
```c
104 //PAGEBREAK: 16
105 // proc.c
106 int             cpuid(void);
107 void            exit(void);
108 int             fork(void);
109 int             growproc(int);
110 int             kill(int);
111 struct cpu*     mycpu(void);
112 struct proc*    myproc();
...
126 int             getnice(int);
127 int             setnice(int, int);
```
- `getnice`, `setnice` 선언

___
##### 테스트 프로그램 컴파일
- 우선 테스트 코드를 XV6 운영체제에서 컴파일하고 링크 해야 한다.
	- XV6의 `Makefile`에 새로운 테스트 프로그램을 추가해야 함.

##### XV6 실행
```shell
make qemu
```

##### 테스트 프로그램 실행
```shell
$ gnice 5
```
- 정상적으로 출력됐을 경우, 다음과 유사한 결과를 가져야 함
```shell
Nice value for pid 5 is: 20
```
- 또한 `snice` 명령어를 사용하여 특정 PID의 nice 값을 변경하고 그 결과를 확인할 수 있어야 한다.
