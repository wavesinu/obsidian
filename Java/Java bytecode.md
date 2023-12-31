### bytecode란?
바이트코드는 특정 하드웨어가 아닌, 가상 머신에서 실행되도록 설계한 중간 코드이다.
Java에서는 소스 코드를 컴파일하면 바이트코드로 변환되는 `.class` 파일이 생성된다. 이 바이트코드는 [[JVM]]에서 실행된다.
### 바이트코드의 특징
1. 플랫폼 독립적
	- 바이트코드는 특정 하드웨어나 운영 체제에 종속되지 않는다. 
	- 따라서 Java 프로그램은 "한 번 작성하면 어디서나 실행"이라는 원칙에 따라 다양한 플랫폼에서 실행될 수 있다.
2. 보안
	- 바이트코드는 소스 코드보다 분석하기 어렵기 때문에, 어느 정도 보안을 제공한다.
	- [ ] 그러나 바이트코드는 역공학을 통해 다시 소스 코드로 변환될 수 있기 때문에 절대적인 보안을 제공하는 것은 아니다.
3. 최적화
	- JVM은 방이트코드를 실행하기 전에 [[JIT 컴파일러]]를 사용하여 바이트코드를 네이티브 코드로 변환할 수 있다.
		- 이를 통해 프로그램의 실행 속도가 향상될 수 있다.
4. 이식성
	- 바이트코드는 다양한 JVM 구현 사이에서 이식성을 제공한다.
		- 이는 Java 프로그램이 다양한 장치와 플랫폼에서 일관된 방식으로 작동하도록 보장한다.