# Generic (제네릭)

<div align="right">2022.10.21</div>

## 제네릭이란?

> 제네릭이란 타입에 의존하지 않는 범용 코드를 작성할 때 사용하며, 제네릭을 사용하면 중복을 피하고 코드를 유연하게 작성할 수 있다.
> <br/>
> 제네릭이 없다면, 함수(클래스, 구조체, 열거형 등)타입마다 모든 경우를 다 정의해야 하기 때문에 매우 불편하다.

<br/>

## 제네릭을 사용하지 않는 경우

```Swift
let numbers = [2, 3, 4, 5]
let scores = [3.0, 3.3, 2.4, 4.0, 3.5]
let people = ["Jobs", "Cook", "Musk"]

// 정수를 파라미터로 받는 함수
func printIntArray(array: [Int]) {
    for number in array {
        print(number)
    }
}

// 실수를 파라미터로 받는 함수
func printDoubleArray(array: [Double]) {
    for number in array {
        print(number)
    }
}

// 문자열을 파라미터로 받는 함수
func printStringArray(array: [String]) {
    for number in array {
        print(number)
    }
}

printIntArray(array: numbers)
printDoubleArray(array: scores)
printStringArray(array: people)
```

> 위 3가지 함수는 모두 같은 기능을 한다. 하지만 파라미터의 타입이 다르기 때문에 같은 코드를 실행하는 함수를 3번이나 정의해야한다.
> <br/>
> 이렇게 타입이 다르다는 이유로 여러개의 함수를 만드는 것이 비효율적이라는 것이다.

<br/>

## 제네릭 문법

```Swift
let numbers = [2, 3, 4, 5]
let scores = [3.0, 3.3, 2.4, 4.0, 3.5]
let people = ["Jobs", "Cook", "Musk"]

// 여러 타입을 받아 사용할 수 있는 함수 하나만 정의
func printArray<T>(array: [T]) {
    for element in array {
        print(element)
    }
}

printArray(array: numbers)
printArray(array: scores)
printArray(array: people)
```

> 타입 파라미터<T>는 함수 내부에서 파라미터의 타입이나 리턴형으로 사용된다. (함수 바디에서 사용하는 것도 가능)
>
> (1) 관습적으로 Type(타입)의 의미인 대문자 T를 사용하지만, 다른 문자를 사용해도 된다.
>
> (2) <T, U> <A, B> 이렇게 타입파라미터를 2개이상도 선언 가능하다.

<br/>

## 구조체에서 제네릭 정의하기

```Swift
struct GenericMember<T> {
    var members: [T] = []
}

var member1 = GenericMember(members: ["Jobs", "Cook", "Musk"])
var member2 = GenericMember(members: [1, 2, 3])
```

<br/>

## 클래스에서 제네릭 정의하기

```Swift
class GridPoint<A> {
    var x: A
    var y: A

    init(x: A, y: A){
        self.x = x
        self.y = y
    }
}

let aPoint = GridPoint(x: 10, y: 20)
let bPoint = GridPoint(x: 10.4, y: 20.5)
```

<br/>

## 열거형에서 제네릭 정의하기

```Swift
enum Pet<T> {
    case dog
    case cat
    case etc(T)
}

let animal = Pet.etc("고슴도치")
```

> 열거형에서는 연관값을 가질때 제네릭으로 정의가 가능하다.

<br/>

## 프로토콜에서 제네릭 정의하기

```Swift
protocol RemoteControl {           // <T>의 방식이 아님
    associatedtype T               // 연관형식은 대문자로 시작해야함
    func changeChannel(to: T)      // 관습적으로 Element를 많이 사용
    func alert() -> T?
}

struct TV: RemoteControl {

    typealias T = Int              // 생략 가능

    func changeChannel(to: Int) {
        print("TV 채널바꿈: \(to)")
    }

    func alert() -> Int? {
        return 1
    }

}
```
