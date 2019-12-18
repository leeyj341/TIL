# SQL

* Primary Key(PK)

> 기본키, 중복없이 단 하나만 있어야 하는 키를 말한다.

![pk](images/pk.png)

PK를 가지고 있는 테이블을 **ParentTable**이라고 부른다.

* Foreign Key

> 외래키, 다른 테이블에 설정된 기본키를 참조해 사용할 때 외래키라고 부른다.

![fk](images/fk.png)

FK를 가지고 있는 테이블을 **ChildTable**이라고 부른다.

* 정규화

> 관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 과정을 말한다. 위의 두 표를 예로 볼 수 있다.

* JOIN

>정규화된 테이블을 가지고 원하는 작업을 진행하는 과정을 **"JOIN한다"**고 한다.

## SQL Query

### DDL

* CREATE

> 데이터베이스나 테이블을 만드는 명령어

```sql
create user java identified by java;
```

* DROP

> 데이터베이스나 테이블 등을 삭제하는 명령어

* ALTER

> 데이터베이스나 테이블 등의 구성을 변경하는 명령어

```sql
alter user java identified by java123;
```

### DML

* SELECT

> 테이블에서 행을 검색하는 명령어

* INSERT

> 테이블에 신규 행을 추가하는 명령어

* DELETE

> 테이블에서 행을 삭제하는 명령어

### DCL

* COMMIT

> 데이터베이스 변경 내용을 확정하는 명령어

* ROLLBACK

> 데이터베이스 변경 내용을 취소하는 명령어

* GRANT 

> 사용자에게 처리 권한을 부여하는 명령어

* REVOKE

> 사용자 처리 권한을 제거하는 명령어