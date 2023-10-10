>ORM(Object-Relational Mapping) 프레임워크는 프로그래밍 언어와 관계형 데이터베이스 간의 불일치 문제를 해결하기 위한 프로그래밍 기술이다.
>ORM은 프로그래밍 언어의 객체와 데이터베이스 테이블 간의 매핑을 제공하여, 개발자가 SQL 쿼리를 작성하는 대신 객체 지향적인 방식으로 데이터베이스 작업을 수행할 수 있게 도와준다.
### ORM 프레임워크의 장점
1. **데이터베이스 독립성**
	- ORM은 다양한 데이터베이스 시스템을 지원한다.
		- 데이터베이스 변경 시 ORM 설정만 수정하면 된다.
2. **객체 지향적 접근**
	- 데이터베이스 테이블 대신 객체와 작업하므로, 비즈니스 로직을 더 자연스럽게 표현할 수 있다.
	- 각종 객체에 대한 코드를 별도로 작성하기 때문에 코드의 가독성이 향상된다.
	- SQL의 절차적, 순차적인 접근이 아닌 객체 지향적인 접근으로 인해 생산성이 증가한다.
1. **자동화된 [[CRUD]] 작업**
	- ORM 프레임워크는 객체의 생성, 조회, 업데이트, 삭제 작업을 자동화해준다.
2. **트랜잭션 관리**
	- ORM은 데이터의 일관성을 유지하기 위한 트랜잭션 관리 기능을 제공한다.
### ORM 프레임워크의 단점
- 잘못 구현하는 경우 속도 저하 및 심각할 경우 일관성이 무너지는 문제점이 발생할 수 있다.
- 일부 자주 사용되는 대형 쿼리는 속도를 위해 SP를 쓰는 등 별도의 튜닝이 필요하다.
- 프로시저가 많은 시스템에서는 ORM의 객체 지향적인 장점을 활용하기 어렵다.
### OOP와 RDBMS의 불일치 문제
1. **상속 불일치 (Inheritance Mismatch)**:
   - 객체 지향 프로그래밍에서는 상속을 통해 객체 간의 계층 구조를 표현할 수 있다. 반면, 관계형 데이터베이스에서는 이러한 계층 구조를 직접적으로 표현하는 방법이 없다.

2. **연관성 불일치 (Association Mismatch)**:
   - 객체 지향 모델에서는 객체 간의 다양한 연관 관계 (일대일, 일대다, 다대다 등)를 표현할 수 있다. 이러한 관계를 데이터베이스 테이블에 매핑하는 것은 복잡할 수 있다.

3. **데이터 타입 불일치 (Data Type Mismatch)**:
   - 객체 지향 언어와 관계형 데이터베이스는 종종 다른 데이터 타입 시스템을 가진다. 예를 들어, 객체 지향 언어에서의 복잡한 객체나 컬렉션을 관계형 데이터베이스의 기본 데이터 타입으로 직접 매핑하는 것은 어려울 수 있다.

4. **식별성 불일치 (Identity Mismatch)**:
   - 객체 지향 프로그래밍에서는 객체의 동일성은 메모리 상의 위치나 참조에 의해 결정될 수 있다.
	   - 반면, 데이터베이스에서는 주로 기본 키에 의해 식별된다.

5. **트랜잭션 불일치 (Transaction Mismatch)**:
   - 객체 지향 시스템에서는 일반적으로 긴 지속성의 트랜잭션을 가질 수 있으나, 데이터베이스 트랜잭션은 짧고, 빠르게 커밋되거나 롤백되어야 한다.

6. **비동기 불일치 (Concurrency Mismatch)**:
   - 객체는 여러 스레드나 프로세스에 의해 동시에 액세스될 수 있다. 이러한 동시성 문제를 관리하는 방법은 객체 지향 시스템과 데이터베이스 시스템에서 다를 수 있습니다.