# Strong Reference Cycle (강한 순환 참조)

<div align="right">2022.09.27</div>

## 강한 순환 참조란?

### 두개의 클래스 인스턴스가 서로를 가르키는 경우, 메모리에서 해제될 시점에, 인스턴스의 참조 카운트가 0이 되지 못하여 두개가 계속해서 메모리 상에 존재하게 되는 현상이다.

<br/>

## 코드 예시

```Swift
class CarBrand {
    var brandName: String
    var product: Car? // rf : +1

    init(name: String) {
        self.brandName = name
    }
}


class Car {
    var carName: String
    var brand: CarBrand? // rf : +1

    init(name: String) {
        self.carName = name
    }
}


var kia: CarBrand? = CarBrand(name: "기아") // rf : +1
var k5: Car? = Car(name: "k5") // rf : +1


kia?.product = k5 // rf : -1
k5?.brand = kia // rf : -1

// 누적 rf가 0이 되지 않아,
// kia와 k5 객체의 메모리 해제가 되지 않는다.
```

<br/>

## 해결 방안

1. Weak Reference (약한 참조)
2. Unowned Reference (비소유 참조)

> weak 과 unowned 키워드로 선언한 변수를 통해 인스턴스에 접근은 가능하지만, 서로 가르키는 인스턴스의 레퍼런스 카운트를 올라가지 않게 한다.

<br/>

## Weak과 Unowned의 차이점

### Weak

nil체크가 가능하여, 인스턴스가 nil인 경우 작업을 중단하는 것이 가능하다.

<br/>

### Unowned

인스턴스의 nil확인이 불가능하여, 실제 인스턴스가 해제되었다면 에러가 발생한다.

> 옵셔널로 선언은 가능하지만, nil로 초기화가 되지 않는다! ⭐️
