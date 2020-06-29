# JavaScript 기본

## 변수 선언

* 기존의 방식

  ```javascript
  var varNum = 3
  var varNum = 4
  varNum = 15
  console.log(varNum)
  // 어떤 오류도 없이 정상 작동하고 제일 마지막으로 할당된 15가 출력됨
  ```

* ES6

  * let

    ```javascript
    let letNum = 3
    let letNum = 10
    // 컴파일 오류가 발생한다
    letNum = 10
    // 선언 후 재할당은 가능하다
    ```

  * const

    ```javascript
    const constNum = 3
    constNum = 10
    // 동일한 이름의 선언은 물론 재할당도 불가능하다.
    ```

    보통 `const`를 사용할 경우 대문자로 변수를 정의하는게 컨벤션이다.

## 호이스팅

* var

  ```javascript
  console.log(name)
  var name = '홍길동'.
  // 호이스팅이 발생해 var 선언부가 위로 올라가서 아무 문제없이 실행이 된다.
  ```

* let

  ```javascript
  console.log(name)
  let name = '홍길동'
  // 호이스팅이 발생하지만 let의 경우 선언 전에 사용했다는 오류를 발생시킨다.
  ```

## Arrow Function

```javascript
const arrow = (name) => {
    return console.log(name)
}
// 실행하는 내용이 한 줄이면 return & 중괄호 지우기 가능
const arrow = name => name
// 넘겨주는 인자가 없을 경우
const noArgs = () => 'noArgs'
// key와 value로 이루어진 값을 리턴받고 싶은 경우
const returnObject = () => ({key:'value'})
```

* Arrow Function을 사용한 forEach

  ```javascript
  const colors = ['red']
  colors.forEach(color => console.log(color))
  ```

* 변수로 사용하는 함수

  ```javascript
  const greeting = function() {
      console.log(this)
  }
  greeting()
  // greeting이 출력하는 this는 최상위 window 객체가 된다.
  
  const you = {
      name: 'kim',
      greeting
  }
  you.greeting()
  // greeting이 you 객체를 this로 출력한다.
  // {name: "kim", greeting: ƒ}
  ```

  

  

