___
##### <font color="#2DC26B">Related Links</font>
___
#### 데이터 정의어(DDL: Data Definition Language)
> 데이터베이스를 정의하는 언어이며, 데이터를 생성, 수정, 삭제하는 등의 데이터 전체의 골격을 결정하는 언어이다.
- **CREATE**
- **ALTER**
- **DROP**
- **TRUNCATE**
> [!faq]- DML과 DCL
> **DML(Data Manipulation Language)**
> 정의된 데이터베이스에 입력된 레코드를 조회하거나 수정하거나 삭제하는 등의 역할을 하는 언어
> - select : 데이터 조회
> - insert : 데이터 삽입
> - update: 데이터 수정
> - delete: 데이터 삭제
> 
> **DCL(Data Control Language)**
> 데이터베이스에 접근하거나 객체에 권한을 주는 등의 역할을 하는 언어
> 
> - grant: 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 부여
> - revoke: 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 박탈, 회수
> - commit: [[Transaction]] 작업을 저장
> - rollback: 트랜잭션 작업을 취소, 원래대로 복구



#### 저장구조 정의어와 view 정의어
- 어떤 DBMS에서는 **저장구조 정의어(SDL: Storage Definition Language)**를 사용하여 내부 스키마를 나타내고, **뷰 정의어(VDL: View Definition Language)**를 사용하여 뷰를 명시하거나 개념 스키마 사이의 사상을 나타낸다.
#### 데이터 조작어
- 데이터를 검색, 삽입, 삭제, 수정하기 위한 조작 언어
- DML 명령어는 범용 프로그래밍 언어에 삽입되어 사용될 수 있고, 이때 범용 프로그래밍 언어를 **호스트 언어**라고 하고, 삽입된 DML 명령어를 데이터 부속어라고 한다.
#### DBMS 구성모듈
![[Pasted image 20230831174541.png]]
