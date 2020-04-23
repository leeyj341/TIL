## 0. Java Application

```java
public static void main(String[] args){}
```

`java interpreter`가 위 함수를 인식해 실행되는 것을 `java application`이라고 함.

## 1. 변수

> 데이터 타입 변수명 = 초기화 작업;

```java
int num = 0;
```

### 1. 기본형	

1. 문자 (char)

2. 숫자 (byte, short, int, long, float double)

3. boolean

### 2. 참조형

* API에 포함된 클래스
* 내가 만든 클래스

> class 클래스명 = new 초기화;

```java
String str = new String();
```

`new`를 사용해 `heap`메모리에 올려준다. (= 동적할당)

* `String`같은 클래스같이 기본으로 제공되는 것들을 `java api`라고 한다.

## 2. 연산자

* `&&` `||` 비교 연산자 or 쇼트 연산자라고도 부름
* `+` `-` `*` `/` 사칙연산 
* `&` `|` `^` `<<` `>>` 과 같은 비트 연산자

## 3. 제어구문

* 순차형

* 선택형

  * 조건문

  ```java
  if(1 > 0) System.out.println("1은 0보다 크다");
  
  switch(num) {
      case 0:
          break;
      case 1:
          break;
  }
  ```

* 순환형

  * 반복문