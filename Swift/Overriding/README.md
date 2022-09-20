# Overriding (재정의)

<div align="right">2022.09.20</div>

## Overriding의 의미

> 클래스의 상속에서 상위클래스의 속성/메서드를 재정의(기능을 약간 변형하여 사용)하는 것이다.

<br/>

## Overriding이 가능한 대상

- 저장속성을 제외한 속성들 (계산속성...)
- 메서드
- 서브스크립트
- 생성자

> ⭐️ 저장속성은 재정의가 불가능하다.

<br/>

## 문법

```Swift
class SomeSubclass: SomeSuperclass {
    override var aValue: Int {
        get {
            return 1
        }
        set {
            super.aValue = newValue
        }
    }

    override func doSomething() {
        super.doSomething()
        print("Do something 2")
    }
}
```

- `override` 키워드를 앞에 붙여준다.
- `super` 키워드로 부모클래스의 속성 또는 메서드를 호출해준다.

<br/>

## Overloading(오버로딩) 과의 차이점

### Overloading

---

오버로딩은 하나의 함수 이름에 여러 함수를 대응시키는 것이다.
<br/>
즉, 함수 이름은 같지만, 매개변수나 리턴타입 등을 다르게 하여 중복으로 선언할 수 있다.

<br/>

### Overriding

---

오버라이딩은 상속 받은 하위 클래스에서 함수,프로퍼티 등을 재정의 하는 것이다.
