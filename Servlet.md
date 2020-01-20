# Servlet

> 웹 상에서 자바코드가 실행되게 만들어주는 기술
>
> 서블릿은 클라이언트 페이지에서 발생하는 클라이언트의 요청을 처리하기 위한 기술
>
> ---
>
> 클라이언트로부터 요청이 전달되면 서버에서 실행되며 DB연동이나 서버의 자원을 엑세스하여 만들어진 결과를 클라이언트로 응답한다.
>
> ---
>
> 클라이언트의 요청을 인식하고 실행되도록 하기 위해서는 서블릿은 정해진 규칙대로 작성이 되어야 하고 서버가 서블릿을 찾아서 실행할 수 있도록 정해진 위치에 작성되어야 한다.
>
> ---
>
> 서블릿 객체는 **딱 한 번**만 메모리에 올라간다.
>
> ---
>
> **정해진 위치란?** 
>
> 표준화된 폴더 구조안에 있는 classes 폴더([서블릿 디렉토리](https://blog.naver.com/heaves1/221588663214)) - **시험문제1**

* 사용하는 라이브러리

  ![](images/servlet&jsp라이브러리.png)

* 서블릿 객체의 소멸

  * WAS의 reloading
  * Context의 reloading
  * 서블릿 컴파일

## <Servlet 작성규칙>

> 누가 실행해도 작동이 되어야 하기 때문에 작성 규칙이 존재한다.

* 표준화된 폴더 구조 안에서 서블릿 디렉토리에 저장되어야 한다.

  * classes 폴더

    ---

    ```markdown
    C:\iot\work\webwork\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps에서 찾는다.
    
    위의 경로 + serverweb\WEB-INF\classes에 작성되어야 한다.
    => 이 위치에 서블릿 클래스가 없으면 못 찾는다.
    ```

* public 클래스로 작성해야 한다.

  ```markdown
  서버가 찾아서 실행해야 하기 때문
  ```

* 서블릿 클래스를 상속해야 한다.

  ```markdown
  우리가 작성한 서블릿 클래스를 서버가 찾아서 생성하고 호출하기 위해서는 
  서버가 인식할 수 있는(서버가 사용할 수 있는) 타입이어야 하므로 
  **서버에 등록된 타입으로 서블릿 클래스를 작성**한다.
  ```

  ```markdown
  Servelet(Interface)
  	^
  	l
  GenericServlet	- 일반적인 내용을 담고 있는 서블릿
  	^
  	l
  HttpServlet		- http프로토콜에 특화된 내용을 담고 있는 서블릿
  	^
  	l
  MyServlet		- 내가 하고 싶은 일이 기술된 서블릿(**개발자가 만드는 서블릿**)
  ```

* 서버가 호출하는 메서드를 오버라이딩 해야 한다.

  ```markdown
  서블릿 클래스는 일반 클래스를 사용하는 방법처럼 객체생성해서 사용하는 클래스가 아니다.
  **서블릿이 호출되면 서버가 서블릿 객체를 생성하고 적절한 시점에 따라
  메서드를 자동으로 호출**한다.
  즉, 서블릿의 Lifecycle을 서버가 관리한다. 
  		  -----------
  		  객체를 생성하고 소멸시키는 것
  ```

  ```markdown
  서버가 적절한 시점에 따라 자동으로 메서드를 호출할 때 원하는 작업을 처리하기 위해서는
  **서버가 호출하는 메서드를 오버라이딩해서 내가 원하는 내용을 기술**해야 한다.
  ```

  * 오버라이딩할 메서드

    * `init` : 서블릿이 초기화 될 때 호출

    * `service` : 클라이언트가 요청을 하면 호출되는 메서드

      ```markdown
      클라이언트의 요청을 처리할 수 있는 내용을 기술
      ex) 로그인, 게시판 목록 보기, 회원가입.....
      ```

    * `doGet` 

      : `service`와 동일하게 동작하며 클라이언트가 get방식으로 요청하는 경우에만 호출

    * `doPost`

      : `service`와 동일하게 동작하며 클라이언트가 post방식으로 요청하는 경우에만 호출

    * `destroy` : 서블릿 객체가 소멸될 때 (메모리에서 해제될 때) 호출

* 서블릿을 등록

  ```markdown
  서버가 서블릿을 찾아서 실행할 수 있도록 서블릿을 web.xml에 등록하는 작업
  										--------
  										서블릿에 대한 내용을 등록하는 설정파일
  ```

  1. 서블릿 등록

     ```xml
     <!-- 사용할 서블릿이 어떤 클래스인지 web.xml에 정의 --> 
     <servlet>
       	<servlet-name>서블릿 이름(alias)</servlet-name>
       	<servlet-class>실제 사용할 서블릿클래스(패키지 포함)</servlet-class>
     </servlet>
     ```

     ```xml
     <!-- ex) basic 패키지에 작성한 FirstServlet을 first라는 이름으로 등록 --> 
     <servlet>
       	<servlet-name>first</servlet-name>
       	<servlet-class>basic.FirstServlet</servlet-class>
     </servlet>
     ```

  2. 서블릿 매핑

     ```xml
     <!-- 서블릿을 어떤 url로 요청할지 등록 -->
     <servlet-mapping>
       	<servlet-name>미리 등록한 서블릿의 이름</servlet-name>
       	<url-pattern>요청 url(반드시 '/' 나 '.'으로 시작)</url-pattern>
     </servlet-mapping>
     ```

     ```xml
     <!-- ex) 위에서 등록한 first서블릿을 /first.multi로 요청 --> 
     <servlet>
       	<servlet-name>first</servlet-name>
       	<servlet-class>/first.multi</servlet-class>
     </servlet>
     ```

## <Servlet 요청 방법>

### get 방식으로 요청

* 주소표시줄에 입력하고 요청

  > 테스트 용으로 사용

  ```markdown
  					server.xml에 등록한 path, 보통은 context명
  					------------
  http://localhost:8088/serverweb/first.multi
                           		-----------
                           		web.xml에 등록한 요청 path
                           		<url-pattern>에 등록
  ```

* 하이퍼링크를 클릭

  ```html
  <a href="http://서버ip:port/contextpath/서블릿요청url">하이퍼 링크</a>
  <a href="/contextpath/서블릿요청url">하이퍼 링크</a>
  ```

* `<form>`태그에서 method속성을 "get"으로 설정하고 submit버튼 선택

  > `action`속성에 설정한다.
  >
  > `form`태그를 정의하면서 method속성을 생략하면 get방식으로 요청된다.
  >
  > submit버튼을 눌러서 요청하면 `<form>`태그의 action속성에 정의한 서블릿이 요청(서블릿이 호출되어 실행되도록 한다.)되며 `<form></form>`내부에 정의한 모든 양식태그들의 `name`과 `value`가 서블릿으로 전달된다.

  ```html
  <form method="get" action="/contextpath/서블릿요청url">
      <input type="submit" value="전송"/>
  </form>
  ```

### post 방식으로 요청

* `<form>`태그에서 method속성을 "post"으로 설정하고 submit버튼 선택

>`action`속성에 설정한다.
>
>submit버튼을 눌러서 요청하면 `<form>`태그의 action속성에 정의한 서블릿이 요청(서블릿이 호출되어 실행되도록 한다.)되며 `<form></form>`내부에 정의한 모든 양식태그들의 `name`과 `value`가 서블릿으로 전달된다.

```html
<form method="post" action="/contextpath/서블릿요청url">
    <input type="submit" value="전송"/>
</form>
```

* 요청방식

  * get

    : 요청할 때 입력하는 내용이 url뒤에 추가되어 전송되는 양식

      (요청메시지 헤더에 추가)

      클라이언트가 입력하는 내용이 그대로 노출된다.

      전송할 수 있는 데이터의 크기에 제한이 있다.

    > 게시판 목록 확인하기, 상품정보 가져오기, 검색하기......

  * post

    : 요청메시지 body에 추가되어 전송되므로 클라이언트에 노출되지 않지만

      툴을 이용하면 확인할 수 있으므로 암호화해서 전송해야 한다.

      보낼 수 있는 데이터 크기에 제한이 없다.

      서버의 값을 클라이언트가 원하는 값으로 update(변경)하는 경우

    > 회원등록(insert), 회원정보 수정하기(update), 파일업로드, 메일쓰기....

## <클라이언트가 전달하는 요청 메시지에서 클라이언트의 입력 정보를 추출하기>

### 요청

* 요청

  >클라이언트가 요청 메시지를 서버로 전달하면 여러 가지에 클라이언트의 정보가(클라이언트가 입력한 데이터, 쿠키, 세션정보, ip, port...) 서버로 전달된다.
  >
  >서버는 이 데이터를 가지고 요청객체(요청객체를 만들면서 전달받은 데이터를 요청객체에 세팅하는 작업을 수행한다.)를 생성한다.

  ```markdown
  [요청객체]
  ServletRequest
  	^
  	l
  HttpServletRequest
  ```

  ```markdown
  http프로토콜에 특화된 내용은 => HttpServletRequest에서 찾는다.
  일반적인 내용 => ServletRequest
  ```

* 요청정보 추출

  > ex) -----/Servlet/login.do?id=lee&pass=1234
  >
  > **id**는 파라미터명 **lee**는 파라미터 value

  * `getParameter`

    > `ServletRequest`의 메서드로, 메서드를 호출하며 전달한 `name`에 대한 `value`를 리턴

    * 리턴값 

      : `String`으로 파라미터의 값

        ```markdown
      주소표시줄에 직접 넘긴 `value`로 =의 오른쪽에 있는 문자열
      `form`태그를 이용해서 사용자가 직접 입력한 값
        ```

    * 매개변수 

      : `String`으로 파라미터 이름

      ```markdown
      주소표시줄에 직접 넘긴 `name`으로 =의 왼쪽에 있는 문자열
      양식태그를 정의할 때 `name`속성에 정의한 값
      ```

      ```html
      <input type="text" name="id">
      					  <!---->
      				<!-- 파라미터명 -->
      ```

  * `getParameterValues`

    > `ServletRequest`의 메서드로 파라미터명이 같은 모든 `value`를 모아서 `String[]`로 리턴
    >
    > ex) `CheckBox`, `List`에서 복수개 선택, 임의로 동일한 이름을 정의해서 넘긴 데이터

    * 리턴타입 

      : `String[]`로 파라미터의 **값**들

    * 매개변수 

      : `String`으로 **파라미터명을 정의**

