# 객체지향 프로그래밍 (Object Oriented Programming)

<div align="right">2022.09.14</div>

## OOP의 개념

> OOP는 객체의 관점에서 프로그래밍 하는 것을 의미한다. 반대되는 개념으로 C언어는 절차지향 프로그래밍인데, 절차지향 프로그래밍의 프로세스는 함수 단위로 순서대로 진행된다. 객체지향 프로그래밍은 객체들의 유기적인 관계를 통해서 프로세스가 진행된다. [코드](#예시-코드)로 예를 들자면, 동물에 관한 정보와 메서드를 담은 클래스를 하나 정의한다. 그후 정의된 클래스로 동물 객체를 생성하여 메모리에 할당한다. 이렇게 생성된 객체의 속성과 메서드에 접근하여 프로그래밍을 한다.

<br/>

### 스위프트 예시코드

```Swift
class Animal {
    var name = "동물"
    var weight = 0

    func sit() {
        print("\(name)가 앉았습니다.")
    }

    func layDown() {
        print("\(name)가 누웠습니다.")
    }
}

var dog = Animal()

dog.name = "강아지"
dog.weight = 8

print(dog.name)     // "강아지"
print(dog.weight)   // "8"
dog.sit()           // "강아지가 앉았습니다."
dog.layDown()       // "강아지가 누웠습니다."
```

객체지향을 사용하는 언어들

- Java, Python, C++, Swift, Ruby 등

<br/>

## OOP의 4대 특징

### 1. 추상화 Abstraction

- 추상화는 객체들의 `공통된 특징`을 파악해 클래스로 정의하는 설계 기법이다.
  <br/>
- [코드](#예시-코드)로 예를 들자면, 강아지, 고양이, 호랑이 등등 우리가 생각하는 `여러 종류`의 동물이 있다. _이것을 다 클래스화하고 변수와 메서드 등을 개별적으로 만드는 것이 아니라!_ `필수적`으로 필요한 `속성`들과 `메서드`들만 추려서 클래스로 정의하는게 바로 `추상화`이다. 예를들어, 동물 이름, 몸무게, 잠자기, 눕기 만 클래스에 정의해놓는것이다.

<br/>

### 2. 캡슐화 Encapsulation

- 캡슐화는 객체에 대해 `연관`이 있는 `속성`과 `메서드`를 `하나의 클래스`로 묶는 것을 의미한다.
  <br/>
- 캡슐화를 하면, 접근제어자(private, public 등)를 사용하여 객체 외부에서 내부 데이터의 `접근 통제`가 가능해진다. 이게 바로 `은닉화` 개념이다.

- 스위프트 예시코드

  ```Swift
  class Person {
      private var name = "이름" // 속성을 은닉

      func nameChange(name: String) {
          self.name = name
      }
  }

  var person = Person()
  person.nameChange(name: "홍길동")
  // print(person.name) -> 에러 (접근불가)
  ```

  <br/>

### 3. 상속성 Inheritance

- 상속성은 부모클래스의 속성과 메서드를 자식클래스에 그대로 물려받는 개념이다.
  <br/>
- 상속을 통해 코드가 재활용이 되어 생산성이 높아진다.

- 스위프트 예시코드

  ```Swift
  class Person {
    var id = 0
    var name = "이름"
    var email = "abc@gmail.com"
  }

  class Student: Person {
      // id
      // name
      // email
      var studentId = 0
  }

  class Undergraduate: Student {
      // id
      // name
      // email
      // studentId
      var major = "전공"
  }
  ```

  <br/>

### 4. 다형성 Polymorphism

- 다형성은 하나의 객체가 여러가지 타입의 형태로 저장될 수 있다는 개념이다.
  <br/>
- 오버라이딩(Overriding)과 오버로딩(Overloading)을 통해 하나의 메서드나 클래스를 다양한 방법으로 동작시키는 것 또한 포함하는 개념이다.

- 스위프트 예시코드

  ```Swift
  class Aclass {
    func doSomething() {
        print("Do something")
    }
  }

  class Bclass: Aclass {
    override func doSomething() { // 메서드 재정의
        print("Do another job")
    }
  }
  ```
