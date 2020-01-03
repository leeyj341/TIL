# CSS

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

