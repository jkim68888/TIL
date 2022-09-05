# Collection (컬렉션)

<div align="right">2022.09.05</div>

## 컬렉션 타입의 정의

> 지정된 타입의 데이터들의 묶음이다. Swift에서는 [배열](#array-배열), [딕셔너리](#dictionary-딕셔너리), [집합](#set-집합) 이렇게 세가지 컬렉션 타입이 있다.

<br/>

### Array (배열)

```Swift
var arr = ["Apple", "Banana", "City"]
```

> 같은 데이터 타입의 값들을 순서대로 저장하는 리스트이다. (중복값 저장 가능)

<br/>

### Dictionary (딕셔너리)

```Swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]
```

> 순서없이 키(Key) 와 값(Value) 한 쌍으로 데이터를 저장한다. (중복값 저장 불가능)

<br/>

### Set (집합)

```Swift
var set: Set<String> = ["Apple", "Banana", "City"]
```

> 같은 데이터 타입의 값들을 순서없이 저장하는 리스트이다. (중복값 저장 불가능)
> <br/>
> 반드시 Set이라고 타입을 지정해줘야 한다.

<br/>

## Subscript (서브스크립트 문법)

```Swift
var strArray = ["Apple", "Banana", "City"]

strArray[0]
```

> 대괄호를 이용하며, 배열과 딕셔너리에 접근할 때 사용한다.

<br/>

## Hashable

> 유일한 값!이 가능한 타입이라는 뜻이다.

> Swift 에서는 String, Int 등 기본타입은 모두 Hashable 하다.

- 장점
  - 값의 유일성 보장
  - 빠른 검색 속도

> Dictionary와 Set은 Hashable한 타입으로 되어있다. 따라서 배열보다 검색 속도가 빠르다.
