# MongoDB

> 자바스크립트 기반의 비동기방식 데이터베이스
>
> ---
>
> * 많은 양의 데이터를 처리해야 할 때
>
> * 스키마가 복잡해지는 구조를 가진 데이터일 때
>
> ---
>
> 위의 경우를 제외하고는 oracle을 사용

* 특징

  * NoSql 방식 : **N**ot **O**nly **Sql**
  * 비정형 데이터(스키마가 없다.)
  * json으로 데이터 처리 
  * ex)
    * 기업 설문

* [doc](https://docs.mongodb.com/v3.6/) 참조

  > 하둡의 맵리듀스 방식과 비슷한 Sharding이나 설치법, 기본구조 설명 등 자세한 설명을 확인할 수 있다.

## 설치 및 실행

> mongoDB 홈페이지에서 Enterprise버전(3.6)을 다운

* 환경변수 Path에 MongoDB bin 경로 추가

* `mongod`명령을 이용해 실행가능하다.

  * 이때 서버 경로를 설정해주지 않으면 에러가 발생하기 때문에 경로 설정 필요

    <img src="images/mongodb.png" style="zoom:67%;" />

* 설정 후 `mongod -dbpath c:\iot\bigdata\mongodata`로 실행

* 다른 cmd창으로 띄워 `mongo`명령으로 클라이언트 접속이 가능하다.

  ![](images/mongodb1.png)

* `show dbs;`로 db의 정보 확인 가능

  > `show collections`(= `select * from tab;`)로 응용 가능

## 용어

* collection (rdbms에서 테이블)

  > 관계형 데이터베이스처럼 스키마를 정의하지 않는다.

  * 종류

    * capped collection

      : 고정 사이즈를 주고 생성하는 컬렉션 ex) log 정보

      미리 지정한 저장공간이 모두 사용되면 맨 처음에 저장된 데이터가 삭제되고 공간으로 활용

    * non capped collection

      : 일반적인 컬렉션

  * 생성

    * `db.createCollection("컬렉션명")` 

      **=>** 일반 collection

    * `db.createCollection("컬렉션명", {옵션 list})`

      **=>** 각각의 옵션을 설정해서 작업 (json)

  * 삭제

    * `db.collection명.drop();`

  * 컬렉션명 변경

    * `db.collection명.renameCollection("변경할컬렉션명");`

* document (레코드)

* field (컬럼)

* _id (기본키) 

  * **반드시 들어가야 함**
  
* new Date() : oracle의 sysdate와 같음.

## 명령

