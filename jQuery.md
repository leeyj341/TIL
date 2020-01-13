# jQuery

> 일종의 자바스크립트 라이브러리
>
> 자바스크립트의 프로그래밍 양을 줄일 수 있다.

```javascript
//페이지가 로딩되고 dom객체가 형성이 되면 익명의 함수를 실행하겠습니다.
$(document).ready(function() {
    alert("jQuery시작.......");
})
```

`window.onload`와 같다. 

=> 윈도우가 시작되면 실행한다.

* 자바스크립트 라이브러리
  * DOM
  * Ajax

## 선택자

> css처럼 `*`은 전체, `id`는 `#`, `class`는 `.`, `tag`는 그냥 태그이름으로 선택자를 지정한다.

```javascript
$(document).ready(function() {
	$("*").css("color", "blue");

	$("#tag").on("click", function() {
		$("p").css("color", "orange");
	})
    
	$("#id").on("click", function() {
		$("#myid").css("color", "red");
	})
    
	$("#class").on("click", function() {
		$(".myclass").css("color", "yellow");
	})
})
```

* `[]`

  : 속성으로 접근할 수 있는 선택자

  ```javascript
  $("#href").on("click", function() {	
      //href속성을 가진 모든 요소에 접근
  	$("[href]").css("color","skyblue");
  });
  ```

  ```javascript
  $("#attrVal").on("click", function() {	
      //a태그의 target속성이 _blank가 아닌 요소에 접근해 css 속성 변경
  	$("a[target!='_blank']").css("color","pink");
  })
  ```

* `:?`

  : 타입이 ?인 요소에 접근할 수 있음

  ```javascript
  $("#inputbutton").on("click", function() {	
      //type이 버튼인 것만 골라 작업
  	$(":button").css("color","green");
  });
  ```

* 기타

  ```javascript
  $("#treven").on("click", function() {	
      //table row가 짝수면 css속성 변경(0부터 시작)
  	$("tr:even").css("background-color","blue");	
  })
  
  $("#trodd").on("click", function() {	
      //table row가 홀수면 css속성 변경
  	$("tr:odd").css("background-color","yellow");	
  })
  ```

## json

> 속성을 여러 개 주고 싶을 때 사용한다.

```javascript
$("#changeColor").on({"click":function() {
						$("#mydiv").css("color", "blue");
						},
                      "mouseover":test});// callback으로도 사용가능
```

```javascript
$("#main").children().first().css({"color":"orange", 
                                   "border":"solid 1px red"});
```

`{}`을 이용해 안에 여러 개의 기능 및 속성을 적용할 수 있다.

## UI

> [jQuery에서 제공하는 기본 UI](https://jqueryui.com/)가 있다.

* `draggable`예시

  ```html
  <!doctype html>
  <html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>jQuery UI Draggable - Default functionality</title>
    <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
    <link rel="stylesheet" href="/resources/demos/style.css">
    <style>
    #draggable { width: 150px; height: 150px; padding: 0.5em; }
    </style>
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
    <script>
    $( function() {
      $( "#draggable" ).draggable();
    } );
    </script>
  </head>
  <body>
  	 <!-- div의 id를 반드시 draggable로 설정해야 한다. -->
  	<div id="draggable" class="ui-widget-content">
          <p>Drag me around</p>
  	</div>
  </body>
  </html>
  ```

  