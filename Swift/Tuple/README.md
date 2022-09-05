# Tuple (튜플)

<div align="right">2022.09.04</div>

### 튜플의 정의

> 튜플은 2개 이상의 데이터(값)을 열거하는 자료형이다.

```swift
let threeValues = ("hello", 1, "world")
```

> 튜플의 값은 "추가" / "삭제" 가 불가능하다.

<br/>

### 튜플의 데이터에 접근

```swift
threeValues.0
threeValues.1
threeValues.2
```

<br/>

### Named Tuple

```swift
let twoValues = (num: 1, str: "hello")

twoValues.num
twoValues.str
```

> 인덱스번호로 데이터에 접근할때보다 코드의 가독성이 높아진다.

<br/>

### 튜플의 분해

```swift
let threeNumbers = (1, 2, 3)

let (first, second, third) = threeNumbers

first
second
third
```

> 튜플을 분해하여 변수에 저장할 수 있다.

<br/>

### 튜플의 매칭

```swift
let iOS = (language: "Swift", version: "5")

switch iOS {
  case ("Swift", "5"):
      print("스위프트 버전 5입니다.")
  case ("Swift", "4"):
      print("스위프트 버전 4입니다.")
  default:
      break
}
```

> 스위프트의 switch문은 튜플 매칭을 지원하여, 코드를 간결하게 표현할 수 있다.
