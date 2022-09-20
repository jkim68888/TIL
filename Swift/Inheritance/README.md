# Inheritance (상속)

<div align="right">2022.09.20</div>

## 상속의 의미

> 본질적으로 성격이 비슷한 타입을 새로만들어, 데이터(저장속성)를 추가하거나 기능(메서드)를 변형시키서 사용하는 것이다.

<br/>

## 문법

```Swift
class AClass {
    var name = "이름"
}

class BClass: AClass {
    var id = 0
}
```

> BClass는 AClass를 상속한 것이다.
> <br/>
> 따라서, BClass는 AClass의 `name`이라는 저장속성도 갖고 있다.

<br/>

## Final 키워드

```Swift
final class Human {
    var name: String?
    var age: Int?
}
```

> 클래스의 상속을 `금지`하는 키워드이다.

<br/>

> 스위프트에서는 `다중상속`이 되지 않는다!
