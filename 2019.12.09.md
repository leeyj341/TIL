# 2019.12.09

## 0. 배열 및 명령행 매개변수

```java
// 자바 스타일의 배열 선언, 생성, 초기화
int[] myArr = new int[] {10, 20, 30, 40, 50};
```

* 메인 메서드의 매개변수(args)

> 커맨드 라인에서 `java class`명령을 사용해 실행할 때 뒤에 `client1` `client2`와 같은 매개 변수를 주면, 각각 다른 명령을 실행할 수 있게 해주는 역할을 함. 

```java
public static void main(String[] args) {}
```

ex) `c:\iot\exam java class ip port` 이런식으로 사용할 수 있음

## 1. 다차원 배열

> 배열을 참조하는 배열, `[][]...` 이렇게 원하는 차원만큼 배열을 생성할 수 있음.

```java
int[] arr = new int[3][3];

int[][] myArr1 = {
				{1, 2, 3, 4, 5},
				{6, 7, 8, 9, 10},
				{11, 12, 13, 14, 15}
		}; // int[][] myArr1 = new int[3][5];

// 배열이 참조하는 배열 요소의 갯수를 각각 다르게 정의도 가능
int[][] myArr = new int[3][];
		myArr[0] = new int[3];
		myArr[1] = new int[2];
		myArr[2] = new int[1];

int[][] myArr2 = {
				{1, 2, 3},
				{6, 7, 8, 9},
				{11, 12, 13, 14, 15}
		}; // int[][] myArr2 = new int[3][];
```

이런식으로 다양한 차원의 배열을 선언해 사용할 수 있다.



