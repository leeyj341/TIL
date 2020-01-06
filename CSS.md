# CSS

## 우선순위

1. 속성 값 뒤에 `!important` 를 붙인 속성
2. `HTML`에서 [`style`](https://ofcourse.kr/html-course/태그의-속성#style-속성)을 직접 지정한 속성
3. `#id` 로 지정한 속성
4. `.클래스`, `:추상클래스` 로 지정한 속성
5. `태그이름` 으로 지정한 속성
6. 상위 객체에 의해 **상속**된 속성

## 선택자

### 태그 선택자

> `body`,`p`,`a`,`div`등 다양한 태그를 기준으로 같은 태그끼리 동일한 스타일을 적용할 수 있다.

```css
a {
	color: #4285f4;
}
```

```css
div a {
	color: #4285f4;
	text-decoration: none;
}
```

태그 안에 정의된 하위 태그를 선택자로 사용할 수도 있다. 

```css
div.myclass {
	color: aqua;'
}
```

태그 안에 정의된 클래스 선택자로 스타일을 정의할 수 있다.

```css
h1, h2 {
	color: blue;
}
```

이런식으로 여러 태그에 한꺼번에 스타일을 정의할 수 있다.

### #id 

> 한 아이디는 단 하나의 요소에만 정의될 수 있기 때문에, 같은 아이디로 여러 요소의 스타일을 정의할 수 없다. 
>
> => 애초에 한 문서에서 같은 id를 가질 수 없다.

```html
<div id="mydiv">test</div>
<div id="mydiv">test2</div>			<!-- 이건 안돼 -->
```

### .class

> 여러 타입에 같은 이름의 클래스 선택자를 정의할 수 있어 여러 곳에 같은 스타일을 주고 싶을 때 사용한다.

```html
<div class="myclass">test</div>
<div class="myclass">test2</div>	<!-- 가능함 -->
```

## positioning

> `static`,`absolute`,`relative`,`fixed`,`inherit`등의 속성으로 웹 페이지 상에서 
>
> 요소의 위치를 정하는 것