# Enumerations (열거형)

<div align="right">2022.09.06</div>

## Enum의 정의

> 연관된 상수(케이스)들을 하나의 이름으로 묶은 자료형이다.

```Swift
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
    case saturday
    case sunday
}
```

### Raw Values (원시값)

```Swift
enum Alignment: String {
    case left = "L"
    case center = "C"
    case right = "R"
}

let leftValue = Alignment.left.rawValue //"L"

let align = Alignment(rawValue: "L") //left
```

> 열거형 케이스에 매칭되는 기본값이 원시값이며, 정수 또는 문자열이 될 수 있다.

<br/>

### Associated Values (연관값)

```Swift
enum Computer {
    case cpu(core: Int, ghz: Double)
    case ram(Int, String)
    case hardDisk(gb: Int)
}

let myChip1 = Computer.cpu(core: 8, ghz: 3.5) //cpu(core: 8, ghz: 3.5)
```

> 각 케이스마다 저장할 형식을 따로 정의하는 것이다. 이때, 자료형에는 제한이 없으며 튜플의 형태로 사용한다.