**※** `html`을 작성시 **`name`속성**은 반드시 DB에 정의된 **칼럼명과 동일하게** 맞춰줘야 한다.

### 응답

* 응답

  > 클라이언트가 요청한 내용을 처리하고, 처리결과를 웹 페이지에 출력되도록 응답해야 한다.
  >
  > 서블릿에서는 응답을 할 수 있도록 출력스트림을 지원한다.

  * 응답하는 문서의 타입과 인코딩방식을 정의

    ```java
    res.setContentType("응답형식(MIME타입);문자셋");
    res.setContentType("test/html;charset=euc-kr");
    ```

  * 응답객체에서 출력 스트림 얻기

    > `ServletResponse` 객체의 `getWriter`를 이용해서 리턴받는다.

    ```java
    PrintWriter pw = response.getWriter();
    ```

  * 메서드의 매개변수로 응답할 내용을 명시한다.

    => 실제로 불가능(추후에 개선된 내용으로 변경)

    => Ajax용

    ```java
    pw.메서드("출력할 내용");
    		//-----------
    		// html 태그
    ```

* 응답코드

  * **200** : 정상요청

  * **404** : 요청한 url에 맞는 파일을 찾을 수 없습니다.

  * **405** : 요청방식에 따라 실행되는 메서드가 없다.

    ​		  => 요청방식과 메서드명을 확인
    
  * **500** : 런타임 에러
  
    * 공유명 확인
    * DB조회 제대로 되었나 확인 (size 출력)
    * sql 점검
    * sysout으로 파라미터 출력
    * DBUtil에서 제대로 오라클과 연결되어 있는지 확인 

