# Android 구조

## 컴포넌트 기반

* Activity

  > 하나의 액티비티가 하나의 화면이 됨
  >
  > 뷰 하나 당 화면구성 요소 하나
  >
  > AppCompatActivity를 상속받음 
  >
  > 모든 Activity는 onCreate메서드를 구현해야 함

  * `.xml`을 통해 드래그&드랍으로 view를 구현할 수 있다.

  * **LifeCycle**

    * 켤 때

      ```markdown
      onCreate()		* 한 번 호출됨
      	v
      onStart()
      	v
      onResume()
      ```

    * 백그라운드 상태로 나갔을 때 (일시정지 구간)

      ```markdown
      onPause()	 
      	v
      onStop()
      ```

    * 종료할 때

      ```markdown
      onPause()	 
      	v
      onStop()
      	v
      onDestroy()		* 한 번 호출됨
      ```

* Service

  > 오래 실행되는 작업
  >
  > 화면 앞단에서 실행되는 것이 아니라 화면 뒷단(보이지 않는 부분)에서 실행

* ContentProvider

  > 어플리케이션 내에서 사용할 수 있는 데이터를 공유하기 위한 컴포넌트 

* BroadCastReceiver

  > 앱 간에 또는 구성 요소 간에 메시지를 주고받을 수 있게 하는 요소
  >
  > 화면이 없는 상태에서 인텐트 안에 포함된 메시지를 주고받을 때 사용됨

## 리소스의 외부화

> res 폴더에 정적자원을 저장하면 자동으로 generate 되면서
>
> 프로그램에서 사용할 수 있다.
>
> ---
>
> 리소스의 관리가 용이하다 => **유지보수가 쉽다** (R.java)

* 문자열 이미지
* 화면
* 외부파일

## manifests

> 앱에 대한 설명서(명세 파일)라고 생각하면 됨 