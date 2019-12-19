# SQL

* **P**rimary **K**ey(PK)

> 기본키, 중복없이 단 하나만 있어야 하는 키를 말한다.

![pk](images/pk.png)

PK를 가지고 있는 테이블을 **ParentTable**이라고 부른다.

* **F**oreign **K**ey

> 외래키, 다른 테이블에 설정된 기본키를 참조해 사용할 때 외래키라고 부른다.

![fk](images/fk.png)

FK를 가지고 있는 테이블을 **ChildTable**이라고 부른다.

* 정규화

> 관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 과정을 말한다. 위의 두 표를 예로 볼 수 있다.

* JOIN

>정규화된 테이블을 가지고 원하는 작업을 진행하는 과정을 **"JOIN한다"**고 한다.

## SQL-Plus 명령어

```sql
conn system/manager
-- 접속 / 아이디 / 패스워드
cl scr
-- 지금까지 사용했던 명령, 화면 다 지워짐
set linesize 300;
-- 설정한다 / 한 라인에 보여지는 글자 수 / 글자 개수
desc customer;
-- customer라는 이름의 테이블 정보를 보여줌
```

## SQL Query

> DB에 원하는 작업을 수행할 수 있도록 하는 명령언어

* **;**을 만나기 전까지는 명령으로 인식하기 때문에 Enter를 입력해도 명령이 끝나지 않음. => 여러 줄로 sql문을 작성할 수 있다.

* 대소문자를 구분하지 않는다.

* *****은 모든 컬럼을 조회하겠다는 의미

* 컬럼에 null을 저장할 수 있다.

* **null**은 **0**이나 space만 입력해놓은 값과 **다른 값**

  사용할 수 없고 저장되지 않은 값

* 컬럼명 대신 **alias(별명)**를 정의해서 사용할 수 있다.

```sql
select ename 사원명, hiredate as 입사일, sal "나의 급여" from emp;
```

* 여러 컬럼을 합쳐서 하나의 컬럼명으로 조회할 수 있다. `||`연산자 이용

```sql
select ename || '의 급여는 ' || sal || '입니다.' from emp;
```

* 오라클의 문자열, 날짜 데이터는 `' '`로 표현한다.

* 연산의 결과로 컬럼을 생성할 수 있다. (+, *, /, -, 함수...)

  단 null이 포함되어 있는 컬럼은 연산할 수 없다.

  ```sql
  select ename, sal, comm, sal+comm 급여합 from emp;
  ```

* 중복이 있는 경우 중복을 제거하고 출력하기 위해 select문에 distinct를 추가할 수 있다.

```sql
select distinct job from emp;
```

위 예시는 emp라는 테이블에 job이 몇 종류 있는지 알아보기 위해 사용했다.

### DDL

> **테이블**을 생성, 삭제, 수정하는 명령

#### CREATE

> 데이터베이스나 **테이블을 생성**하는 명령어

```sql
create user java identified by java;
-- 생성한다 / 유저를 / 이름이 java인 / 식별된 / 패스워드가 java로
create table test(
    id varchar2(10) primary key,
    pass varchar2(15) not null,
	name varchar2(10));
-- test 테이블 생성(컬럼 데이터형(글자수) 제약조건);
```

#### DROP

> 데이터베이스나 테이블 등을 **삭제**하는 명령어

```sql
drop database testdelete;
-- 삭제한다 / database를 / 이름이 testdelete인
drop table customer;
-- customer 테이블을 삭제한다
```

#### ALTER

> 데이터베이스나 테이블 등의 구성을 **변경**하는 명령어

```sql
alter user java identified by java123;
-- 수정한다 / 유저를 / 이름이 java인 / 식별된 / 패스워드가 java123으로
```

### DML

> 테이블의 **데이터**를 **조작**하는 명령문
>
> 반드시 작업이 완료된 후 **commit** 명령문을 실행해야 저장이 됨

#### SELECT

> 테이블에서 행을 **검색**하는 명령어

```sql
select * from tab;
-- 선택한다 / 전부를 / tab에서
select user from dual;
-- 현재 접속 계정 출력 명령어

select 컬럼명 alias명;
select 컬럼명 as alias명;
select 컬럼명 "alias명";	-- 중간에 공백이 있는 경우 ""로 묶어줘야 함 
-- 별명으로 조회하는 명령
```

