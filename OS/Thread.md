
![[Pasted image 20231008172703.png]]
### 컴퓨터 구조 관점에서의 쓰레드
- 쓰레드는 프로세스([[Process]]) 내에서 실행되는 가장 작은 실행 단위이다.
- 프로세스 내의 모든 쓰레드는 해당 프로세스의 메모리 영역을 공유한다.

### OS 관점에서의 쓰레드

- 쓰레드는 프로세스의 실행을 담당한다.
- 프로세스는 하나 이상의 쓰레드를 가질 수 있다.
- 각 쓰레드는 고유한 스택([[Stack]])을 가지나, 코드, 데이터, 힙 영역은 공유한다.
- 쓰레드 간 통신은 별도의 통신 메커니즘 없이도 메모리를 통해 통신이 가능하다.
---
### 쓰레드란?
>쓰레드란 프로세스 내에서 실행되는 흐름의 단위를 말한다.
>일반적으로 하나의 프로그램은 하나의 쓰레드를 가지고 있지만, 프로그램의 환경에 따라 다수의 쓰레드를 동시에 실행시킬 수 있으며, 이러한 실행 방식을 **멀티 쓰레드**([[Multi Thread]])라고 한다.
>각 쓰레드는 자신만의 스택([[Stack]])과 레지스터([[Register]])를 가진다.

### 쓰레드의 장단점
##### 장점
- **자원 효율성**
	- 쓰레드는 하나의 프로세스 내의 자원(코드, 데이터, 힙)을 공유하기 때문에 프로세스에 비해 자원 할당 비용이 적게 들고 문맥 교환([[Context Switch]]) 비용도 적게 든다.
- **병렬 처리의 유연성**
	- 다중 쓰레드의 경우, 일부 쓰레드의 처리가 지연되더라고 다른 쓰레드에서 작업을 계속 처리할 수 있다.
		- 다중 쓰레드를 사용하여 CPU의 여러 코어에서 동시에 작업을 수행할 수 있음.
		- 이로 인해 전체 시스템의 성능 향상을 기대할 수 있다.
- **통신의 간편성**
	- 프로세스 간의 통신은 [[IPC]]가 필요하지만, 쓰레드는 공유 주소 공간(데이터, 힙)을 사용하여 데이터를 교환할 수 있다.
- **시스템 콜 최소화**
	- 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.
- 
##### 단점
- 하나의 쓰레드에서 발생한 문제가 프로세스 전반에 영향을 미칠 수 있다.
- 자원을 공유하기 때문에 동기화 문제가 발생할 수 있다.
---
### 쓰레드 동기화 방법의 종류
- [[Mutex]]
- [[Semaphore]]
- [[Monitor]]
위 3가지 방법 모두 쓰레드 동기화를 위한 도구로써, 여러 쓰레드나 프로세스가 공유 자원에 동시에 접근할 때 발생할 수 있는 문제를 방지하기 위해 사용된다. 이들의 공통점은 다음과 같다.
1. **공유 자원 보호**
	- 모든 동기화 메커니즘의 주요 목적은 공유 자원을 보호하는 것이다. 여러 쓰레드가 동시에 공유 자원에 접근하려고 할 때, 이러한 도구를 사용하여 동시 접근을 제어하고, 데이터의 일관성과 무결성을 보장한다.
2. **상호 배제([[Mutual Exclusion]])**
	- 이 방법들은 모두 상호 배제의 원칙을 따른다. 즉, 한 번에 하나의 쓰레드만 특정 코드 영역이나 자원에 접근할 수 있도록 한다.
		- 이를 통해 동시성 문제, 예를 들어 **<font color="#9c86e9">Race Condition</font>을 방지한다.
3. **대기 및 깨우기**
	- 쓰레드가 자원에 접근하려고 시도할 때, 해당 자원이 이미 다른 쓰레드에 의해 사용 중인 경우, 쓰레드는 대기 상태로 전환된다. 자원이 사용 가능해지면, 대기 중인 쓰레드 중 하나가 깨어나 자원을 사용하게 된다.
4. **데드락([[Deadlock]]) 및 기아 문제([[Starvation]])**
	- 위 방법들을 사용할 때, Deadlock이나 Starvation과 같은 문제가 발생할 수 있다.
		- 이러한 문제는 여러 쓰레드가 동기화 도구를 사용하여 자원에 접근하려고 할 때 발생할 수 있음.