### 요청재지정

> 클라이언트로부터 들어온 최초 요청을 `servlet`에서 원하는 다른 자원으로 요청을 넘기는 것을 요청재지정이라 한다.

```markdown
요청재지정을 하는 목적은 서블릿에서 화면단을 분리시키고 분리시킨 화면이 응답하도록 하기 위해 필요하다.
웹을 개발하기 위해 사용하는 최적화된 패턴인 MVC패턴을 적용하기 위해 반드시 필요한 개념
```

* 데이터공유

  1. scope

     > page, request, session, application에 각각 map구조(key, value)의 저장소를 갖고 있고 그 저장소에 추가하고 저장소에서 꺼내온다.

     * page -> `javax.servlet.jsp.PageContext`

       > `jsp`문서내에서만 사용할 수 있다.

     * request -> `javax.servlet.ServletRequest`

       >한 번에 request에 대해서 처리하고 response하기 전까지 사용되는 모든 객체에서 공유

     * session -> `javax.servlet.http.HttpSession`

       >세션이 생성되고 사용되는 모든 것들이 공유할 수 있도록 세션이 생성되는 시점 로그인
       >
       >세션이 해제되는 시점 로그아웃(or 정해진 시간동안 사이트를 사용하지 않는 경우)

     * application -> `javax.servlet.ServletContext`

       > 모두공개 : 톰캣메모리에 공유
       >
       > => 로그인 유무와 상관없이 사용하는 모든 곳에서 공유

  2. 데이터 공유하는 메서드

     > 공유되는 데이터를 `attribute`라 한다.

     ```java
     모든객체(scope에 해당).setAttribute("공유할 attribute이름", 공유할 객체);
         												//-----------
         								 //자바에서 사용할 수 있는 모든 것
     ```

  3.  공유된 데이터 가져오기

     ```java
     java.lang.Object 
         = 모든객체(scope에 해당).getAttribute("공유된 attribute의 이름");
     ```

