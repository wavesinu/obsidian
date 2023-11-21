### 컴퓨터 구조 관점에서의 프로세스
- 프로세스는 실행 중인 프로그램의 인스턴스, 즉 실행중인 프로그램을 의미한다. 이때 프로그램은 디스크 상의 실행 가능한 코드이며, 프로세스는 이 프로그램이 메모리 상에서 실행되는 상태를 의미한다.
- 프로세스는 자체적인 독립된 메모리 영역을 가진다.
	- 이 영역은 코드, 데이터, 스택([[Stack]]), 힙([[Heap]]) 등으로 구성된다.
### OS 관점에서의 프로세스
- 각 프로세스는 독립된 주소 공간과 자원(파일 핸들, I/O)을 가진다.
- 프로세스 간 통신은 [[IPC]] 메커니즘을 통해 이루어진다. ([[Pipe]], [[Message Queue]], [[Socket]] 등)

### 프로세스와 쓰레드의 차이
1. **독립성**
	- 프로세스는 독립된 메모리 영역을 가지며, 쓰레드([[Thread]])는 프로세스 내의 메모리를 공유한다.
2. **통신**
	- 프로세스 간 통신은 IPC를 통해 이루어지지만, 쓰레드 간 통신은 공유 메모리를 통해 간단하게 이루어진다.
1. **생성 및 종료**
	- 쓰레드의 생성 및 종료는 프로세스에 비해 빠르고 효율적이다.
2. **안정성**
	- 하나의 쓰레드가 예외 상황을 만나 충돌하면, 같은 프로세스 내의 다른 쓰레드들도 영향을 받을 수 있다.
		- 하지만 하나의 프로세스가 충돌하더라도 다른 프로세스에는 영향을 미치지 않는다


> <font color="#9c86e9"><font color="#b2a2c7">**프로그램의 실행을 보장하는 단위는 프로세스인가 쓰레드인가?**</font></font>
> 프로세스는 실행 중인 프로그램의 인스턴스이며, 하나의 프로세스는 하나 이상의 쓰레드를 포함할 수 있다.
> 반면, 쓰레드는 프로세스 내에서 실행되는 개별적인 실행 흐름이며, 쓰레드는 프로세스의 메모리 공간과 자원을 공유하면서 실행되고, 프로세스 내에서 동시에 여러 쓰레드가 실행될 수 있다.
> 
> 따라서, <font color="#e36c09">프로그램의 실행을 보장하는 최소 단위는 쓰레드</font>라고 할 수 있다!
> 프로세스는 이러한 쓰레드들의 컨테이너 역할을 하며, 각각의 쓰레드에 실행 컨텍스트와 실행 흐름을 제공한다.

---
### 프로세스의 메모리 구조
![[Pasted image 20231008171241.png]]
각 프로세스는 위 그림과 같은 구조를 갖는다. 각 영역은 다음과 같은 역할을 한다.
- **Code 영역**
	- 프로그램을 실행시키는 실행 파일 내의 명령어들이 위치하는 공간
- **Data 영역**
	- 전역 변수, `static` 변수들이 위치하는 공간
- **Heap 영역**
	- 동적할당([[Dynamic Memory Allocation]])을 위한 메모리 영역(`malloc()`, `new` 등)
- **Stack 영역**
	- 지역 변수, 파라미터(함수에 전달되는 인자)가 위치하는 공간
---