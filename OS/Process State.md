프로세스의 상태는 프로그램이 실행되면서 여러 단계를 거치게 되는데, 이는 운영체제에서 프로세스 관리의 핵심 요소 중 하나이며, 각 상태는 프로세스의 현재 위치나 상황을 나타낸다.

![[Pasted image 20230918204512.png]]
### new(embryo)
- 이 상태는 프로세스가 생성되기 시작하는 단계이다. 프로세스가 메모리에 로드되기 전의 초기 생성 단계를 의미한다.
- 프로세스가 처음으로 생성되면, 필요한 메모리를 할당받기 위한 요청이 이루어지고, 해당 프로세스에 관한 메타데이터와 관련 정보가 운영체제의 프로세스 테이블에 등록된다.
### ready
- 프로세스가 CPU를 사용할 준비가 완료된 상태이다.
- 프로세스가 실행되기 위한 모든 정보와 자원은 할당되었으나, CPU가 다른 프로세스를 처리 중일 때, 해당 프로세스는 준비 상태를 유지하게 된다.
	- 준비 상태의 프로세스들은 [[CPU Scheduling]]에 의해 선택되어 running 상태로 전환될 준비를 하고 있다.
### waiting(blocked)
>장치마다 waiting queue가 존재함. (키보드 etc.)
- 프로세스가 어떤 <font color="#9c86e9">이벤트나 조건을 기다리는 상태</font>이다.
- 예를 들어, 프로세스가 I/O 작업이 필요한 경우, 혹은 특정 자원이나 신호를 기다리는 경우에 waiting 상태가 된다.
- 필요한 작업이나 자원에 대한 응답이 완료되면 프로세스는 다시 ready 상태로 전환된다.
	- I/O request: `read(...)`
	- Wait for an event: `sleep(3)`
	- Wait for a msg: `recv(...)`
- 
### running(scehduler dispatch)
- 프로세스가 현재 CPU에서 실행 중인 상태이다.
- 운영체제의 스케줄러에 의해 선택된 프로세스는 running 상태로 변경되고, 해당 프로세스의 명령어들이 실행된다.
### terminated
- 프로세스의 실행이 종료된 상태이다.
- 프로세스가 모든 작업이 완료하거나 예외적인 상황으로 종료될 경우 이 상태가 된다.
	- 이 상태가 되면(`exit` 시스템 콜을 통해) 프로세스에 할당된 자원들은 OS에 의해 반납되고, 프로세스 테이블에서도 해당 프로세스의 정보가 제거된다.
---
### 멀티태스킹에서의 Process State
