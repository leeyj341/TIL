# UIManager

> 유니티에서 UI 사용이 불편하기 때문에 UI의 생성과 삭제, 열고 닫기가 편리하도록 매니저 클래스를 두어 정리한다.

## ISSUE 1

* `LoadUI`를 어떻게 처리할 것인가?

  > UIContentBase를 상속받는 대부분 UI들은 `LoadUI`를 통해 세부 UI를 호출하도록 작성되어 있다. 하지만 모든 UI가 사용하고 있는 것이 아니기에 통일성에 어긋나고 많은 UI가 작성되었을 때 작성여부를 혼동할 수 있다.

* 해결방안

  * `LoadUI`를 Base 단에 정의하여 Base단에서 호출 시 Exception을 발생시켜 개발자에게 인지시켜준다.

    ```c#
    public void ShowUI()
    {
        // 하위 클래스에서 정의되어 있다면 Error를 호출하지 않는다.
    	LoadUI();    
    }
    
    public virtual void LoadUI()
    {
        // 상위 클래스에 정의된 에러 하위에선 실제 구현 내용을 적는다.
        Debug.LogError("LoadUI를 사용하지 않았습니다!!");
    }
    ```

  * 이렇게 되면 현재 `UIManager`에서 `Initialize`하는 부분에 `LoadUI`를 넣는 것이 더 좋은 방법인 듯 하다. `LoadUI`는 처음 생성될 때만 호출하면 되기에 `ShowUI`를 할 때마다 재호출할 필요가 없기 때문이다.

    ```c#
    ShowUI() -> Initialize()
    ```

## ISSUE 2

* `Refresh`가 필요한 UI와 아닌 UI의 기능 구분?

  > `Refresh`를 호출하지 않는 UI더라도 공통구조를 위해 상위 클래스에 정의할 필요가 있다. 이때는 `LoadUI`와 달리 따로 `Exception`을 호출하지 않는다. 
  >
  > 하지만 이런 구조라면 `Refresh`를 호출하는 타이밍은 언제가 좋을까?

* 해결 방안

  * `ShowUI`로 UI를 켤 때마다 호출해준다.

    > 이 방법은 이전 데이터를 유지해야 할 때 유지가 불가능하다.

  * `ShowUI`시 매개변수로 새로고침이 필요한지 아닌지를 받아 `Refresh`여부를 결정한다.

    ```c#
    public virtual void ShowUI(bool isRefreshed)
    {
        // Refresh가 필요한 경우에만 Refresh를 호출한다.
     	if (isRefreshed)
            Refresh();
    }
    ```

    > 이렇게 구현하면 ShowUI를 호출하는 부분이 어디가 될지에 대한 문제가 또 생기기 때문에 이것도 좋은 방법이 아니다.

    

