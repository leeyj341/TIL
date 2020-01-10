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

