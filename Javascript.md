# Javascript

## 공부 순서

**<초급>**

1. 문법

   * 사용방법
   * 변수
   * 제어구문

2. 함수

3. 객체

    * 내장객체

      String, Array, Date, Math

4. 이벤트 핸들러

5. 브라우저객체모델(BOM)

**<중급>**

1. DOM
2. JSON
3. Ajax
4. 자바스크립트 프로토타입
   * 사용자 정의 객체
   * 클로저

**<고급>**

자바스크립트의 프레임워크 사용

1. bootstrap - css와 javascript의 프레임워크

2. MEAN stack 

   * **M**ongoDB
   * **E**xpressJs(express.js)
   * **A**ngularJs
   * **N**odeJs

   => Input, Ouput이 빈번하게 발생하는 프로그램 작성 시 유용한 기술

3. ReactJs - 웹 UI개발에 사용(facebook이 공개한 오픈소스 라이브러리)

4. Vue.js

5. D3

## 자바스크립트 사용 방법

1. `body` 태그 안에 직접 정의

```html
<body>
	<script type="text/javascript">
		document.write("<h1>브라우저에 데이터 출력하기 - 연습용</h1>");
	</script>
</body>
```

`dodument.write()`는 거의 사용하지 않지만 디버깅 시 사용하면 좋다.

=> 자바의 `sysout`과 같은 기능을 한다.

2. `head` 태그 안에 `function`을 정의하고 사용

```html
<head>
	<script type="text/javascript">
		function test() {
			alert("테스트 중 - 자바스크립트 사용방법");		
		}	
	</script>
</head>
<body>
	<script type="text/javascript">
		test();
	</script>
</body>
```

3. 태그 내부에서 inline으로 사용 : 이벤트 핸들러에 연결

```html
<input type="button" value="자바스크립트 실행하기" onclick="alert('안녕');">
<input type="button" value="자바스크립트 함수 호출" onclick="test();">
```

4. 외부문서로 작성하고 호출하기

   * .js 파일 내부

   ```javascript
   function test2() {
   	alert("test... 테스트");
   }
   ```

   * .html 내부

   ```html
   <!-- head 안 -->
   <script type="text/javascript" src="/clientweb/common/js/test.js"></script>
   
   <!-- body 안 -->
   <script type="text/javascript">
   		test2();
   </script>
   <a href="javascript:test();">연결하기</a>
   ```

## 변수

* var

  : 데이터 타입을 지정하지 않기 때문에 선언한 변수에 정수나 문자열 모두 저장할 수 있다.

  * **함수 안**에 **var** 타입으로 변수 선언시 **지역변수**로 작동한다.
  * **함수 밖에서 선언**되면 타입을 떠나 **무조건 전역변수**로 작동한다.

### 특징

* 자바 스크립트에서 정수 나누기 정수는 정수가 아니다.

  => `parseInt()`나 `Math.floor()`를 통해 정수화 시켜야 한다.

## 함수

> 자바와 비슷하기 때문에 함수도 같은 형식으로 사용할 수 있다.
>
> 다만, `return`값이 있는 함수는 자바와 조금 형식이 다른데 그 예는 아래와 같다.

```html
<script type="text/javascript">
    function test3(num1, num2) {
		result = num1 + num2;
		return result;
	}
</script>
```

자바에서는 메서드에 리턴 형식을 적어줘야 하지만 **자바스크립트는 데이터 타입을 지정할 필요가 없기 때문에** return 값이 있는 함수는 위처럼 사용할 수 있다.

### 이벤트 핸들러

> `onclick`과 같이 `html`태그에서 데이터 타입으로 `EVENT`를 받는  속성들을 말한다.

