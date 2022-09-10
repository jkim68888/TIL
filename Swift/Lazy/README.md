# Lazy Stored Properties (지연 저장 속성)

<div align="right">2022.09.10</div>

## 문법

`lazy var`로 선언한다.

```Swift
struct Bird {
    var name: String
    lazy var weight: Double = 0.2 // lazy 속성은 선언시점에 기본값을 저장해야한다. ⭐️

    init(name: String) {
        self.name = name
        // weight은 여기서 초기화 시키지 않는다! ⭐️
    }
}
```

> 중요 포인트 🌟
>
> 1. lazy속성은 var로 선언해야 한다. (let으로는 선언할 수 없다.)
> 2. lazy속성은 initializer에서 초기화하지 않고 선언시점에 기본값을 저장해야 한다는 것이다.

<br/>

## 특징

```Swift
struct Bird {
    var name: String
    lazy var weight: Double = 0.2

    init(name: String) {
        self.name = name
    }
}

var a = Bird(name: "새") // 인스턴스가 생기는 시점에서는 weight이라는 속성은 초기화 되지 않는다.
a.weight // 이 시점에 weight이라는 속성이 초기화된다. (이 시점에 메모리 공간이 생기고 값이 저장된다는 뜻) ⭐️
```

> 일반 저장 속성(let, var)은 인스턴스가 초기화되는 시점에서 값을 갖고 초기화된다.
> <br/>
> 하지만, 지연 저장 속성(lazy var)은 `해당 속성에 접근하는 순간`에 개별적으로 초기화 된다.

<br/>

## Lazy 사용 이유

1. 메모리 낭비를 막기 위함. 즉, 메모리를 효율적으로 관리할 수 있음.
2. 초기화 시점을 다른 속성과 다르게 해야 할 경우가 생긴다. 이럴때, lazy로 선언하여 먼저 초기화된 속성에 접근할 수 있다.
