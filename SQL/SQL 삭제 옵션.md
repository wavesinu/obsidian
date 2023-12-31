### [[RESTRICT]]
- 참조하는 외래키가 있을 경우 삭제를 방지한다.
- 주로 참조 무결성 제약조건을 엄격하게 보장하려는 상황에서 사용된다.
### [[CASCADE]]
- 기본 키 레코드를 삭제할 때 해당 키를 참조하는 모든 외래키 레코드도 함께 삭제한다.
- 연관된 데이터의 일관성을 유지하려는 상황에서 유용하다.
- 실수로 중요한 데이터를 삭제할 위험이 있으므로 주의가 필요하다.
### [[SET NULL]]
- 기본 키 레코드를 삭제할 때, 해당 키를 참조하는 외래키 컬럼의 값을 `NULL`로 설정한다.
- 연관된 데이터의 연결만 끊고 싶을 때 사용된다.
- 외래키 컬럼이 `NULL` 값을 허용하는 경우에만 사용할 수 있다.
### [[NO ACTION]]
- 현재 트랜잭션 내에서는 아무런 조치가 취해지지 않는다.
- 트랜잭션이 종료될 때까지 참조 무결성을 검사한다.
- 실제로는 다른 삭제 옵션과 유사한 동작을 수행하지만, 검사 시점이 다르다.