#### UPDATE

#### INSERT

> 테이블에 신규 행을 **추가**하는 명령어

```sql
insert into Department values ('001', '전산', '7', '02-111-2222');
-- 삽입한다 / Department 테이블에 / ()안 정보를 가진 행을
```

#### DELETE

> 테이블에서 행을 **삭제**하는 명령어

### DCL

#### COMMIT

> 데이터베이스 변경 내용을 **확정**하는 명령어

```sql
commit;
```

#### ROLLBACK

> 데이터베이스 변경 내용을 **취소**하는 명령어

#### GRANT 

> 사용자에게 처리 **권한을 부여**하는 명령어

```sql
grant connect,resource to scott;
-- 권한을 부여 / connect와 resource / scott에게
```

#### REVOKE

> 사용자 처리 권한을 제거하는 명령어

### 조건

#### WHERE

> select 절 사용시 위 명령을 통해 조건을 추가한다.

* * 검색 결과를 제한 (조건에 만족하는 데이터만 조회)
  * **from절 다음**에 정의
  * **조건식이 true**가 되도록 정의
  * 비교연산자: `<, <=, >, >=, =, **<>(!= 와 같은 의미)**, !=
  * 비교하는 값이 문자나 날짜일 경우 **' '** 사용
  * 비교하는 값은 **정확하게 대소문자를 구분**해줘야 한다.

```sql
select ename,job,hiredate,sal from emp where job='MANAGER';
```

##### AND, OR, IN 연산자

> **두 개 이상의 조건**이 있는 경우 사용할 수 있는 연산자

* AND

  : **모든 조건**이 일치

* OR

  : 모든 조건 중 **한 개만 일치** (조건이 모두 다른 컬럼인 경우)

```sql
select * from emp where deptno = 10 or sal >= 2000;
```

* IN

  : or 연산자의 의미와 동일

   컬럼명 in (비교할 값, 값, ...)

   **같은 컬럼**에서 **값**을 **여러 개 비교**해야 하는 경우

```sql
select ename,job,deptno from emp where job in ('MANAGER', 'PRESIDENT');
```

* NOT 

  : 부정

```sql
select ename,job,deptno from emp where job not in ('MANAGER', 'PRESIDENT');
```

##### null값에 대한 비교

* IS NULL

  : null인 데이터를 조회

```sql
select ename, sal, comm from emp where comm is null;
```

* IS NOT NULL

  : null이 아닌 데이터를 조회

```sql
select ename, sal, comm from emp where comm is not null;
```

**※ null과 0은 다르다**

##### LIKE

> 대표문자와 함께 사용
>
> 조건비교를 위해 **입력한 값**이 **문자열에 포함**되어 있는 것을 찾는 경우

* % : 모든 문자열

```sql
select ename,sal,comm from emp where ename like 'A%';
-- ename이 A로 시작하는 모든 문자열 select
select ename,sal,comm from emp where ename like '%A%';
-- ename에 A가 어디에 위치하든 중간에 하나라도 있는 모든 문자열 select
```

* _ : 한 자리 문자를 의미

```sql
select ename,sal,comm from emp where ename like '_A%';
-- ename의 두 번째 문자가 A인 모든 문자열 select
```

##### BETWEEN

> 같은 컬럼에서 사이 조건을 비교하는 경우
>
> BETWEEN a AND b 형식으로 사용

```sql
select ename,sal from emp where sal between 2000 and 5000;
```

### 정렬

#### ORDER BY

> ORDER BY 컬럼명 정렬기준(asc, desc)

* 기본은 오름차순이다.

* WHERE 절 다음에 위치한다

##### 오름차순(asc)

> 작 -> 큰 
>
> ex) 1, 2, 3, 4, 5, ...  / ㄱ, ㄴ, ㄷ, ㄹ, ....

```sql
select ename, sal, job from emp order by sal; -- asc 생략가능
```

##### 내림차순(desc)

> 큰 -> 작 
>
> ex) 5, 4, 3, 2, 1, ...  / ㅎ, ㅍ, ㅌ, ㅋ, ....

```sql
select ename, sal, job from emp order by sal desc;
```