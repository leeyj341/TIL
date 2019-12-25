# JDBC

> 자바를 통한 오라클 DB의 사용
>
> 자바를 통해 쿼리를 작성, DB의 정보를 사용할 수 있다

* ojdbc6.jar

  : oracle에서 제공하는 jdbc 사용에 관련한 라이브러리다 (.jar 파일)

## OracleDriver

> oracle.jdbc.driver 패키지 안에 있는 핵심 클래스로 jdbc를 사용하기 위해 로딩해주어야 한다.

```java
Class.forName("oracle.jdbc.driver.OracleDriver");
// Class의 API로 드라이버를 로딩해주는 메서드
```

Class의 forName은 인스턴스 객체를 만드는 것이 아니라 jvm이 모르는 오라클의 class정보를 알려주기 위한 메서드이다. 오라클이 DB를 불러오는 과정은 공개되면 안되기 때문에(영업 비밀) 코드의 내용은 다 숨겨져 있다.

```java
Connection con = DriverManager.getConnection(url,user,password);
// DBMS에 연결하고 연결 정보를 Connection타입으로 반환한다
```

* url 

  : 데이터베이스의 주소로 오라클의 기본 형식은 **jdbc:oracle:thin:@ip주소:port번호:db버전**

* user

  : db에 로그인 할 user 명

* password

  : 로그인 할 user의 비밀번호

```java
Statement stmt = con.createStatement();
// sql을 실행하기 위한 객체를 생성한다
```

```java
int result = stmt.excuteUpdate(sql);
// DML쿼리문을 실행할 수 있는 메서드로 sql에 원하는 쿼리문을 넣어주면 된다
```

복습 끝...