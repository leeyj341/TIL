# R

> 데이터 분석 소프트웨어

## 설치

> 컴퓨터 이름, 사용자 이름, 상위 폴더 이름에 한글, 특수문자, 기호가 포함되면 안됨

* R

  : 우리나라에서 접속할 것이기 때문에 한국에 서버를 두고 있는 미러 사이트 중 아무거나 클릭해서 다운받는다. (CRAN)

  * 경로는 program files가 아니라 iot/bigdata로 설정한다.

* Rstudio

  > R을 편리하게 실행할 수 있게 해주는 툴의 개념

## 실행

> Rstudio로 R을 실행한다.

### 명령

* ?

  : 뒤에 검색할 명령을 입력하면 해당 명령에 대한 정보를 help 창에 보여줌

### 단축키

* Alt + `-` : `<-`(할당)
* Alt + Home : 현재 커서가 있는 문장 전체 선택

### 함수

* class() : 현재 변수의 자료형(타입)을 알려주는 함수

* as

  * .character() : as객체의 함수로 매개변수를 캐릭터형으로 변경

    > `test <- as.character(result1)`

  * .numeric() : 숫자형으로 변경

* c() : combine

* seq() : 연속 값을 지닌 변수를 만듬

  * by : 뒤에 주는 수만큼 건너뛴다

* names() : 벡터의 이름을 출력

* length() : 요소의 갯수를 리턴

* mean() : 평균 리턴

* cbind

* rbind

## 데이터 구조

* vector 

  > `myvector <- c(100,200,300)`

  * 인덱스 접근이 가능하다. (1부터 시작)

  * 연산 가능

    >myvector * 2
    >myvector + 20

  * 벡터끼리 연산도 가능

    > myvector + myvector2

* data frame

  > 행과 열로 구성된 2차원 데이터 구조로, 다양한 변수 타입을 구성이 가능하다

  ```R
  # matrix를 dataframe으로 변환
  mydataframe <- data.frame(dataframeMat1)
  # 벡터를 여러 개 만들어서 dataframe을 작성
  eng <- c(100,99,90)
  math <- c(100,99,100)
  mydf1 <- data.frame(eng, math)
  # dataframe을 직접 정의
  mydf2 <- data.frame(eng=c(100,100,100),m=c(90,90,90))
  ```

* matrix

  > matrix(1:15)

  ```R
  # 열 3개인 행렬을 만듬
  mymat1 <- matrix(1:15, ncol=3)
  # 행 방향으로 데이터 추가 (기본은 열 방향)
  mymat1 <- matrix(1:15,ncol=3,byrow = T)
  # 행 열
  mymat1[2,2]
  # 1행의 1,2,3 열의 데이터 출력
  mymat1[1,c(1:3)]
  # 1행의 모든 열
  mymat1[1,]
  # 1열의 모든 행
  mymat1[,1]
  # 행과 열의 이름 수정
  rownames(mymat1) <- c("r1","r2","r3","r4","r5")
  colnames(mymat1) <-  c("a", "b", "c")
  ```

* data.table

  > data.frame보다 강력
  >
  > 기본으로 제공되는 게 아니라 다운받아서 사용

  * fread

    : data.table 라이브러리에서 지원되는 function으로 데이터를 읽는 기능

### 데이터 가져오기

* 외부파일
* 트롤링
* DB(오라클,mongodb,hadoop,...)

> R에서 사용할 수 있는 여러 형태의 데이터로 변환
>
> 변환된 데이터를 액세스

### 데이터의 정보를 확인

>컬럼갯수, row갯수, 타입, 유형, 실제 저장된 데이터....

* head() : 위에서 n 줄 읽기, default는 6줄

  > head(exam, n = 5)

* tail() : 뒤에서 n줄 읽기, default는 6줄

## 패키지

> 다양한 함수를 포함하고 있는 라이브러리
>
> install.packages("패키지명")

* ggplot2

  : 다양한 그래프를 그릴 수 있는 패키지

  ```R
  #		읽을 데이터  , x축   , y축    ,  그래프의 모양
  qplot(data = mpg, x= drv, y = hwy, geom = "line")
  ```