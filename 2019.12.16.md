# 2019.12.16

## 1. 인터페이스

> 추상메서드만 모아놓은 특별한 클래스

공통된 특징으로 부모 클래스를 만들어 상속했는데 공통으로 가질 필요가 없는 메서드가 생겼을 때 인터페이스를 통해 구현할 수 있다.

```java
public class Duck {
    public void fly(){
        System.out.println("날다");
    }
}
public class PaperDuck {
    // 날 수 없다
}
public class RubberDuck {
    // 날 수 없다
}
public class MallardDuck {
    // 날 수 있다
}
public class TameDuck {
    // 날 수 있다
}
```

위의 경우 `interface`를 통해 '날다'라는 메서드를 구현해 구분지을 수 있다.

```java
public interface FlyingDuck {
    public void Fly();
}
// 날 수 없는 오리
public class RubberDuck extends Duck { 
}
// 날 수 있는 오리
public class TameDuck extends Duck implements FlyingDuck {
}
```

### * 특징

* **다중상속**이 가능하다.

  -> 하나의 클래스만 상속받을 수 있는 특성 때문에 인터페이스가 생겼다고 봐도 무방함

* 일반 메서드와 일반 멤버변수를 가질 수 없다.

  -> 모든 멤버변수는 **`public static final`**, 모든 메서드는 **`public abstract`**

* `interface`가 `interface`를 상속받을 수 있다.

=> 즉, 인터페이스는 **다형성**을 **극대화** 시키기 위해 사용하는 클래스다.

```java
public interface InterA {
}
public interface InterA {
}
public class SuperA {
}
// 이런 식으로 C++의 다중 상속과 비슷하게 구현할 수 있다.
public class SubA extends SuperA implements InterA, InterB {
}
```

## 2. Exception Handling

> 실행 시 발생할 수 있는 예외 또한 클래스로 관리하고 있다.

* 컴파일 에러

  : 컴파일 시에 발생하는 에러(주로 문법 오류)

* 런타임 에러

  : 실행 시에 발생하는 에러

* 논리적 에러

  : 실행은 되지만, 의도와 다르게 동작하는 것

### 1. 에러(Error)

: 프로그램 코드에 의해서 수습될 수 없는 심각한 오류

### 2. 예외(Exception)

: 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

> `Exception`클래스와 `Error`클래스는 `Throwable`클래스를 상속받고 있다.

### 3. 예외처리 방법

#### 1. `try`-`catch` 문

```java
try {
    //예외발생 가능성이 있는 코드
    String str = null;
    str.length();
} catch(Exception e) {	//Exception e = new NullPointerException();
    //예외 발생 시 실행할 문장
    System.out.println("str이 null이다");
	System.out.println("예외 메시지 : " + e.getMessage());
} finally {
    //예외발생 하든 안하든 반드시 실행해야 하는 명령문
}
```

```markdown
str이 null이다
예외 메시지 : null
```

`NullPointerException`이 발생해서 `catch`블럭의 내용을 수행한다. **`Exception`클래스가 모든 예외 처리 클래스의 부모**이기 때문에 해당하는 예외 처리 결과가 보여졌다.

=> **그러나** 이렇게 상위 클래스를 사용하는 것이 아니라, 각각 **에러에 맞는 클래스**를 **사용**할 수 있도록 해야 한다.

* 다양한 Exception의 처리를 위해서 catch블럭을 **여러 개 정의**하고 사용할 수 있다.
* **상위 타입**에 속하는 Exception은 **가장 나중에 정의**해야 한다.

#### 2. `throws`

> **API 메서드 선언부**에 이 명령어가 추가되어 있으면 **반드시 예외처리**를 해주어야 한다.

```java
try {
	FileInputStream fs = new FileInputStream("test.txt");
	System.out.println(fs.read());
	System.out.println(Integer.parseInt("1234"));
	System.out.println(Integer.parseInt("1234"));
} catch(FileNotFoundException e) {
	System.out.println("파일을 찾을 수 없습니다.");
	//파일을 다시 선택할 수 있도록 처리하는 코드 필요
} catch (IOException e) {
	System.out.println("파일을 읽을 때 오류가 발생했습니다.");
}
```

`FileNotFoundException`이나 `IOException`같은 경우 위에서 언급한 바와 같이 예외처리를 해주지 않으면 컴파일 오류가 발생하지만 `Integer`의 `parseInt`메서드는 그렇지 않다.

* `NumberFormatException`은 **`RuntimeException`**이기 때문에 **문법적으로 제한하지 않아** 컴파일 오류가 발생하지 않는다. 

  => 제한하지 않더라도 처리해주는 것이 좋다.

> **메서드 선언부에 `throws`키워드**를 추가하면 그 메서드를 실행하는 다른 메서드에게 오류를 알려줄 수 있고, **같은 오류**라도 **다른 방식**으로 처리할 수 있다.

```java
public int test(int num1, int num2) throws ArithmeticException {
	int result = num1 / num2;
	return result;	
}
//예외를 호출하는 곳에서 직접 처리하기
public void show() {
	int result = 0;
	int num1 = 0;
	int num2 = 0;
	try {
		Scanner key = new Scanner(System.in);
		System.out.print("숫자입력: ");
		num1 = key.nextInt();
		System.out.print("숫자입력: ");
		num2 = key.nextInt();
		result = test(num1, num2);
	} catch (ArithmeticException e) {
        //똑같은 예외지만 다양하게 처리하고 있음
		if(num1 % 10 == 0) result = 1000;
		else if(num1 % 7 == 0) result = 10000;
		else result = 100;
	} finally {
		//무조건 실행되어야 하는 명령문
		System.out.println("test() 호출결과: " + result);
	}	
}
```

위의 경우 `throws ArithmeticException`를 통해 처리하는 쪽이 아닌 **호출하는 쪽에서 에러를 발생**시키고 있다. 

이렇게 예외를 발생시키면 `try-catch`문과 다르게 **같은 예외라도 다르게 처리**할 수 있어 프로그래머가 **유연한 코드를 작성**할 수 있도록 해준다.

#### 3. `throw`

> 프로그래머가 **고의로 발생**시키는 예외

```java
public static void main(String[] args) {
	try {
        //자동인지가 아닌 고의로 발생시키는 에러이기 때문에 new 사용
		throw new Exception("고의로 발생시킴");
	} catch (MyException e) {
		System.out.println("에러 메시지: " + e.getMessage());
	}
}
```

예외가 발생할 상황이 없지만 고의로 예외를 발생시켰다. 

예로, 잔액을 출금하는 메서드에 잔액이 0원이라면 에러가 발생해야 하지만 **Java언어 상에서 0은 오류로 정의되어 있지 않다.**

이런 경우에 위의 **`throw`키워드를 사용**해 **고의로 에러를 발생**시킬 수 있다.

#### 4. 기타 

> 사용자 정의 `Exception`

```java
public class MyException extends Exception {
	public MyException(String message) {
		super(message);
	}
}
```

나만의 `Exception`을 만들었으나 **JVM이 인지하지 못하는 오류 사항**이기 때문에 발생시키는 것도 프로그래머가 해야 한다.

위에서 설명한 **`throw`**키워드를 통해 **사용자가 정의한 `Exception`**을 발생시킬 수 있다.