> [document](https://docs.mongodb.com/v3.6/reference/method/)

* `use mydb`

  : "mydb"라는 이름의 db로 접속 (= conn mydb/mydb)

* `db.stats()`

  : 현재 db의 정보를 보여줌

* `db.logout()`

  : 현재 db에서 로그아웃

## CRUD

### insert

> db.컬렉션명.insert({데이터...})
>
> db.컬렉션명.insertOne({데이터...})
>
> db.컬렉션명.insertMany({데이터...})

* document에 대한 정보는 json의 형식으로 작성

* mongodb에서 document를 삽입하면 자동으로 _id가 생성 - 기본키의 역할

  ```markdown
  "_id" : ObjectId("5e6ee81470642ecd7a6a29aa")
  				----------------------------
  				현재 timestamp + machine Id + mongodb프로세스id 
  				+ 순차번호
  				  -------
  				  추가될 때마다 증가
  ```

### update

* update를 위한 명령어

  * $set 

    : 해당 필드의 값을 변경 (업데이트를 하기 위한 명령어)

    none capped collection인 경우 업데이트할 필드가 없는 경우, 추가한다.

    > db.컬렉션명.update({조건필드: 값}, //sql의 update문 where절
    >
    > ​									{$set: {수정할필드: 수정값}, //set절
    >
    > ​                                    {update와 관련된 옵션: 옵션값});

  * $inc : 해당필드에 저장된 숫자의 값을 증가

  * $unset : 원하는 필드를 삭제할 수 있다.

  * 옵션

    * multi 

      : true를 추가하지 않으면 조건에 만족하는 document 중 첫 번째 document만 update

* document 수정

* 조건을 적용해서 수정하기 위한 코드도 json으로 구현

* save

  : 이미 중복된 document가 있으면 수정된 값으로 대체된다.

  ```javascript
  var x = db.score.findOne() // collection의 첫 번째 document를 리턴
  x.num = 120
  db.score.save(x);
  
  // ↓ 이렇게도 사용이 가능
  var x = db.score.find();
  for(var i=0; i < db.score.find().count(); i++) {
      x[i].num = 1000; 
      db.score.save(x[i]);
  };
  ```

### select

* findOne() : 첫 번째 document만 리턴
* count() : 행의 갯수를 리턴
* sort({필드명:sort옵션}) : 정렬
  * 1 : 오름차순
  * -1 : 내림차순
* limit(숫자) : 위에서부터 숫자만큼의 document만 조회
* skip(숫자) : 위에서부터 숫자만큼의 document를 skip하고 조회

* find

  > db.컬렉션명.find(조건, 조회할 필드에 대한 명시)
  >
  > `-`아무런 옵션이 없으면 전체 조회
  >
  > 조건, 조회할 필드에 대한 명시 모두 json

  * 조회할 필드의 정보 명시

    * 형식 :

      ```markdown
      {필드명:1} : 화면에 표시하고 싶은 필드
      {필드명:0}	: 명시한 필드가 조회되지 않도록 처리
      ```

  * 조건

    * $lt	 :	`<` **l**ess**t**han
    * $gt    :    `>`
    * $lte   :    `<=`
    * $gte  :    `>=`

    > ex) addr이 인천인 데이터 : id, name, dept, addr
    >
    > ​      db.score.find({addr:"인천"}, {id:1,name:1,dept:1,addr:1});
    >
    > ex) score컬렉션에서 java가 90점 이상인 document 조회
    >
    > ​	  (id, name, dept, java)
    >
    > ​	  db.score.find({java: {$gte:90}},{_id:0,id:1,name:1,dept:1,addr:1});

    * $or : 여러 필드를 이용해서 같이 비교 가능

      >db.score.find({$or:[{dept: "인사"},{addr: "인천"}]});

    * $and : and

    * $in : 하나의 필드에서만 비교

      >db.score.find({id:{$in:["song","hong","kang"]}});

    * $nin : not in

      ​			즉, 정의한 조건을 제외한 document를 조회

    * $exists : 입력한 값이 존재하는지 

      > db.score.find({servlet:{$exists:null}});

  * 정규표현식을 적용

    > db.컬렉션명.find({조건필드명:/정규표현식/옵션});
    >
    > ex) db.score.find({id:/kim|park/});

    * 기호

      * | : or

      * ^ : ^뒤의 문자로 시작하는지 체크

      * [] : 영문자 하나는 한 글자를 의미하고 []로 묶으면 여러 글자를 표현

        ​	  ex) [a-i] : a에서 i까지의 모든 영문자

    * 옵션

      * i : 대소문자 구분없이 조회 가능

        >db.score.find({id:/kim|park/**i**});

### delete

> mongodb에 저장된 데이터 삭제
>
> 조건을 정의하는 방법은 find()나 update()와 동일

* remove()

  > db.컬렉션명.remove({필드명:조건});
  >
  > ex) db.score.remove({servlet:{$lt:80}});

### 배열

* 배열에서 사용할 수 있는 명령어

  * $addToSet : 배열의 요소를 **1개** 추가

    > 없는 경우에만 값을 추가, **중복을 체크**

  * $push : 배열의 요소를 **1개** 추가

    > **중복을 허용**

  * $pop : 배열의 요소를 제거

    * 1 : 마지막 요소를 제거
    * -1 : 첫 번째 요소를 제거

  * $each 

    : addToSet이나 Push에서 사용할 수 있다.

    **여러 개**를 배열에 추가할 때 사용

    > `db.score.update({id:"jang"},{$push:{"info.city":{$each:["천안","가평","군산"]}}});`

  * $sort : 정렬 

    * 1 : 오름차순
    * -1 : 내림차순

    > `db.score.update({id:"jang"},{$push:{"info.city":{$each:["천안","가평","군산"],$sort:1}}});`

  * $pull : 배열에서 조건에 만족하는 요소를 제거 

    * 단, 조건은 오직 **1개**

    >`db.score.update({id:"jang"},{$pull:{"info.city":"천안"}});`

  * $pullAll : 배열에서 조건에 만족하는 요소 제거

    * 조건 **여러 개**

    >`db.score.update({id:"jang"},{$pullAll:{"info.city":["천안","군산"]}});`

### json

> **J**ava**S**cript **O**bject **N**otation라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**
>
> 어떤 프로그래밍 방식이 아닌 데이터 포맷

* 특정 언어에 종속되지 않는다.
* JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.

#### 문법

> "key" : "value"

* {} : json object
* [] : json array

## Aggregation

> 오라클의 group by와 동일하다.

* 간단한 집계를 구하는 경우 mapreduce를 적용하는 것 보다 간단하게 작업 가능

* pipeline을 내부에서 구현

  한 연산의 결과가 또 다른 연산의 input데이터로 활용

### 명령어(RDBMS와 비교)

* $match : where절, having절

  ```markdown
  $match:{필드명:{연산자:조건값}}
  			  -------------
  			  비교연산 or 조건이 여러 개
  ```

  >db.exam.aggregate([{$match:{addr:"인천"}},{$group:{_id:"$dept", num:{$avg:"$java"}}}]);

* $group : group by

  ```markdown
  {$group: {id: 그룹으로 표시할 필드명, 
  연산결과를 저장할 필드명:{연산함수:값}}
  							----
  							숫자나 필드참조
  ```

* $sort : order by

* $avg : avg 그룹함수

* $sum : sum 그룹함수

* $max : max 그룹함수

### 형식

```markdown
db.컬렉션명.aggregate(aggregate명령어를 정의)
					---------------------
					여러 가지를 적용해야 하는 경우 배열로
ex) addr별 인원수
	db.exam.aggregate([
			{$group:{_id:"$addr",
					 num:{$sum:1}}
			}
	]);
```

