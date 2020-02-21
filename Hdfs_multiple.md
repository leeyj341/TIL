# Hdfs 

## MultipleOutputs

> 한 개의 입력데이터를 이용해서 여러 개의 output을 만들고 싶은 경우 사용

### Mapper

> GenericOptionParser작업할 때와 동일하게 map메서드를 구성하며 보통 구분할 수 있도록 key에 각 상황별로 문자열만 추가

### Reducer

> Mapper에서 넘겨준 데이터에서 구분자를 기준으로 분리해서 합산 - 개별 output이 생성될 수 있도록 처리

* `setup`메서드

  : Resucer 객체가 처음 실행될 때 한 번 호출되는 메서드

    MultipleOutputs 객체를 생성

* `reduce`

  : 각각의 상황별로 write가 호출될 수 있도록 처리

    (up, equal, down)

* `cleanUp`

  : Reducer의 작업이 종료될 때 한 번 호출되는 메서드

    MultipleOutputs객체를 해제 (**반드시 처리**해야 함)

### Driver

> MultipleOutputs로 출력될 경로를 Path에 설정
>
> prefix로 구분문자열을 정의

