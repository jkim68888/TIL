# Class와 Struct (클래스와 구조체)

<div align="right">2022.09.09</div>

## 클래스와 구조체의 개념

클래스와 구조체는 프로그램의 코드를 조직화 하기 위해 사용하는 커스텀 타입이다.

> Swift의 Type에는 기본타입인 `Basic Type`과 사용자 정의 타입인 `Custom Type`이 있다. Custom Type에는 `Enum`, `Class`, `Struct`가 있다.

## Class

```Swift
// 클래스형으로 Dog타입 생성
class Dog {
    var name = "강아지"
    var weight = 8

    func sit() {
        print("앉았습니다.")
    }
}

// 클래스 인스턴스 생성
var bori = Dog()
```

## Struct

```Swift
// struct형으로 Dog타입 생성
struct Dog {
    var name = "강아지"
    var weight = 8

    func sit() {
        print("앉았습니다.")
    }
}

// 스트럭트 인스턴스 생성
var bori = Dog()
```

## Class와 Struct의 차이점

> 가장 큰 차이점은 메모리 저장 방식이다.
> <br/>
> Struct는 값 자체를 스택 영역에 저장하지만, Class는 변수는 스택에 저장하나 데이터 값는 힙에 저장하여 메모리 주소값이 힙을 가르킨다.

```Swift
// 클래스 값 복사
class Person {
    var name = "사람"
}

var p = Person()
var p2 = p

p.name = "혜리"

print(p.name) //"해리"
print(p2.name) //"해리"⭐️
```

```Swift
// 구조체 값 복사
struct Person {
    var name = "사람"
}

var p = Person()
var p2 = p

p.name = "혜리"

print(p.name) //"해리"
print(p2.name) //"사람"⭐️
```

> 따라서 값 복사시, Struct는 다른 메모리 공간에 `값이 복사`되어 저장되지만, Class는 값이 복사되어 저장되는 것이 아니라 `메모리 주소를 전달`하여 저장한다.

| 구분             | Struct(구조체)                                | Class(클래스)                                      |
| ---------------- | --------------------------------------------- | -------------------------------------------------- |
| 타입             | Value Type(값 형식)                           | Reference Type(참조 형식)                          |
| 메모리 저장 방식 | Stack에 값을 저장하여 복사할때 전달           | Heap에 값을 저장하여 복사시 메모리 주소를 전달     |
| let/var 선언     | let으로 선언시 저장 속성이 전부 상수로 선언됨 | let으로 선언해도 저장 속성은 let/var 선언에 따른다 |
| 생성자 관련      | initialize 제공                               | 편의 생성자 존재                                   |
| 메서드 + 속성    | 메서드 내에서 속성 변경 불가능                | 메서드 내에서 속성 변경 가능                       |
| 소멸자           | 소멸자 없음                                   | 소멸자 있음                                        |
| 상속가능여부     | 상속 불가능                                   | 상속 가능                                          |
