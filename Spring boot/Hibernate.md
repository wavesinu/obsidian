#JPA #JDBC
### Hibernate란?
>Hibernate는 Java의 [[ORM]] 프레임워크 중 하나로, [[JPA]]의 구현체이며 JPA 인터페이스를 구현하는 동시에 내부적으로 [[JDBC]] API를 사용한다. 또한 객체 지향 프로그래밍[[OOP Principle]]과 관계형 데이터베이스([[RDBMS]]) 간의 불일치 문제를 해결하는 데 도움을 준다. 

### Hibernate의 장점
1. **객체 지향적인 코드**
	- Hibernate를 사용하면 개발자는 객체 지향적인 코드를 작성할 수 있으며, 데이터베이스와의 상호작용은 Hibernate가 처리한다.
		- 이로 인해 코드의 가독성과 유지 보수성이 향상된다.
2.  **데이터베이스 독립성**
	- Hibernate는 다양한 데이터베이스 시스템을 지원한다. 따라서 데이터베이스 변경 시 Hibernate의 설정만 수정하면 된다.
3. **자동 테이블 생성**
	- 개발 초기 단계에서 유용하게 사용될 수 있는 기능으로, Java 클래스 기반으로 데이터베이스 테이블을 자동으로 생성하거나 수정할 수 있다.
4. **자체 Query 언어 지원**
	- [[HQL]](Hibernate Query Language)을 통해 객체지향적인 쿼리를 작성할 수 있다.
5. **트랜잭션 관리**
	- Hibernate는 트랜잭션 관리를 지원하여 데이터의 일관성과 무결성([[Database Constraints]])을 유지하는 데 도움을 준다.
6. **유연한 매핑**
	- 애노테이션 또는 XML을 사용하여 객체와 데이터베이스 테이블 간의 매핑을 유연하게 설정할 수 있다.
### HIbernate, JPA, 그리고 JDBC와의 관계
**JDBC**
- Java 애플리케이션과 관계형 데이터베이스 간의 통신을 위한 API이다.
- 개발자는 SQL 쿼리를 직접 작성하고, 그 결과를 처리해야 한다.

**Hibernate**
- Hibernate는 ORM 프레임워크로, JDBC위에서 구축되었다.
- Hibernate는 JDBC의 복잡성을 추상화하고, 객체 지향적인 접근을 제공한다.

**JPA**
- JPA는 Java ORM을 위한 표준 API이다.
- Hibernate는 JPA의 구현체 중 하나이다. 즉, <font color="#9c86e9">JPA는 인터페이스이며, Hibernate는 그 인터페이스를 구현한 구현체이다.</font>
- JPA를 사용하면 다른 ORM 프레임워크로 쉽게 전환할 수 있다.
	- 예를 들어, Hibernate에서 EclipseLink로 변경하는 것이 가능하다.
>요약하면, JDBC는 Java와 데이터베이스 간의 저수준 연결을 제공하며, Hibernate는 JDBC 위에 구축된 ORM 프레임워크이다. JPA는 ORM을 위한 Java 표준 인터페이스이며, Hibernate는 JPA의 구현체 중 하나다.
---
```embed
title: "JPA, Hibernate, 그리고 Spring Data JPA의 차이점"
image: "https://suhwan.dev/images/jpa_hibernate_repository/jpa_hibernate_relationship.png"
description: "Suhwan Jee’s blog"
url: "https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/"
```
```embed
title: "[DB] 하이버네이트(Hibernate)란?"
image: "https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1T1UN%2Fbtrc1UBAvpT%2FuOIlIqk2d8og9tCKqqG7gk%2Fimg.png"
description: "ORM 기술에 대한 명세인 JPA(Java Persistence API)의 구현체의 한 종류 JPA의 구현체이므로 JPA의 특징을 함께 정리했어요. Hibernate란? 하이버네이트는 자바 언어를 위한 ORM 프레임워크에요. JPA의 구현체로, JPA 인터페이스를 구현하며, 내부적으로 JDBC API를 사용해요. JPA는 관계형 데이터베이스와 객체의 패러다임 불일치 문제를 해결할 수 있다는 점과 영속성 컨텍스트(엔티티를 영구 저정하는 환경) 제공이 큰 특징이에요. JPA 자바 애플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정…"
url: "https://livenow14.tistory.com/70"
```
