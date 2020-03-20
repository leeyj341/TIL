# Spring Data

> 신기술에 대응하기 위해 만든 프레임워크
>
> 복잡하게 처리해야 할 일을 캡슐화 해 편하게 사용할 수 있게 만듬
>
> 우리는 `Spring data for mongodb`를 사용

* Repository interface 

  : 제일 상위의 인터페이스

## 설치

* Spring MVC project 생성

* pom.xml 수정
  
  * mavenRepository에서 `spring data core mongoDB core 1.6.0`
  
* servlet 설정 파일 수정

  > rdbms 사용 때 핵심 클래스를 등록했던 것처럼 mongodb 역시 기능을 제공하는 핵심 클래스 등록을 해야 한다.

  ```html
  <!-- mongodb서버에 접속할 수 있도록 ip, port정보를 명시 -->
  <mongo:mongo id="mongo" port="27017" host="127.0.0.1" />
  	
  <!-- mongodb를 spring에서 접속해서 제어할 수 있는 기능을 제공하는 핵심 클래스를 등록 -->
  <beans:bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
  	<beans:constructor-arg ref="mongo"/>
  	<beans:constructor-arg name="databaseName" value="bigdata"/>
  </beans:bean>
  ```

## 실행

> RDBMS 접근과 마찬가지로 document를 CRUD 하기 위해서는 해당 document와 매칭되는 DTO 클래스가 필요하다.

* @Document(collection="score")

  : 핵심 클래스가 인식할 수 있도록 annotation을 추가한다. 어떤 Collection의 document인지 모르기 때문에 **반드시 Collection명을 지정**해주어야 한다.
  
* Controller, DAO, Service 단의 구조는 RDBMS과 거의 일치한다.

* ScoreRepository

* MongoTemplate
