# Function (함수)

<div align="right">2022.09.04</div>

### Parameter (파라미터)

> 매개변수/인자 라고도 부르며, 함수의 입력값(input)으로 사용되는 변수이다.

- 가변파라미터

  ```swift
  func getAverage(_ numbers: Int...) -> Int {
      var total = 0

      for n in numbers {
        total += n
      }

      return total / numbers.count
  }

  getAverage(1,2,3,4,5)
  ```

  > 하나의 파라미터로 여러개의 아규먼트를 전달할 수 있다.
  > 단, 가변파라미터는 기본값을 가질 수 없다.

<br/>

### Argument (아규먼트)

> 인수라고도 부르며, 함수의 호출에 사용되는 실제 값이다.

- Argument Label

  ```swift
  func someFunction(writeYourFirstNumber a:Int, writeYourSecondNumber b: Int) {
      print(a + b)
  }

  someFunction(writeYourFirstNumber: 3, writeYourSecondNumber: 4)
  ```

  > 더 명확하게 요구사항을 알 수 있는 장점이 있다.

- 와일드카드 패턴

  ```swift
  func addNum(_ num1:Int, _ num2: Int) {
      print(num1 + num2)
  }

  someFunction(1, 2)
  ```

  > 아규먼트 레이블을 생략할 수 있다.

<br/>

### Scope (스코프)

> 함수 내에서 선언한 변수는 함수 밖에서 접근할 수 없다.
> <br/>
> 단, 외부의 변수를 함수 내에서 접근하는 것은 가능하다.
