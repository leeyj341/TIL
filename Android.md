# Android

## Activity

### ViewGroup

#### Layout

> view를 어떻게 배치할 것인지, 어떤 방식으로 배치할 것인지를 
>
> 디자인 할 수 있는 요소
>
> 중첩 사용도 가능하다

* 공통 속성

  * layout_width : view의 너비

  * layout_height : view의 높이

    * match_parent

      : 부모의 크기(너비, 높이)에 딱 맞게 그리겠다

    * wrap content

      : 자기의 기본 사이즈

  * orientation

    : 배치 방향

      default는 horizontal, vertical로 변경 가능

  * id

    : 각 위젯을 식별할 수 있는 이름

  * margin 

    : 주위 여백

  * padding 

    : 내부 컨텐츠와 border 사이의 간격

  * layout_weight 

    : 여백에 대한 비율

  * layout_gravity

    : parent내부에서 현재 view의 정렬

  * gravity

    : view 내부에서의 정렬

* 종류
  * ConstraintLayout

    : 외부 라이브러리, 제약 조건 기반 모델

     상위 view나 부모를 기준으로 위치를 정하는 layout

  * LinearLayout

    : 박스 모델, 나열하는 형식의 layout
  
    * LayoutParams
  
      : 레이아웃에 줄 수 있는 속성을 정의하는 객체
  
  * RelativeLayout
  
    : 다른 뷰와의 상대적인 위치를 이용해 view의 위치를 결정
  
  * TableLayout
  
    : Linear와 비슷하지만 table로 관리할 수 있어 편리하다
  
    * stretchColumns
  
      : linear의 weight 속성을 주는 것과 비슷한 방식으로
  
      각 요소가 TableRow에서 차지하는 영역을 결정
  
  * FrameLayout
  
    : 여러 장을 띄워놓고 선택에 따라 보여줄 화면을 정할 때 주로 사용
  
    내부 요소에 visibility 속성을 적용해 사용
    
    * visibility
      * gone : 메모리에 올라가지 않고 보이지 않음
      * visible : 메모리에 올라가고 보임
      * invisible : 메미로에 올라가고 보이지 않음
  
* tools

  > 안드로이드의 속성이 아니라 안드로이드 스튜디오에서만 적용되는 속성

#### Text

> 문자열을 디자인 할 수 있는 view 요소
>
> email, password, address, date 등 다양한 요소로 text를 표현할 수 있다

* TextView

  * textAppearance

    : OS가 다 다르기 때문에 폰트의 사이즈를 정하기 어려움

    이 속성으로 모든 기기에 호환되는 텍스트 크기를 선택할 수 있다

* String의 리소스화

  > res의 value 폴더 안 strings에 텍스트를 등록한 후 사용할 수 있다

### Widget

> 실제 화면에 구현되는 view 요소들

* TextView

* Button

* ScrollView

  * 하위는 한 개이어야만 한다.

  * fillViewport속성을 true로 추가

* 기타 등등 ...

### manifests

> 전체 프로젝트의 설정 정보가 저장되어 있는 xml 파일

```java
<intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

시작 activity는 항상 이 요소가 설정되어 있어야 한다.

## Event

> 윈도우의 클릭 이벤트처럼 안드로이드에서도 터치나 키패드 이벤트를 처리할 수 있다.

* OnClickListener

  > 이벤트가 발생하면 즉시 동작할 수 있도록 만들어주는 리스너

  * 인터페이스로 정의되어 있다

    : 다양한 방식으로 이벤트를 처리할 수 있기 때문

  ```java
  public void ActivityClickListener implements 
      								view.OnClickListener {
      @Override
      public void onClick(View v) {
          //클릭이벤트 시 처리할 내용
      }
  }
  ```

  * 익명 이너 클래스

    ```java
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            //처리할 내용
        }
    });
    ```

    ```
    new 인터페이스명() => 지정한 인터페이스의 하위객체를 만들어서
    매개변수로 전달하겠다는 의미
    ```

## Inflator

### LayoutInflator

> view를 생성하는 객체
>
> xml로 생성하지 않고 코드로 생성할 때 사용

## Adapter

> 앱을 구성하는 목록을 만드는 객체

### 사용자 정의 Adapter 만들기

> 안드로이드에서 앱을 구성할 때 목록형식을 가장 많이 사용
>
> 사용자 정의로 디자인한 뷰를 목록으로 사용하고 싶은 경우
>
> 인드로이드 내부에서 제공하는 Adapter로 표현하고 싶은 내용을 모두 표현할 수 없다.(이벤트 연결, 각 목록의 구성을 다르게 생성...)

* 구성요소

  * `Adapter`를 이용해서 출력할 데이터를 저장하는 객체(`DTO` or `VO`)

  * 사용자 정의 `Adapter`

    1. 안드로이드에서 제공하는 `Adapter`클래스를 상속

       > 리스트 뷰를 만들 때 필요한 정보를 저장할 수 있도록 멤버변수 정의
       >
       > Context, row 디자인 리소스, 데이터

    2. 생성자 정의

       > 상속받고 있는 `ArrayAdapter`의 생성자 호출

    3. `ArrayAdapter`에 정의되어 있는 메서드를 오버라이딩

       > `getView` : 리스트 뷰의 한 항목이 만들어질때마다 호출
       >
       > ---
       >
       > ​			  => 전달된 리소스를 이용해서 뷰를 생성(`LayoutInflator`)
       >
       > ​			  => 한 row를 구성하는 뷰를 찾아서 데이터와 연결

    4. `getView`메서드에서 성능개선을 위한 코드를 작성

       > 한 번 생성한 뷰를 재사용
       >
       > `findViewById`는 한 번만 찾아오기

    5. `ViewHolder`객체를 생성

       > row를 구성하는 뷰를 `findViewById`하는 작업을 한 번만
       >
       > row에 대한 구성 View를 멤버변수로 선언
       >
       > 생성자에서  `findViewById`처리를 구현
       >
       > 최초로 뷰를 만들 때(row에 대한 뷰) 이 객체를 생성해서 활용

    6. row를 구성하는 뷰에 상태값을 저장하기

       > 각 뷰의 이벤트를 통해 저장
       >
       > ---
       >
       > 각 뷰의 상태값을 저장할 수 있도록 객체 생성
       >
       > -> 상태값을 저장한 객체를 자료구조에 저장
       >
       > ​	focus를 잃어버릴 때 상태를 저장

  * `Adapter`를 통해 만들어진 리스트뷰를 보여줄 액티비티

    * main layout 필요