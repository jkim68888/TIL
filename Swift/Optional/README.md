# Optional (옵셔널)

<div align="right">2022.09.05</div>

### 옵셔널의 개념

> nil이 포함되어 있는 타입을 옵셔널 타입이라 하며, 원래는 변수 선언시 nil값을 허용하지 않으나 옵셔널은 nil값을 허용한다.

- 옵셔널 변수 선언

  ```swift
  var optionalInt: Int?
  ```

  > 변수를 초기화 하지 않으면 nil값이 기본으로 설정된다.

<br/>

### Unwrapping (옵셔널 타입 추출)

> 옵셔널 변수를 unwrapping 하지 않고서는 값을 사용할 수 없다.

<br/>

1. Forced Unwrapping (강제 추출)

```swift
var num: Int?

num!
```

> nil값이 아니라는 확신이 있을때만 사용해야 한다. (nil인 경우에는 에러가 나기 때문)

<br/>

2. 옵셔널 바인딩 (if let 바인딩, guard let 바인딩)

```swift
// if let 바인딩

var num: Int?

if let newNum = num {
  print(newNum)
}
```

```swift
// guard let 바인딩

var num: Int?

guard let newNum = num else { return }
print(newNum)
```

> 바인딩, 즉 새로운 변수에 대입이 되는 경우에만 코드를 진행하겠다는 의미다.

> if let은 해당 if문 안에서만 변수를 사용할 수 있으나, guard문은 if문과 같은 스코프 제약이 없기 때문에 더 편리하다.

<br/>

3. Nil-Coalescing (닐 코얼레싱)

```swift
var num: Int?

num ?? 0
```

> nil인 경우에 기본값을 제시한다.
