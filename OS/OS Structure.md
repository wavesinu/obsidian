## General OS Structure
- 애플레케이션이 OS로 들어올 때는 소프트웨어 인터럽트의 형태로 들어온다.
	- 그러나 커널 안에 들어오면 커널 안에서 다른 매니저나 다른 모듈에 접근할 때엔, function call의 형태로 해당 기능을 호출한다.
### DOS(Disk Operating System)
- 1980년대와 1990년대 초반에 널리 사용되던 운영체제
- 주로 단일 사용자, 단일 작업 시스템으로 설계되었음.
- 커맨드 라인 인터페이스를 기반으로 한다.
- **장점**
	- 간단하고, 메모리 요구 사항이 적다.
	- 사용자가 시스템의 저수준 작업에 직접 접근할 수 있다.
- **단점**
	- 다중 작업, 다중 사용자 환경에는 적합하지 않다.
	- GUI에 대한 지원이 부족하다.
	- 메모리 관리 및 하드웨어 지원에 제한이 있다.

### Monolithic Structure
- 모든 시스템 서비스를 하나로 연결된 단일 프로그램으로 구현한다.
- 커널 내부의 모든 함수는 서로를 직접 호출할 수 있다.
- **장점**
	- 모든 요소가 하나의 주소 공간에 있기 때문에 성능이 좋다.
	- 시스템 호출 간의 오버헤드가 적다.
- **단점**
	- 하나의 부분을 수정하면 전체 시스템에 영향을 줄 수 있다.
		- 유지 보수가 어렵다.
	- 하나의 오류가 전체 시스템을 망가뜨릴 수 있다.
	- 확장성이 제한적이다.
### Layerd Structure
![[Pasted image 20231001155938.png]]
- OS를 계층별로 나누어 구현한다.
- 각 계층은 바로 아래의 계층만을 사용해 구현한다.
- **장점**
	- 설계와 구현이 간단하고 명학하다.
	- 각 계층은 독립적으로 개발이 가능, 따라서 유지보수(테스팅, 디버깅 등)가 쉽다.
	- 하나의 계층에서 발생한 오류가 다른 계층에 영향을 주지 않는다.
- **단점**
	- 여러 계층을 거쳐야 하는 경우, 성능 오버헤드가 발생할 수 있다.
	- 올바를 계층의 순서와 분할을 결정하는 것이 어렵다. -> 초기 OS 설계의 어려움
### MicroKernel Structure
> MicroKernel Structure 구조는 OS의 커널이 최소한의 기능만을 포함하도록 설계한 구조이다.
- 커널은 기본적인 메시지 전달, 하드웨어 추상화, 스케줄링만을 처리한다.
- 대부분의 시스템 서비스는 사용자 모드에서 실행되는 별도의 프로세스로 구현된다.
- 커널과 시스템 서비스 간의 통신은 메시지 전달([[Message Passing]])을 통해 이루어진다.
- **장점**
	1. **유연성**
		- 다양한 서비스와 프로토콜을 쉽게 추가하고 변경할 수 있음.
	2. **안정성**
		- 하나의 서비스에서 발생한 오류가 다른 서비스에 영향을 주지 않음.
		- 사용자 모드에서 실행되기 때문에, 전체 시스템에 영향을 주는 오류가 적다.
	3. **보안**
		- 각 서비스는 독립적인 주소 공간에서 실행됨.
			- 하나의 서비스가 다른 서비스의 메모리에 접근하는 것을 방지함.
	4. **포트 가능성**
		- 하드웨어 의존성이 적어, 다양한 플랫폼에 쉽게 OS를 이식할 수 있음.
			- 미니 커널 부분만 새로운 아키텍처에 맞게 포팅만 하면 됨.
- **단점**
	1. **성능 오버헤드**
		- 메시지 패싱을 통한 통신은 성능 오버헤드를 일으킬 가능성이 있음.
			- 여러 서비스 간의 통신이 필요한 경우, 지연이 발생할 수 있음.
	2. **복잡성**
		- 메시지 기반의 통신과 서비스 간의 상호 작용을 설계 및 구현이 복잡함.