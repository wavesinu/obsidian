- 기본 키 레코드를 삭제할 때 해당 키를 참조하는 모든 외래키 레코드도 함께 삭제한다.
- 연관된 데이터의 일관성을 유지하려는 상황에서 유용하다.
- 실수로 중요한 데이터를 삭제할 위험이 있으므로 주의가 필요하다.
---
### ON DELETE CASCADE
>`ON DELETE CASCADE`는 주 테이블에서 레코드가 삭제될 때, 관련된 외래키를 가진 자식 테이블의 레코드도 자동으로 삭제되게 하는 옵션이다.
>**즉, 데이터의 일관성을 유지하려는 목적으로 사용된다.**
- **작동 원리**
	1. 주 테이블에서 특정 레코드가 삭제될 때, 해당 레코드의 기본 키 값을 참조하는 외래키가 있는 모든 자식 테이블의 레코드가 함께 삭제된다.
	2. 이는 연쇄적으로 작동할 수 있다. 즉, 한 자식 테이블의 레코드가 삭제되면, 그 자식 테이블이 또 다른 테이블의 부모 테이블로서 기능할 때 해당 자식 테이블의 레코드도 삭제될 수 있다.
- **사용 사례**
    - 예를 들어, Users 테이블과 Orders 테이블이 있을 때, 한 사용자가 삭제되면 해당 사용자의 모든 주문도 함께 삭제되게 하려면 ON DELETE CASCADE를 사용할 수 있다.
    - 이러한 동작은 **데이터의 일관성을 유지하기 위해 필요한 경우가 많다**. 사용자가 삭제된 경우 해당 사용자의 주문 정보는 더 이상 필요하지 않을 수 있기 때문이다.
- **주의 사항**
	- `ON DELETE CASCADE`는 실수로 많은 양의 데이터를 잃을 위험이 있다.
	- 대량의 데이터가 연쇄적으로 삭제될 때, 데이터베이스의 부하가 증가할 수 있다.

```SQL
CREATE TABLE PERSONAL_INFO
(
    Person VARCHAR(20) NOT NULL,
    Age INT(11),
    Child VARCHAR(20),
    PRIMARY KEY (Person),
    FOREIGN KEY (Child) REFERENCES PERSONAL_INFO(Person) ON DELETE CASCADE
);

INSERT INTO PERSONAL_INFO VALUES ('John', 20, NULL);
INSERT INTO PERSONAL_INFO VALUES ('Kim', 42, 'John');
INSERT INTO PERSONAL_INFO VALUES ('Lee', 22, NULL);

DELETE FROM PERSONAL_INFO WHERE Person = 'John';

select * from PERSONAL_INFO;
```
- 위 SQL문을 실행한 결과, FK로 John을 참조하고 있던 Kim까지 삭제되는 것을 확인할 수 있다.