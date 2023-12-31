### 클래스 로더
- **역할**: `.class` 파일(바이트코드)을 로드하고, 링크를 통해 바이트코드([[Java bytecode]])가 적절하게 실행될 수 있도록 준비하는 역할을 합니다.
- **동작 과정**:
    1. **로딩**: 파일 시스템에서 JVM 메모리에 `.class` 파일을 로드합니다.
    2. **링크**: 검증, 준비, (선택적으로) 해석 단계를 거쳐 바이트코드를 실행할 준비를 합니다.
    3. **초기화**: 정적 변수를 할당하고 정적 초기화 블록을 실행합니다.
- **영역**: 메소드 영역(Method Area)에 클래스의 바이트코드, 메타데이터, 정적 변수 등이 저장됩니
### 런타임 데이터 영역
- **메소드 영역(Method Area)**: 클래스의 바이트코드, 메타데이터, 정적 변수 등이 저장됩니다.
- **힙(Heap)**: 객체와 배열이 동적으로 할당되는 영역입니다.
- **스택(Stack)**: 메소드 호출과 로컬 변수에 대한 정보가 저장되는 영역입니다.
- **PC 레지스터(PC Registers)**: 현재 실행 중인 JVM 명령의 주소를 가지고 있습니다.
- **네이티브 메소드 스택(Native Method Stack)**: 네이티브 메소드에 대한 정보를 저장하는 영역입니다.
### 실행 엔진
- **역할**: 바이트코드를 실행하는 역할을 합니다. 이는 인터프리터와 [[JIT 컴파일러]]를 통해 수행됩니다.
    - **인터프리터**: 바이트코드를 한 줄씩 해석하고 실행합니다. 빠르게 시작하지만, 전반적인 실행 속도는 느립니다.
    - **JIT 컴파일러**: 자주 사용되는 바이트코드를 네이티브 코드로 컴파일하여 실행 속도를 향상시킵니다.
- **영역**: 실행 엔진은 JVM의 전체 영역에서 동작하며, 주로 메소드 영역에 저장된 바이트코드와 스택 영역의 정보를 사용하여 프로그램을 실행합니다.
### **네이티브 인터페이스(JNI: Java Native Interface)**:
- Java 코드가 C, C++ 등의 네이티브 코드와 상호 작용할 수 있게 해주는 프레임워크입니다.
### **네이티브 메소드 라이브러리**
- [[JNI]]를 통해 호출되는 실제 네이티브 코드 라이브러리입니다.