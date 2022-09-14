# 시간 복잡도 (Time Complexity)

<div align="right">2022.09.14</div>

## 시간복잡도의 개념

> 입력값이 주어졌을때, 문제를 해결하는데 걸리는 시간과의 상관관계.

<br/>

## 효율적인 알고리즘과 시간복잡도와의 관계

> 입력값이 늘어났을때, 문제 해결 시간이 얼마나 늘어나는지 판단하여,
> <br/>
> 입력값이 늘어나도 걸리는 시간이 덜 늘어나게끔 최소한의 시간복잡도를 갖는 알고리즘이 효율적이다.

<br/>

## 빅오 표기법

1️⃣ O(1)

```Swift
func solution(array: [Int]) {
  print("hello world")
}
```

> 입력값에 `관계없이` 복잡도가 동일하게 `유지`된다.

<br/>

2️⃣ O(N)

```Swift
// 예시: for문

func solution(array: [Int]) {
  for i in array {
    print(i)
  }
}
```

> for문은 입력값이 증가하면 해당 문제를 처리하는 시간과 메모리 사용이 `입력값의 길이(N)`만큼 증가한다.

<br/>

3️⃣ O(N^2)

```Swift
// 예시: 이중for문

func solution(array: [Int]) {
  for i in array {
    for j in array{
      print(i+j)
    }
  }
}
```

> 이중for문은 for문안에 for문이 있으므로, 입력값이 증가하면 해당 `입력값의 길이를 제곱한 만큼`의 시간이 걸리게 된다.

<br/>

4️⃣ O(n log n)

```Swift
// 예시: sorted함수

func solution(array: [Int]) -> [Int] {
  return array.sorted()
}
```

> sorted함수는 내부적으로 O(n log n)만큼의 시간복잡도가 걸리게끔 설계되어있는 함수이다.

<br/>

## 빅오표기법 비교

![c](https://user-images.githubusercontent.com/75922558/190040589-645b54ad-4f93-4023-8ef4-c3c7681ee9b6.png)
