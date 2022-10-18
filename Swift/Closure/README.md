# Closure (클로저)

<div align="right">2022.10.18</div>

## 클로저란?

> 클로저란 이름이 없는 익명함수이다. 즉, 함수와 기능은 똑같지만 굳이 이름이 없어도 호출할 수 있는 형태로 사용이 가능하다.

<br/>

## 일반 함수와 클로저 비교

### 일반 함수의 형태

```Swift
func myFuction() -> Int {
  return
}
```

### 클로저의 형태

```Swift
{ () -> Int in
  return
}
```

<br/>

## 함수의 특징

- 함수를 [변수에 할당](#변수에-함수-할당)할 수 있다.
- 함수를 [파라미터로 전달](#파라미터로-함수-전달)이 가능하다.
- [함수를 리턴](#함수를-리턴)할 수 있다.

<br/>

> 클로저를 사용하면 위 3가지 특징의 코드를 좀 더 간결하게 작성할 수 있다.

<br/>

## 클로저 문법

### 변수에 함수 할당

```Swift
let closure = { (param: String) -> String in
    return param + "!"
}

closure("스티브")
```

<br/>

### 파라미터로 함수 전달

```Swift
// 클로저를 파라미터로 받는 함수 정의
func closureParamFunction(closure: () -> ()) {
    print("프린트 시작")
    closure()
}

// 함수 실행
closureParamFunction(closure: { () -> () in
    print("프린트 종료")
})
```

<br/>

### 함수를 리턴

```Swift
let hello: (String, String) -> String = { (firstName, lastName) in
	return lastName + firstName
}

func closureReturnFunction(message: String) -> String {
	return hello("지현", "김") + message
}

closureReturnFunction(message: "입니다.")
```

<br/>

## 클로저 문법의 최적화

> 클로저는 쉽고, 간결한 코드 작성을 위해 축약된 형태의 문법을 제공한다.

```Swift
// 함수 정의
func closureFunction(closure: () -> Void) {
    print("프린트 시작")
    closure()
}

// 함수 실행
// 축약되지 않은 형태
closureFunction(closure: {
    print("프린트 종료")
})

// 소괄호를 앞으로 가져오기
closureFunction(closure: ) {
    print("프린트 종료")
}

// 아규먼트 생략
closureFunction() {
    print("프린트 종료")
}

// 소괄호 생략 (후행클로저 trailing closure)
closureFunction {
    print("프린트 종료")
}
```

<br/>

### 클로저의 파라미터 생략

> 첫 번째 파라미터는 $0, 두 번째 파라미터는 $1로 바꿔서 쓸 수 있다.

```Swift
// 함수 정의
func performClosure(param: (String) -> Int) {
    param("Swift")
}

// 함수 실행
performClosure { $0.count } // 파라미터를 $0으로 축약
```

<br/>

## 클로저의 활용

> 배열의 메서드인 map(), reduce(), filter(), sort() 등에서 사용된다.

### map()

```Swift
let arr1 = [1, 3, 6, 2, 7, 9]
let arr2 = arr1.map { $0 * 2 } // [2, 6, 12, 4, 14, 18]
```

<br/>

### reduce()

```Swift
arr1.reduce(0) { $0 + $1 } // 28
```

> Swift에서는 연산자도 함수이다. 함수는 곧 클로저이기 때문에 연산자는 클로저이다. 1 + 2를 실행하면, +라는 이름을 가진 연산자 함수가 실행된다. 파라미터로는 1과 2가 넘겨지게 되므로, + 함수는 파라미터 두 개를 받아서 합을 반환하는 클로저라 할 수 있다. 즉, { $0 + $1 }과 같은 의미이다. 따라서 아래처럼 +라는 연산자를 클로저로 넘기는 것도 가능하다.

```Swift
arr1.reduce(0, +) // 28
```
