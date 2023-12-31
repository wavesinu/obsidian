### JIT(Just-In-Time) 컴파일러란?
> 인터프리터 방식의 단점을 보완하기 위해 도입되었다.
> 인터프리터 방식으로 실행하다가 적절한 시점에 바이트코드([[Java bytecode]]) 전체를 컴파일하여 기계어로 변환하고, 이후에는 기계어로 직접 실행하는 방식이다.
- JIT 컴파일러는 프로그램을 실행하는 도중에 바이트코드나 중간 코드를 해당 시스템의 네이티브 코드로 동적으로 컴파일한다.
- 변환된 네이티브 코드는 프로그램의 실행 속도를 빠르게 만들어 준다.
###  JIT 작동방식
- 프로그램이 실행될 때, JIT 컴파일러는 자주 사용되는 코드 부분(핫스팟)을 삭별하고 이를 네이티브 코드로 최적화 하여 컴파일한다.
- 이렇게 된 코드(컴파일된 코드)는 캐시([[Cache]])에 저장되어, 같은 코드가 다시 호출될 떄 빠르게 실행될 수 있다.
### 장점
- **성능 향상**
	- 네이티브 코드로의 동적 컴파일로 인해 실행 속도가 빨라진다.
- **최적화**
	- 실행 중에 프로그램의 실제 동작을 분석하여 최적화할 수 있다.
### 단점
- **초기 오버헤드**
	- 처음 코드를 컴파일 하는데 시간이 걸릴 수 있다.


Java에서는 자바 컴파일러가 자바 프로그램 코드를 바이트 코드로 변환한 다음, 실제 바이트코드를 실행하는 시점에서 [[JVM]]이 바이트코드를 JIT 컴파일을 통해 기계어로 변환한다.

