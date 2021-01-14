# Extension Method

> 유니티에 기본 제공되는 `Toggle`, `Transform` 등에서 쉽게 내용을 변경하기 어려운 부분을 확장 메서드로 구현할 수 있다.

```c#
namespace Extensions
{
    public static class ExtensionMethod
    {
        // 메서드 구현
    }
}
```

* 예

  * `Poisition`의 `x`값만 변경

    ```c#
    public static void ChangePosX(this Transform trs, float newX)
    {
        trs.position = new Vector3(newX, trs.position.y, trs.position.z);
    }
    ```

## Button에 OnPointerDown 기능 추가하기?

> 유니티 `Button`에서는 OnClick이라는 이벤트를 제공해 클릭이 발생하면 해당 이벤트에 원하는 메서드를 연결시켜 실행되게 할 수 있다.
>
> 하지만 클릭이외에 `PointerDown`이나 `PointerUp`은 처리가 어렵기 때문에 다른 방식으로 해당 이벤트를 처리해 줄 필요가 있다.

* `EventTrigger`를 활용한 이벤트 추가

  ```c#
  public static void AddListener(this Button button, UnityAction action, ButtonEventType type = ButtonEventType.PointerDown)
  {
      EventTrigger trigger = button.gameObject.AddComponent<EventTrigger>();
  
      EventTrigger.Entry entry = new EventTrigger.Entry();
  
      switch (type)
      {
          case ButtonEventType.PointerDown:
              entry.eventID = EventTriggerType.PointerDown;
              break;
          case ButtonEventType.PointerClick:
              entry.eventID = EventTriggerType.PointerClick;
              break;
      }
      
      button.onClick.RemoveAllListeners();
      entry.callback.AddListener((data) => action.Invoke());
      trigger.triggers.Add(entry);
  }
  ```

  이렇게 `PointerDown`이 필요한 `Button`에 Extension Method를 추가하여 작업할 수 있다.

  하지만 이 방법은 버튼 자체가 기능을 가지는 것이 아니기 때문에 다른 더 좋은 방법이 필요하다.

* 커스터마이징 `Button` 구현

  > 유니티에서는 기존 `Component`를 상속하여 새로운 `Component`를 구현할 수 있게 제공되어있다. 이것을 이용해서 Click Event가 PointerDown을 통해 발생하도록 수정할 수 있다.

