# Grammar

> 파이썬의 문법을 알아보자

## 논리 연산자

* and

  ```python
  print("___and___")
  print(True and True)	# True
  print(True and False)	# False
  print(False and False)	# False
  print(False and True)	# False
  ```

* or

  ```python
  print("___or___")
  print(True or True)		# True
  print(True or False)	# True
  print(False or False)	# False
  print(False or True)	# True
  ```

* not

  ```python
  print("___not___")
  print(not True)			# False
  print(not [])			# True
  ```

* in

  ```python
  print("___in___")
  print("a" in "apple")		# True
  print(1 not in [1, 2, 3])	# False
  ```

* 단축 평가

  ```python
  # ""가 False "Text"가 True이기 때문에 or문이 끝나서 그 다음은 연산하지 않는다.
  print("" or "Text" or "Text_2")
  
  # ""가 False "Text"가 True이기 때문에 and문을 만족하지 못하고 
  # 다음 or문을 검사해 "Text_2"가 출력된다.
  print("Text" and "" or "Text_2")
  ```

## Sequence

* range

  ```python
  sample_list = list(range(31))
  print(sample_list)
  print(sample_list[3])
  print(sample_list[3:24])
  print(sample_list[5:-1])
  print(sample_list[5:])
  ```

  ```python
  # 3부터 sample_list의 길이만큼, 2단계씩 뛰어서 출력하겠다
  print(sample_list[3:len(sample_list):2])
  # 비워두면 끝까지 출력하겠다는 의미
  print(sample_list[:13:2])
  # 뒤에서부터 전체 다 출력
  print(sample_list[::-1])
  ```

## immutable & mutable

* immutable

  ```python
  string = "immutable"				# immutable
  list_a = ["immutable?", "real?"]	# mutable
  
  print(string[0])
  print(list_a[0])
  string[0] = "a" 	# 한 번 정해진 string 값은 변환할 수 없다.(오류)
  list_a[0] = "mutable"
  ```

  ```python
  # immutable
  string_a = "a"
  string_b = string_a
  string_b = "b"
  print(string_a, string_b) 	# a, b
  ```

  같은 것을 바라보게 만들어도 **immutable** 특성을 가진 string은 해당 값만 변환이 된다.

  ```python
  # mutable
  list_a = ["immutable?", "real?"]
  list_b = list_a
  print(list_a, list_b)
  list_b[0] = "mutable"
  print(list_a, list_b)		# 둘의 내용이 같다.
  ```

