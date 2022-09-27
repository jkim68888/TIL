# ARC (Automatic Reference Counting)

<div align="right">2022.09.27</div>

## ARC란?

### ARC는 현재 스위프트에서 사용하고 있는 메모리 관리 모델이며, 컴파일 시점에 메모리 관리 메소드를 자동으로 삽입해주고, 객체에 대한 참조 카운트가 0이 되면 자동으로 메모리를 해제한다.

<br/>

## MRC

> MRC는 ARC 이전에 나온 메모리 관리 모델이다. Objective-C 에서 사용했으며, Manual Reference Counting이라는 뜻으로, retain과 release와 같은 메모리 관리 메소드를 개발자가 직접 수동으로 삽입해줘야했다.

<br/>

## 코드 예시

```Swift
Class Point {
  var x, y: Double
  func Draw() {
    print("Draw something")
  }
}

let point1 = Point(x: 0, y: 0) // rf : +1
let point2 = point1
// retain(point2)              // rf : +1

point2.x = 5
// release(point2)             // rf : -1
// release(point1)             // rf : -1

// 누적 rf가 0이므로,
// point1과 point2가 가르키고 있는 Point객체는 메모리에서 해제된다.
```
