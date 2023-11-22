### Java Virtual Machine
![[Pasted image 20231001213301.png]]
- Java는 OS에 종속적이지 않다는 특징을 가지고 있다. OS에 종속받지 않고 실행되기 위해선 OS위에서 Java를 실행시키기 위해 사용되는 것이 JVM이다.
	- 즉, OS에 종속받지 않고 CPU가 Java를 인식 및 실행 할 수 있게 하는 가상 컴퓨터를 말한다.
- Java 소스코드, 즉 원시 코드 `*.java` 는 CPU가 인식하지 못하므로 기계어로 컴파일 해야한다.
- 하지만 Java는 JVM이라는 가상머신([[Virtual Machine]])을 거쳐 OS에 도달하기 때문에 OS가 인식할 수 있는 기계어로 컴파일 되는 것이 아닌, JVM이 인식할 수 있는 [[Java bytecode]](`*.class`)로 변환된다.
	- 변환된 bytecode는 기계어가 아니기 때문에 OS에서 바로 실행되지 않는다.
	- 이 때, JVM이 OS가 bytecode를 이해할 수 있도록 해석한다.
		- 따라서 bytecode는 JVM 위에서 OS 상관없이 실행될 수 있다,
### 컴파일 하는 방법

1. **Java 프로그램 작성**
    - Using any text editor (like `nano`, `vim`, or even more user-friendly ones like Visual Studio Code or IntelliJ IDEA), write a simple Java program. For example:
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Hello, World!");
        }
    }
    ```
    - Save the file as `HelloWorld.java`.
2. **Java 프로그램 컴파일**
    - Navigate to the directory where you saved your Java file using the Terminal.
    - Compile the program by typing:
    ```zsh
    javac HelloWorld.java
    ```
    - After successful compilation, you should see a new file named `HelloWorld.class` in the same directory. This is the bytecode file that the Java Virtual Machine (JVM) will execute.
3. **프로그램 실행**
    - Still in the Terminal, type:
    ```zsh
    java HelloWorld
    ```
> Java Compiler는 JDK를 설치하면 `javac.exe` 라는 실행 파일 형태로 설치된다.
> 정확히는 JDK의 bin 폴더에 `javac.exe` 라는 실행 파일 형태로 설치된다. Java Compiler의 `javac` 명령어를 사용하면, `.class` 파일을 생성할 수 있다.