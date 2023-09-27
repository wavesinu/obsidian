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
5. 