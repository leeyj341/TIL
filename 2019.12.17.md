# 2019.12.17

## 1. API

### 1. java.lang 패키지

#### * `Object`클래스

* `equals()`

> 두 참조변수가 같은 객체를 참조하고 있는지 판단, `true`와 `false`를 리턴한다.

* `toString()`

> **기본 메서드**로 **생략이 가능**하다.

```java
Object obj1 = new Object();
System.out.println(obj1); // obj1.toString()호출과 동일
						  // 기본 메서드이므로 생략 가능
```

단, [`String`]([file:///C:/iot/setup/jdk-8u231-docs-all/docs/api/index.html](file:///C:/iot/setup/jdk-8u231-docs-all/docs/api/index.html))클래스는 예외이다. 

API문서를 보면 알겠지만 자체 클래스 내에서 **오버라이딩**이 되어있기 때문이다.

#### * `String`클래스

* `equals()`

> `Object`의 `equals`메서드를 오버라이딩 해 **문자열끼리 비교**한다.

```java
String str1 = "java";
String str2 = new String("java");

if(str1 == str2) {//다르다.
	System.out.println("같다.");
} else {
	System.out.println("다르다.");
}
if(str1.equals(str2) {//같다.
	System.out.println("같다.");
} else {
	System.out.println("다르다.");
}
```

* 기타 메서드

```java
String str1 = new String("java programming");
String str2 = new String("재밌다.");
```

```java
//해당하는 인덱스의 문자를 리턴
System.out.println("str1.charAt(1) => " + str1.charAt(1)); 
//a
```

```java
//문자열 합치기
System.out.println("str1.concat(str2) => " + str1.concat(str2));
//java programming재밌다.
```

```java
//해당하는 문자의 인덱스 리턴
System.out.println("str1.indexOf('a') => " + str1.indexOf('a'));
//1
```

```java
//해당하는 문자의 인덱스가 없으면 -1을 리턴
System.out.println("str1.indexOf('합') => " + str1.indexOf('합'));
//-1
```

```java
//마지막으로 나오는 해당 문자의 인덱스 리턴
System.out.println("str1.lastIndexOf('a') => " + str1.lastIndexOf('a'));
//10
```

```java
//문자열의 길이 리턴
System.out.println("str1.length() => " + str1.length());
//16
```

```java
//문자열 비교(대소문자 포함)
System.out.println("str1.equals(\"java programming\") => " + str1.equals("java programming"));
//true
System.out.println("str1.equals(\"Java programming\") => " + str1.equals("Java programming"));
//false
```

```java
//대소문자 비교 안함
System.out.println("str1.equalsIgnoreCase(\"java programming\") => " + str1.equalsIgnoreCase("java programming"));
System.out.println("str1.equalsIgnoreCase(\"Java programming\") => " + str1.equalsIgnoreCase("Java programming"));
//true
```

```java
//문자열 비교 - prefix (대소문자 비교함)
//해당 문자열로 시작하는지 판단 후 결과 리턴
System.out.println("str1.startsWith(\"java\") => " + str1.startsWith("java"));
//true
System.out.println("str1.startsWith(\"Java\") => " + str1.startsWith("Java"));
//false
```

```java
//문자열 비교 - suffix
//해당 문자열로 끝나는지 판단 후 결과 리턴
System.out.println("str1.endsWith(\"ming\") => " + str1.endsWith("ming"));
//true
```

```java
//해당 문자열 대문자로 변경
System.out.println("str1.toUpperCase() => " + str1.toUpperCase());	
//JAVA PROGRAMMING
```

```java
//해당 문자열 소문자로 변경
System.out.println("str1.toLowerCase() => " + str1.toLowerCase());
//java programming
```

```java
//인덱스 2번부터 전체 다
System.out.println("str1.substring(2) => " + str1.substring(2));
//va programming
```

```java
//인덱스 2번부터 8번 전까지(7)
System.out.println("str1.substring(2) => " + str1.substring(2, 8));
//va pro
```

```java
//매개변수로 받은 2개의 문자 중 앞 문자를 뒤 문자로 변환
System.out.println("str1.replace('a', 'A') => " + str1.replace('a', 'A'));
//jAvA progrAmming
```

위 메서드들을 모두 사용해도 원본데이터는 유지된다. 

**원본을 변경하는 것이 아니라 새로운 `String`객체를 생성하여 수정**을 하기 때문이다.

따라서, `String`객체는 **문자열 조작이 빈번**하게 일어난다면 **효율적이지 못하다**.

* `StringBuffer`

> 동시접속에 대한 고려가 되어 있음 (Android...)
>
> => 멀티 쓰레드 환경

* `StringBuilder`

> 동시접속에 대한 고려가 되어있지 않음 (Web...)
>
> => 단일 쓰레드 환경

문자열 조작이 빈번하게 일어난다면 `StringBuffer`나 `StringBuilder`를 사용하는 것이 훨씬 효율적이다.

굳이 성능에 대해 순서를 매긴다면 `StringBuilder > StringBuffer > String`순으로 빠르다.

* `String`의 다양한 변환

```java
String str1 = new String("java programming");
String str2 = new String("java oracle servlet jsp spring");
```

```java
//1. String -> byte[]
byte[] data1 = str1.getBytes();
```

```java
//2. String -> char[]
char[] data2 = str1.toCharArray();
```

```java
//3. String -> String[]
String[] data3 = str2.split(" ");
```

**매개변수**로 받은 **문자열을 기준**으로 문자열을 자른 뒤 **배열에 담아 리턴**한다.

```java
//4. 기본형 -> String
int i = 1000;
double d = 10.0;
test(String.valueOf(i));
test(String.valueOf(d));
test(i + "");
test(d + "");

public static void test(String data) {
	System.out.println("전달된 데이터 => " + data);
}
```

`String`클래스 안에 내장되어 있는 `static`메서드인 `valueof()`를 사용해도 되고 빈 문자열을 더해 문자열로 바꿔줘도 된다.

#### * `StringBuffer`클래스

> `StringBuilder`와 거의 비슷하기 때문에 메서드도 같이 보면 된다.

```java
StringBuffer sb = new StringBuffer("java programming");
```

```java
//맨 끝에 추가하는 작업
sb.append("재밌다");
//java programming재밌다
```

```java
//해당 index위치에 문자열을 추가
sb.insert(2, "자바");
//ja자바va programming재밌다
```

```java
//begin index부터 ~ end-1까지 삭제
sb.delete(2, 6);
//ja programming재밌다
```

```java
//문자열을 뒤집는다.
sb.reverse();
//다밌재gnimmargorp aj
```

문자열 조작이 빈번하면 이렇게 `StringBuffer`나 `StringBuilder`클래스를 사용하면 된다.