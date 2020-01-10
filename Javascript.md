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

* `var`

  : 데이터 타입을 지정하지 않기 때문에 선언한 변수에 정수나 문자열 모두 저장할 수 있다.

  * **함수 안**에 **`var`** 타입으로 변수 선언시 **지역변수**로 작동한다.
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

자바에서는 메서드에 리턴 형식을 적어줘야 하지만 **자바스크립트는 데이터 타입을 지정할 필요가 없기 때문에** `return` 값이 있는 함수는 위처럼 사용할 수 있다.

### 이벤트 핸들러

> `onclick`과 같이 `html`태그에서 데이터 타입으로 `EVENT`를 받는  속성들을 말한다.

### 함수의 호이스팅

>함수의 변수 등 Global영역에 추가해야 하는 것들을 먼저 추가하고 다른 스크립트 명령문을 읽기 때문에 아래와 같이 작업해도 오류가 발생하지 않는다.
>
>이를 **함수의 호이스팅**이라 한다.

```html
<script type="text/javascript">
	test(90);
	function test(num){
		if(num>90){
			alert("성공");
		}else{
			alert("실패");
		}
	}
</script>
```

**함수가 선언되기 전에 호출되는 명령문을 정의**하는 것은 **코드를 엉성하게 만들고** 함수의 선언문이 많이지게 되면 이를 읽어서 글로벌영역에 추가하는 시간이 소요되므로 웹 페이지를 response할 시간이 늦어진다. 고로 권하지 않는다.

## BOM

> 웹 브라우저가 가진 모든 객체로, 브라우저 객체 모델이라고 한다.
>
> 브라우저에 출력되는 모든 구성요소를 객체로 정의하고 접근
>
> 모든 객체는 계층구조를 가지고 있다.

* `window.document... `이런 식으로 각 객체에 접근이 가능하다
  * `window.document.폼객체.텍스트객체`
  * `window.document.myform.id.속성(메소드)`
  * **`window`**는 보통 **생략이 가능**하다.

### window

1. 대화상자

   > 클라이언트가 볼 수 있는 팝업창으로 내용을 띄워주는 기능

   * `alert`

   * `prompt`

     > 클라이언트에게 팝업으로 입력받는 창을 띄워주는 기능

   * `confirm`

   ```html
   <script type="text/javascript">
   	data = myform.num1.value;
   	alert("문자열의 길이 => " + data.length);
       confirm("문자열의 길이 => " + data.length);
       //prompt는 입력창을 제공한다
       prompt("숫자를 입력하세요.");
   </script>
   ```

2. popup

   * `open`

     > 팝업창을 연다.

   * `close`

     > 팝업창을 닫는다.

   ```html
   <script type="text/javascript">
   	mypopup2 = window.open("js_popup.html", "mywin", "width=300, height=300, top=100, toolbar=yes");
       close();
       // window는 생략이 가능하다.
   </script>
   ```

3. 자동실행

   * `setTimeout`

     >매개변수로 실행할 행동과 시간을 받는다.

     ```html
     <script type="text/javascript">
     	window.setTimeout("location.href='https://www.naver.com'", 3000);
         // 3초 뒤에 naver 사이트로 이동한다.
     </script>
     ```

   * `setInterval`

     > 위와 마찬가지로 실행할 행동과 시간을 받지만,
     >
     > 이 함수는 지정한 시간마다 지정한 행동을 반복한다.

     ```html
     <script type="text/javascript">
     	jobid = window.setInterval(showTime, 1000);
         // showTime 메서드를 1초마다 실행
         // jobid 객체에 담은 이유는 clearInterval에서 사용하기 위함
     </script>
     ```

   * `clearInterval`

     > 실행되고 있는 setInterval을 지운다.

     ```html
     <script type="text/javascript">
     	window.clearInterval(jobid);
         // 위에서 실행했던 setInterval 객체를 지운다.
     </script>
     ```

4. 데이터처리

   * `parseInt`

     > 문자열을 숫자 형태로 바꿔준다.

   * `isNaN`

     > 매개변수의 값이 문자이면 `true` 숫자이면 `false`를 반환한다.

   * `eval`

     > 매개변수로 받은 식이나 연산을 실제로 실행한다. 
     >
     > => **보안에 취약**하다.

     ```html
     <script type="text/javascript">
     	myform.mytext.value = eval(myform.mytext.value);
         // myform의 mytext라는 이름을 가진 text 내용을 계산해서 다시 그 내용에 갱신
     </script>
     ```

   * `trim`

     > 공백을 제거한다.

     ```html
     <script type="text/javascript">
         // value가 'text   '인 경우
     	data = myform.num1.value;
     	alert("문자열의 길이 => " + data.length); // 7
     	data2 = data.trim();
     	alert("문자열의 길이 => " + data2.length);// 4
     </script>
     ```

### location

> 문서의 주소와 관련된 객체로 window객체의 프로퍼티

* `href` 프로퍼티

  ```html
  <script type="text/javascript">
  	window.setTimeout("location.href='https://www.naver.com'", 3000);
      // href 프로퍼티에 이동할 주소로 네이버의 주소를 넣어줬다
      // =을 사용해 값을 넣어주지 않으면 현재 윈도우의 주소를 반환한다.
  </script>
  ```

* `toString` 메서드

  > 현재 윈도우의 주소를 String형식으로 반환

* `reload`메서드

  > 새로고침

### document

> 현재 문서에 있는 객체에 접근할 수 있게 해주는 객체

```html
<script type="text/javascript">
	mycheck = document.cbfmt.food;
</script>
<form name="cbfmt">
    <label>아이스크림</label> 
	<input type="checkbox" name="food" value="아이스크림" id="ice"> 
</form>
```

### form(양식 태그)

* form태그와 form태그 하위 태그를 객체로 접근하기 위해서 name속성을 정의하고 접근

  ```html
  <form name="myform">
     	아이디 :<input type = "text" name = "id">
     	패스워드 :<input type = "password" name = "pass">
  </form>
  ```
  
  ```html
  <script type="text/javascript">
  	myid = document.myform.id.value;
  </script>
  ```

- id를 정의하는 경우

  ```html
  <div id = "mydiv"></div>
  ```
  
```html
  <script type="text/javascript">
  	div1 = document.getElementById("mydiv");
  </script>
  ```

### image

## DOM

> 문서 객체 모델, 브라우저가 HTML 문서를 내부적으로 표현하는 표준 모델
>
> HTML 문서의 계층적인 구조를 트리로 표현

* node

  > 트리에 있는 하나의 잎을 **노드(node)**
  >
  > 노드는 문서 안에 들어있는 요소나 텍스트를 나타낸다.

  ```html
  <html>
      <head>
          <title>My title</title>
      </head>
      <body>
          <h1>A heading</h1>
          <a href="#">Link text</a>
      </body>
  </html>
  ```

  HTML 문서 안 모든 태그가 노드가 된다. (공백도 노드로 취급)

  * DOCUMENT_NODE : HTML 문서로 `window.document`와 같다
  * ELEMENT_NODE : HTML 요소(`body`,`a`,`p`,`script`,`style`,`html`,`h1` 등)
  * ATTRIBUTE_NODE : 속성을 나타내는 노드로 `class="myClass"`와 같은 속성
  * TEXT_NODE : 요소 안에 들어있는 텍스트를 나타내는 노드

### 요소 찾기

```javascript
document.getElementById("id");
document.getElementsByTagName("div(와 같은 태그들 모두 사용 가능)");
```



