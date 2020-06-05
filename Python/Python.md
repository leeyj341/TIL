# Python

## 저장

* `int`? `string`? `boolean`?

  ```python
  number = 10
  string = "10"
  boolean = True
  ```

* `arr`

  > 배열, 파이썬에서는 리스트라고 부름
  >
  > `[]`로 감싸준다.

  ```python
  arr = [number, string, boolean]
  arr2 = [10, "10", True, number]
  print(arr2)
  ```

* `dictionary`

  > 자바에서 `map`과 같은 자료구조
  >
  > `{}`로 감싸준다.

  ```python
  mask = {
      "삼성" : 100.
      "역삼" : 50,
      "선릉" : 30,
      "영등포" : 10
  }
  ```

  입력한 순서대로 저장은 되지만(**순서 보장**) 인덱스로 접근할 수 없다.

  ```python
  print(mask["삼성"])
  ```

## 조건

### 내장함수

* `input()`

  > 입력을 받을 수 있는 함수
  >
  > 자바에서 `scanner`와 같다

  ```python
  number = input()
  print(number + 3)
  ```

  하면 

  ```python
  Traceback (most recent call last):
    File "intro_if.py", line 4, in <module>
      print(number + 3)
  TypeError: can only concatenate str (not "int") to str
  ```

  이런 에러가 발생한다.

  ```python
  number = int(input())
  print(number + 3)
  ```

  이렇게 실행해야 함

### 조건문

* `if`

  > python에서 `if`문은 들여쓰기로 **안**의 내용인지 **밖**의 내용인지 판단

  ```python
  if number > 3 :
      print("3초과")
  print("나는 if문 밖")
  ```

  * 여러 조건

    ```python
    if number > 10:
        print("10초과")
        # 그게 아니라, number가 10 이하, 5초과 일때는 ?
    elif 10 >= number > 5 :
        print("애매")
    else
        print("5이하")
    ```

## 반복

### 내장함수

* `enumerate()`

  >enumerate는 “열거하다”라는 뜻이다. 이 함수는 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 리턴한다.

  ```python
  for idx, i in enumerate(number) :
      print(idx, i)
      
  # 결과는 
  # 0 삼성
  # 1 역삼
  # 2 선릉
  # 3 영등포
  ```

  * `dictionary`

    ```python
    for idx, i in enumerate(mask, 3) :
        print(idx, i)
        
    # 3 삼성
    # 4 역삼
    # 5 선릉
    ```

    >`dictionary`는 인덱스가 없기 때문에 여기서 출력되는 인덱스는 for문이 출려되는 순서이다. `enumerate()`의 매개변수로 `dictionary`와 임의의 숫자를넣어주면 그 숫자부터 인덱스가 출력된다.

### 반복문

* `while`

  ```python
  n = 0
  while(n < 3) :
      n += 1
      print(n)
  print(n)
  ```

* `for`

  * `range()`

    ```python
    number = list(range(3, 10, 2)) # 3부터 9까지 2씩 건너뛰면서
    print(number)
    ```

    range를 이용해 for문을 작성할 수 있다.

  ```python
  number = ["삼성", "역삼", "선릉", "영등포"]
  for i in range(len(number)) :
      print(i)
      print(number[i])
  ```

  * `dictionary`의 `for`문

  ```python
  for i in mask.keys() :
      print(i)
  
  for val in mask.values() :
      print(val)
  
  for key, val in mask.items() :
      print(key, val)
      print(mask[key])
  ```

## 외장 함수

> `import`를 통해 불러와야 사용가능한 함수

```python
import random 
print(dir(random))
```

`dir()`을 통해 어떤 메서드를 사용할 수 있는지 확인 가능

* `random`

  ```python
  number = random.choice(range(10))
  print(number)
  ```

  * `list`와 `dict`에서 사용

    ```python
    # list에서 무작위로 뽑아보자.
    arr = [100, 50, 30, 20]
    arr = ["100", "50", "30", "20"]
    pick = random.choice(arr)
    print(pick)
    
    # dict에도 써보자
    mask = {
        "100" : "삼성",
        "50" : "역삼",
        "30" : "선릉",
        "20" : "영등포"
    }
    print(mask[pick])
    ```

  * `sample()`

    > 범위를 주고 그중에서 임의의 몇개를 선택할 때

    ```python
    lotto = random.sample(range(1,46), 6)
    print(sorted(lotto)) # sorted는 정렬
    ```

## 함수

> `def`로 정의해 사용한다.

```python
def add(num, number) :
    return num + number

nums = add(3, 4)
print(nums)

# default값을 설정할 수 있다
def ran(num, number = 10) :
    return num + number

nums = ran(3)
print(nums)

def m_num(a, b) :
    return a - b
a = 3
b = 4

minus = m_num(b, a)
print(minus) # 결과는 1
```

* 모듈화된 함수 사용

  ```python
  from lt import lottos # 내가 만든 모듈 함수
  
  pick = lottos.lotto(1000) 
  print(pick)
  
  # 1. 만약 4등 한 적이 있으면
  # 2. 4등 "몇 번" 했습니다.
  result = pick["4th"]
  if result > 0 :
      print(f"4등 {result} 번 했습니다.")
  ```

  

  