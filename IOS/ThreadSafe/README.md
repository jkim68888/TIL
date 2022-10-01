# Thread Safe (쓰레드 세이프)

<div align="right">2022.10.01</div>

## Thread Safe하지 않다!

> 멀티쓰레드 환경에서 여러 쓰레드에서 같은 시점에 하나의 메모리에 있는 데이터에 동시접근할때 발생하는 문제이며, 이런 문제를 Thread Safe하지 않다고 표현한다.

<br/>
Thread Safe 하지 않은 경우!

![Frame](https://user-images.githubusercontent.com/75922558/193414457-c8d47aa6-0884-4a2d-a5b2-7ca2bd893f05.png)

## 해결 방법 (Thread Safe하게 만들기!)

### 1. lock

> 메모리에 쓰고 있는 동안에는 여러 쓰레드에서 접근하지 못하도록 lock을 걸어서 막는 방법이다.

```Swift
// 참고 : https://ios-development.tistory.com/955

class ViewController: UIViewController {
  var value = 10000
  let lock = NSLock() // lock 객체 생성

  override func viewDidLoad() {
    super.viewDidLoad()

    DispatchQueue.global().async {
      self.subtractionTen()
    }

    DispatchQueue.global().async {
      self.subtractionTen()
    }
  }

  func subtractionTen() {
    self.lock.lock() // lock 사용
    defer { self.lock.unlock() }

    self.value -= 10
    print(self.value)
  }
}

/*
9990
9980
*/
```

<br/>

### 2. 직렬큐로 보내기

> 여러 쓰레드에서 동시큐로 일이 진행되고 있기 때문에 발생하는 현상이므로, 직렬큐를 커스텀으로 만들어서 Thread Safe 하지 않은 일들을 직렬큐로 보내 동시에 일을 하지 못하도록 한다.

```Swift
var array = [String]()

// 직렬큐 생성
let serialQueue = DispatchQueue(label: "serial")

for i in 1...10 {
  DispatchQueue.global().async {
    print("\(i)")
    // array.append("\(i)") // <- 동시다발적으로 메모리에 접근하여, i가 순서대로 출력이 안된다.

    // 직렬큐에서 실행해야 올바른 처리이다!
    serialQueue.async {
      array.append("\(i)")
    }
  }
}
```

<br/>

## DeadLock

> 멀티쓰레드 환경에서 여러 쓰레드가 서로 메모리를 잠그고 사용하려 해서 메서드의 작업이 종료가 안되서 앱이 멈춰버리는 현상이다.
