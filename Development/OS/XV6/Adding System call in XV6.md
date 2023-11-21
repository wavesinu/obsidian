### System call이란?
- 운영체제는 아래와 같이 두가지 타입의 실행을 지원한다.
```
1) Kernel mode
2) User mode
```

### 과제 요구 사항
**목표**
- nice 관련 system call 구현 및 테스트 프로그램 작성
- 각 프로세스 정보에 nice 변수를 추가하고, 이를 읽고 변경하는 syscall 구현 + syscall 기능을 테스트하는 프로그램 작성
### **syscall 인터페이스**
-  `int getnice(int pid)`
- `int setnice(int pid, int value)`
### **syscall 동작 특징**
- `getnice` 함수는 인자로 지정된 pid process의 현재 nice 값을 반환한다.
- `setnice` 함수는 인자로 지정된 pid process의 nice 값을 지정한다.
	- 각 프로세스는 처음 할당되는 nice 값은 20이며, nice 값의 유효범위는 [0, 40]
### syscall의 return 값
- `getnice`
	- 성공 시, 해당 프로세스의 nice 값.
	- 실패 시, -1 반환 (예: 해당 pid process가 없는 경우)
- `setnice`
	- 성공 시, 0을 반환
	- 실패 시에는 다음과 같이 처리
		- 해당 pid의 프로세스가 없는 경우에는 -1을 반환
		- 전달된 nice value가 유효범위를 넘는 경우에는 -2를 반환
### 테스트 프로그램 작성
- 다음과 같은 이름을 갖는 테스트 프로그램을 각각 작성한다.
- `gnice`: 주어진 pid의 현재 nice 값을 출력한다.
	- **usage**: `gnice pid`
- `snice`: 주어진 pid의 nice 값을 주어진 value로 변경한다.
	- **usage**: `snice pid value`
- 해당 pid가 없거나 주어진 nice value가 정상 범위의 값이 아닌 경우
	- 각 상황에 맞는 에러 메시지를 출력한다.
