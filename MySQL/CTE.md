### CTE란?
- CTE(Common Table Expression)는 서브 쿼리로 쓰이는 파생테이블([[Derived table]])과 비슷한 개념으로 사용된다.
- CTE와 비교 대상으로는 [[VIEW]]가 있다. VIEW는 생성하기 위해 권한이 필요하고 사전에 정의를 해야하지만, CTE는 생성 권한이 필요 없고 하나의 쿼리문이 끝날 때까지만 지속되는 일회성 테이블이다.
- CTE는 코드의 가독성과 재사용성을 위해 파생테이블 대신 사용하기에 유리하다.
### CTE를 사용하는 이유
CTE를 사용하는 주요 이유는 다음과 같다.
- 쿼리의 가독성 향상
- 동일한 쿼리에서 여러 번 참조 가능
- 향상된 성능
- 사용자가 VIEW를 생성할 수 없는 경우, VIEW의 유효한 대안이 될 수 있다.
- 재귀 쿼리 생성 가능 : 계층적 데이터를 처리할 때 매우 유용하다.

`SELECT`, `UPDATE` 및 `DELETE` 문은 CTE를 참조할 수 있다.
```SQL
WITH RECURSIVE natural_sequence AS  
    (  
        SELECT 1 AS n  
        UNION ALL  
        SELECT n + 1 FROM natural_sequence  
                     WHERE n < 10  
    )  
SELECT * FROM natural_sequence;
```

