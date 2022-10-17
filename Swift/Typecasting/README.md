# Typecasting (타입캐스팅)

<div align="right">2022.10.17</div>

## 타입캐스팅이란?

> 타입 캐스팅은 인스턴스의 타입을 확인 하거나, 해당 인스턴스를 슈퍼 클래스나 하위 클래스로 취급하는 방법이다.
> <br/>
> Swift에 형 변환은 is와 as 연산자로 구현되며, is연산자는 값의 타입을 확인하고 as연산자는 값 변환을 하는 연산자이다.
> <br/>
> 타입캐스팅을 사용하면, 해당 타입이 맞는지 프로토콜에 적합한지 확인할 수 있다.

<br/>

## 타입캐스팅을 위한 클래스 계층구조 선언

```Swift
// 부모클래스
class Person {
    var id = 0
    var name = "이름"
    var email = "abc@gmail.com"
}

// 하위 클래스
class Student: Person {
    var studentId = 1
}

// 하위 클래스
class Undergraduate: Student {
    var major = "전공"
}

let person1 = Person()
let student1 = Student()
let undergraduate1 = Undergraduate()
```

<br/>

## 형 확인 (Checking Type)

> is 연산자 - 타입에 대한 검사를 수행

```Swift
// 사람 인스턴스는 학생/대학생 타입은 아니다. (사람 타입이다.)
person1 is Person                // true
person1 is Student               // false
person1 is Undergraduate         // false


// 학생 인스턴스는 대학생 타입은 아니다.  (사람/학생 타입니다.)
student1 is Person               // true
student1 is Student              // true
student1 is Undergraduate        // false


// 대학생 인스턴스는 사람이거나, 학생이거나, 대학생 타입 모두에 해당한다.
undergraduate1 is Person         // true
undergraduate1 is Student        // true
undergraduate1 is Undergraduate  // true
```

### 예제

```Swift
let people = [
    Person(),
    Person(),
    Student(),
    Undergraduate(),
    Student()
]

var studentCount = 0
var undergraduateCount = 0

for i in people {
    if i is Student {
        studentCount += 1
    } else if i is Undergraduate {
        undergraduateCount += 1
    }
}

print("People contains \(studentCount) students and \(undergraduateCount) undergraduates")
// "People contains 2 students and 1 undergraduates"
```

<br/>

## 다운캐스팅 (Downcasting)

> as? / as! 연산자 - 상위클래스의 인스턴스를 하위클래스 타입으로 취급하며, 실패가능성이 있다.
> <br/>
>
> ▶︎ as? 연산자
>
> - 참이면 반환타입은 Optional타입
> - 실패시 nil 반환
>
> ▶︎ as! 연산자
>
> - 참이면 반화타입은 Optional타입의 값을 강제 언래핑한 타입
> - 실패시 런타임 오류

```Swift
// Person 타입인 person 인스턴스의 접근 범위를
// Undergraudate 타입으로 늘려주는 것이다.
if let newPerson = person1 as? Undergraduate {
  print(newPerson.major)
}
```

> ⭐️ 캐스팅은 실제 인스턴스나 값을 바꾸는 것이 아니라 지정한 타입으로 취급하는 것이다.

<br/>

## 업캐스팅 (Upcasting)

> as 연산자 - 하위클래스의 인스턴스를 상위클래스 타입으로 취급하며, 실패가능성이 없다.

```Swift
let student = student1 as Person
print(student.name)
```

<br/>

## 브릿징 (Bridging)

> 서로 호환되는 형식을 캐스팅해서 쉽게 사용하는 것이다. 이때는, as연산자를 사용하면 된다.

```Swift
let str: String = "Hello"
let str2 = str as NSString
```
