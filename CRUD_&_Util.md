# CRUD

> Create, Read, Update, Delete
>
> 기본적인 데이터 처리 기능을 말한다.

## DAO

> Data Access Object
>
> DB관련 작업만 하는 클래스를 말한다

## VO or DTO

> Value Object
>
> Data Transfer Object

※ 데이터베이스와 통신 시에 사용하는 Design Pattern 중 하나이다.

# UTIL

## Vector

> 동시 접속에 대한 처리가 되어 있어 어플리케이션에 적합
>
> 기본적인 용량을 잡아놓고 그 이상 초과될 때 마다 현재 용량의 2배만큼 공간을 추가한다.

* <> (Generic)

  : **레퍼런스 타입** 자료형을 파라미터로 받을 수 있다.

  ```java
  Vector<Integer> v = new Vector<Integer>();
  ```

* 인덱스 접근

  : 배열이 기반이기 때문에 **인덱스로 접근**이 가능하다.

  ```java
  v.get(10);		//10번 인덱스에 있는 요소의 값을 가져온다.
  ```

* 기타 [API](https://docs.oracle.com/javase/8/docs/api/)

  ```java
  v.add(10);		//배열의 요소 추가
  v.size();		//배열의 사이즈
  v.capacity();	//배열의 용량
  .
  .
  .
  ```

## ArrayList

>동시 접속에 대한 처리가 없어 Web에 적합

```java
ArrayList<String> list = new ArrayList<String>();
list.add("자바");
list.size()
.
.
.
```

Vector와 유사하기 때문에 자세한 설명은 생략한다.

* [자료구조](https://onsil-thegreenhouse.github.io/programming/java/2018/02/18/java_tutorial_1-22/) 참고