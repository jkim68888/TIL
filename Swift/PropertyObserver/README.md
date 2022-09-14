# Property Observer (속성 감시자)

<div align="right">2022.09.14</div>

## 속성감시자의 정의

> 저장 속성이 변하는 시점을 관찰하는 메서드이다.

<br/>

## 문법

#### willSet / didSet

```Swift
class Profile {
  var name: String = "홍길동"

  var statusMessage: String = "default message" {
    willSet(message) {
      print("메세지가 \(statusMessage)에서 \(message)로 변경될 예정입니다.")
    }
    didSet(message) {
      print("메세지가 \(message)에서 \(statusMessage)로 변경되었습니다.")
    }
  }
}
```

1. willSet: 값이 저장되기 직전에 호출됨
2. didSet: 새로운 값이 저장된 직후에 호출됨

> 주의점 ⭐️
> <br/> > `didSet`은 값이 `저장된 후`에 호출되므로, didSet에서 받은 `파라미터`는 `예전값(oldValue)`가 된다. 변경된 `새로운 값`은 `속성감시자 변수`에 담겨있다.

<br/>

#### oldValue / newValue

> willSet의 파라미터를 생략하면 newValue가 기본 파라미터로 제공되며,
> <br/>
> didSet의 파라미터를 생략하면 oldValue가 기본 파라미터로 제공된다.