* 요청재지정 방법

  * 리다이렉트(`sendRedirect`)

    1. 문법

       : `HttpServletResponse`의 `sendRedirect`메서드를 이용해서 구현

       ```java
       response.sendRedirect("요청재지정될 web application의 경로");
       					//-----------------------------------
       					//html, jsp, 서블릿 모두 가능
       					// ㅣ
       			//"/contextpath/폴더명.../요청될 application의 path"
       			//ex) "/serverweb/dept/list.do"
       ```

       ex) 

       ```markdown
       1. 메일에서 누군가가 보낸 메일을 탭에 즐겨찾기 해놓음
       2. 인터넷 창을 모두 종료하고 다시 켬
       3. 즐겨찾기를 통해 해당 메일로 들어가면 로그인하라는 창으로 `sendRedirect`
       **즉, 방어코드를 작성하기 위해 사용하는 기능**
       ```

    2. 실행흐름
       * 클라이언트에서 요청한다.
       * 서블릿이 실행된다.
       * 서블릿의 실행이 모두 완료되면 클라이언트로 응답한다.
       * 서블릿에서 요청재지정한(`sendRedirect`에서 설정한) `jsp`파일을 다시 요청한다.
       * `jsp`페이지가 클라이언트에 응답된다. 
    3. 특징
       * 두 번 이상의 요청으로 처리되므로 데이터를 공유할 수 없다.
       * 주소표시줄이 마지막 요청path로 변경된다.

  * `forward`

    > `sendRedirect`와 다르게 한 번의 요청으로 모든 web application이 실행된다.
    >
    > 요청재지정된 application으로 모든 제어를 넘기기 때문에 요청재지정된 jsp파일이 응답된다.
    >
    > `RequestDispatcher`가 이런 일을 처리하는 객체

    1. 문법

       ```java
       RequestDispatcher rd 
           = request.getRequestDispatcher("요청재지정할 application 경로");
       								//------------------------------
       								//"/폴더.../application의 path"
       								//context의 path를 생략
       								//jsp, html, 서블릿 모두 가능
       rd.forward(request, response);
       		//-------------------
       		//forward하면서
       		//request와 response객체가
       		//전달되므로 같은 request를
       		//공유해서 사용할 수 있다.
       ```

    2. 실행흐름

       * 클라이언트가 서블릿을 요청한다.
       * 서블릿이 실행된다.
       * 서블릿이 클라이언트로 응답되지 않은 상태에서 `jsp`를 요청재지정(호출)
       * `jsp`가 실행되고 실행된 결과를 클라이언트로 응답한다. 

    3. 특징

       * 한 번의 요청으로 모든 application이 실행되므로 데이터 공유가 가능
       * 주소표시줄이 최초 요청된 서블릿path에서 변경되지 않는다.
       * **서블릿에서 주로 사용되는 요청재지정 방식**

  * `include`

    > forward와 동일하게 `RequestDispatcher`의 메서드를 이용하여 실행하며
    >
    > 요청재지정될 때 모든 제어를 `jsp`로 넘기지 않고 다시 서블릿으로 돌아와 서블릿이 응답된다.

    1. 문법

       ```java
       RequestDispatcher rd 
           = request.getRequestDispatcher("요청재지정할 application path");
       rd.include(request, response);
       ```

    2. 실행흐름

       * 클라이언트가 서블릿을 요청한다.
       * 서블릿이 실행된다.
       * 서블릿이 클라이언트로 응답되지 않은 상태에서 `jsp`를 요청재지정(호출)
       * `jsp`실행이 완료되면 `jsp`실행결과를 갖고 서블릿으로 되돌아온다.
       * 서블릿에서 최종 응답된다.

    3. 특징

       * `forward`와 동일
       * `jsp`에서 주로 사용하는 요청재지정 방식

## DB 연동

