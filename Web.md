# Web

* Web Server

  : 웹 상에서 작업할 수 있는 프로그램이 설치된 pc

* IIs apache, tomcat

  : 웹 서버 실행 프로그램

* ip

  : 컴퓨터의 주소

* port

  : 해당 ip에 접속할 수 있는 입구라고 생각하면 된다.

* 도메인

  : 이름으로 매핑된 ip에 접근할 수 있게 해준다.

## WAS

>Web Application Server
>
>자바언어를 실행하고(컨테이너) 웹 상의 작업도 같이 할 수 있도록 도와주는 프로그램

### 설치 방법

* apache.org

  > tomcat 9 [32-bit/64-bit Windows Service Installer](http://mirror.apache-kr.org/tomcat/tomcat-9/v9.0.30/bin/apache-tomcat-9.0.30.exe) ([pgp](https://www.apache.org/dist/tomcat/tomcat-9/v9.0.30/bin/apache-tomcat-9.0.30.exe.asc), [sha512](https://www.apache.org/dist/tomcat/tomcat-9/v9.0.30/bin/apache-tomcat-9.0.30.exe.sha512)) 설치
  >
  > 설치 과정에서 포트번호를 설정하는데 일단 임의로 번호를 부여한다.
  >
  > -> 8080은 window10의 기본 포트이기 때문에 사용할 수 없다.

* 시작 후 Monitor Tomcat 실행

  > 작업 표시줄에 아이콘 오른쪽 클릭 후 start service

  * C:\Program Files\Apache Software Foundation\Tomcat 9.0\webapps\ROOT에 있는 index.jsp 파일을 수정해 첫 페이지를 수정할 수 있다.

## View

> 사용자에게 보여지는 화면
>
> html, css, javascript, jquery 등을 사용해 구현한다.

* html 

  : 사용자에게 보여지는 구성요소를 만듬

<img src="images/html.png" style="zoom:67%;" />

* css

  : client style sheet 라고 하며 디자인 적 요소를 추가할 수 있는 언어

<img src="images/css.png" style="zoom: 67%;" />

* javaScript

  : 반응형 웹 페이지를 만들 수 있게 해준다. (대화형 페이지)

즉, 뼈대(html), 살(css), 움직임(javaScript)을 구현하는 과정이라고 말할 수 있다.

## 서버기술 Application

> Php, Asp, jango... 자바에서는 servlet, jsp
>
> 웹 서버와 DB Server를 연결해주는 프로그램