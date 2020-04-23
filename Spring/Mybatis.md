# Mybatis 

1. pom.xml에 의존모듈을 추가

   * mybatis
   * mybatis- stpring

2. mybatis에서 사용할 설정 파일을 작성

   * mybatis메인 설정파일

     : mybatis를 실행할 때 필요한 내용을 정의

       connection관리를 위해 필요한 내용(spring으로 관리하므로 생략)

       mapper에 대한 정보

       mapper에서 사용할 dto

       spring설정파일이 저장되는 위치에 추가

       /WEB-INF/config/mybatis-config.xml로 저장

   * mapper

     : sql문을 정의하는 설정 파일

       테이블 한 개에서 사용하는 sql문을 하나의 mapper파일

       src폴더에 추가

3. spring설정 파일에 mybatis를 사용할 수 있도록 등록

   (`SqlSession`객체가 mybatis에서 사용하는 핵심클래스

    => spring jdbc의 ` JdbcTemplate`과 동일)

   * connection을 사용(생성)할 수 있도록 등록

   * `SqlSession`을 사용하려면 factory객체부터 생성해야 하므로 `Factory`객체를 먼저 설정한다. 

     (spring에서 mybatis의 핵심 클래스를 사용할 수 있게 하기 위한 객체)

      ==> `Connection`객체를 사용, mybatis의 메인 설정파일을 등록

   * mybatis의 핵심클래스인 SqlSession클래스의 하위클래스를 생성

     `SqlSessionTemplate` => spring.jdbc의 `JdbcTemplate`과 같은 역할

## 기능 추가하기

0. 새로운 테이블로 작업을 한다면 mybatis-config.xml파일에 VO파일과 mapper 파일 등록

1. mapper에 sql문 추가

2. `DAOImpl`클래스에 메서드 추가

   => mybatis의 핵심클래스인 `SqlSession`클래스를 이용해서 작업

3. `ServiceImpl`클래스에서 DAO의 메서드 호출할 수 있도록 메서드 정의

4. `Controller`에서 `ServiceImpl`의 메서드를 호출해서 작업할 수 있도록 정의

   ```markdown
   BoardController ㅡ> BoardService ㅡ> BoardDAO
   ```

5. `Controller`에서 response하는 뷰에서 `Controller`가 공유해준 데이터를 꺼내서 출력하기(select 작업)

6. tiles설정 파일에서 뷰등록

