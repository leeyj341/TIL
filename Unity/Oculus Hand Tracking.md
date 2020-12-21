# Oculus Hand Tracking

> Oculus VR 장비를 이용하지만 컨트롤러가 아닌 손을 사용해 사용자의 인터랙션을 유도한다.

## OVRHandPrefab

> 오른손 왼손 구분없이 이 prefab을 각 손에 해당하는 Anchor에 넣어 사용한다.

### OVR Skeleton

> 기본 뼈 구조, 뼈 계층, 캡슐 콜라이더 데이터를 포함하는 스크립트
>
> SkeletonType 리스트에서 내가 얻고자 하는 데이터를 선택할 수 있다.

## Add Interactions

```c#
var hand = GetComponent<OVRHand>();
bool isIndexFingerPinching = hand.GetFingerIsPinching(HandFinger.Index);
float ringFingerPinchStrength = hand.GetFingerPinchStrength(HandFinger.Ring);
```

* `isIndexFingerPinching`이 `true`면 현재 Pinching이 진행중이라는 것을 알 수 있다

* `ringFingerPinchStrength`는 현재 얼마나 강한 강도로 Pinching 중인지에 대한 데이터

> 따라서 이 정보를 받아 어떤 상호작용을 만들 것인지 구현할 수 있다

```c#
var hand = GetComponent<OVRHand>();
TrackingConfidence confidence = hand.GetFingerConfidence(HandFinger.Index);
```

* Strength에 더해서 단순 수치가 아니라 단계로 Pinch 정도를 얻어올 수 있음

