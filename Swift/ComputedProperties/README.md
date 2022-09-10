# Computed Properties (계산 속성)

<div align="right">2022.09.10</div>

## 개념

> 속성 형태를 가진 실질적 메서드이며, getter와 setter로 이루어져있다.

<br/>

## 계산 속성 문법

```Swift
class Person {
	var birth: Int = 0

	var age: Int {
		// getter (반드시 구현)
		get {
			return 2021 - birth
		}

		// setter (필요시 구현)
		set(age) {
			self.birth = 2021 - age
		}
	}
}

var p = Person()

p.birth = 2000
p.age // get
p.age = 20 // set
```

> 무조건 var로 선언하고, get블록을 작성해야 한다.

<br/>

## 계산 속성을 사용하지 않고 get과 set 구현하기

```Swift
class Person {
	var birth: Int = 0

  // get method
	func getAge() -> Int {
    return 2021 - birth
  }

  // set method
  func setAge(_ age: Int){
    self.birth = 2021 - age
  }
}

var p = Person()

p.birth = 2000
p.getAge() // get
p.setAge(20) // set
```

> 메서드를 선언하여 구현할 수 있다.

<br/>

## setter가 없는 Computed Properties

```Swift
class Person {
  var birth: Int = 0

  var age: Int {
    return 2021 - birth
  }
}
```

> get 키워드를 생략할 수 있다.

<br/>

## set블록의 기본 파라미터 (newValue)

```Swift
var age: Int {
		get {
			return 2021 - birth
		}

		// 파라미터 이름 설정시
    /* set(age) {
			self.birth = 2021 - age
		} */

    // 기본파라미터 사용시
    set {
      self.birth = 2021 - newValue
    }
}
```

> newValue라는 기본 파라미터를 제공해준다.
