# Android API

## 사용 환경 설정

* 사용할 API의 키를 발급받는다.

* Project Structure에서 Google Play services 라이브러리가 설치되어 있는지 확인

* 없다면 settings -> Android SDK에서 SDK Tools 목록을 선택해 해당 라이브러리를 다운

   <img src="C:\Users\student\Desktop\and_api.png" style="zoom:75%;" />

## Fragment

> 맵이 출력될 수 있게 xml 디자인에 추가한다.

```java
<fragment
        android:id="@+id/myMap"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```

요즘 추세는 fragment를 통해 출력하는 거라고 함...

* 권한 등록 및 키 추가

  ```java
  <uses-permission android:name="android.permission.INTERNET"/>
      
  //application 태그 내에 발급받은 API_KEY를 등록
  <meta-data
      android:name="com.google.android.geo.API_KEY"
      android:value="AIzaSyC27yFbGJbB84s2fiWJzdVu75DR_W7fcGk"/>
  ```

