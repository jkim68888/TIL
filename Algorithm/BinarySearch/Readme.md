# 이진탐색 (Binary Search)

<div align="right">2025.06.04</div>

## 소개

이진탐색은 정렬된 배열에서 특정 값을 찾는 가장 효율적인 알고리즘 중 하나입니다. 매번 탐색 범위를 절반으로 줄여나가는 분할정복 방식을 사용하여 O(log n)의 시간복잡도로 원하는 값을 찾을 수 있습니다.

## 동작 원리

이진탐색의 핵심 아이디어

1. 정렬된 배열의 중간 요소를 확인
2. 찾는 값이 중간 값보다 작으면 왼쪽 절반을 탐색
3. 찾는 값이 중간 값보다 크면 오른쪽 절반을 탐색
4. 값을 찾거나 탐색 범위가 없어질 때까지 반복

이 과정을 통해 매번 탐색해야 할 요소의 수가 절반으로 줄어들어 매우 효율적입니다.

## 기본 구현

### 반복문을 사용한 이진탐색

```javascript
function binarySearch(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        
        if (arr[mid] === target) {
            return mid; // 찾은 인덱스 반환
        } else if (arr[mid] < target) {
            left = mid + 1; // 오른쪽 절반 탐색
        } else {
            right = mid - 1; // 왼쪽 절반 탐색
        }
    }
    
    return -1; // 값을 찾지 못한 경우
}

// 사용 예시
const sortedArray = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
console.log(binarySearch(sortedArray, 7));  // 출력: 3
console.log(binarySearch(sortedArray, 4));  // 출력: -1
```

### 재귀를 사용한 이진탐색

```javascript
function binarySearchRecursive(arr, target, left = 0, right = arr.length - 1) {
    if (left > right) {
        return -1; // 값을 찾지 못한 경우
    }
    
    const mid = Math.floor((left + right) / 2);
    
    if (arr[mid] === target) {
        return mid;
    } else if (arr[mid] < target) {
        return binarySearchRecursive(arr, target, mid + 1, right);
    } else {
        return binarySearchRecursive(arr, target, left, mid - 1);
    }
}

// 사용 예시
const sortedArray = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
console.log(binarySearchRecursive(sortedArray, 11)); // 출력: 5
```

## 응용 패턴

### 1. 첫 번째 또는 마지막 위치 찾기

중복된 값이 있는 배열에서 특정 값의 첫 번째 또는 마지막 위치를 찾는 경우

```javascript
// 첫 번째 위치 찾기
function findFirstPosition(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    let result = -1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        
        if (arr[mid] === target) {
            result = mid;
            right = mid - 1; // 더 왼쪽을 계속 탐색
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}

// 마지막 위치 찾기
function findLastPosition(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    let result = -1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        
        if (arr[mid] === target) {
            result = mid;
            left = mid + 1; // 더 오른쪽을 계속 탐색
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}

// 사용 예시
const duplicateArray = [1, 2, 2, 2, 3, 4, 5];
console.log(findFirstPosition(duplicateArray, 2)); // 출력: 1
console.log(findLastPosition(duplicateArray, 2));  // 출력: 3
```

### 2. 삽입 위치 찾기

정렬된 배열에서 특정 값이 삽입될 위치를 찾는 경우

```javascript
function findInsertPosition(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        
        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return left;
}

// 사용 예시
const sortedArray = [1, 3, 5, 7, 9];
console.log(findInsertPosition(sortedArray, 4)); // 출력: 2 (인덱스 2에 삽입)
console.log(findInsertPosition(sortedArray, 0)); // 출력: 0 (맨 앞에 삽입)
```

### 3. 조건을 만족하는 값 찾기

특정 조건을 만족하는 최소값이나 최대값을 찾는 경우

```javascript
// 제곱근 구하기 (정수 부분만)
function sqrt(x) {
    if (x < 2) return x;
    
    let left = 1;
    let right = Math.floor(x / 2);
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        const square = mid * mid;
        
        if (square === x) {
            return mid;
        } else if (square < x) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return right; // 가장 큰 정수 반환
}

// 사용 예시
console.log(sqrt(8)); // 출력: 2
console.log(sqrt(16)); // 출력: 4
```

## 시간복잡도와 공간복잡도

- **시간복잡도** O(log n)
  - 매번 탐색 범위가 절반으로 줄어들기 때문
  - n개의 요소를 가진 배열에서 최대 log₂n번의 비교만 필요

- **공간복잡도**:
  - 반복문 버전: O(1)
  - 재귀 버전: O(log n) - 재귀 호출 스택 때문

## 주의사항과 최적화 팁

### 1. 오버플로우 방지

중간값 계산 시 오버플로우를 방지

```javascript
// 일반적인 방법 (큰 수에서 오버플로우 가능)
const mid = Math.floor((left + right) / 2);

// 안전한 방법
const mid = left + Math.floor((right - left) / 2);
```

### 2. 경계 조건 처리

```javascript
function binarySearchSafe(arr, target) {
    // 빈 배열 체크
    if (!arr || arr.length === 0) {
        return -1;
    }
    
    let left = 0;
    let right = arr.length - 1;
    
    while (left <= right) {
        const mid = left + Math.floor((right - left) / 2);
        
        if (arr[mid] === target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;
}
```

## 실제 활용 사례

### 1. 배열에서 특정 범위의 요소 개수 구하기

```javascript
function countInRange(arr, min, max) {
    const leftBound = findInsertPosition(arr, min);
    const rightBound = findInsertPosition(arr, max + 1);
    return rightBound - leftBound;
}

// 사용 예시
const numbers = [1, 2, 3, 3, 3, 4, 5, 6];
console.log(countInRange(numbers, 3, 5)); // 출력: 4 (3, 3, 3, 4, 5 중에서 3~5 범위)
```

### 2. 회전된 정렬 배열에서 탐색

> 회전된 정렬 배열이란?<br/>
> 회전된 정렬 배열은 원래 정렬된 배열을 특정 지점에서 잘라서 앞뒤를 바꾼 배열입니다.<br/>
> <br/>
> 예시로 이해하기
>
> // 원본 정렬 배열<br/>
> [1, 2, 3, 4, 5, 6, 7]
> 
> // 인덱스 4에서 회전 (pivot = 4) <br/>
> [5, 6, 7, 1, 2, 3, 4]
> 
> // 인덱스 2에서 회전 (pivot = 2)  <br/>
> [3, 4, 5, 6, 7, 1, 2]
> 
> // 인덱스 0에서 회전 (회전하지 않음)<br/>
> [1, 2, 3, 4, 5, 6, 7]

```javascript
function searchInRotatedArray(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        
        if (arr[mid] === target) {
            return mid;
        }
        
        // 왼쪽 절반이 정렬되어 있는 경우
        if (arr[left] <= arr[mid]) {
            if (target >= arr[left] && target < arr[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } 
        // 오른쪽 절반이 정렬되어 있는 경우
        else {
            if (target > arr[mid] && target <= arr[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    
    return -1;
}

// 사용 예시
const rotatedArray = [4, 5, 6, 7, 0, 1, 2];
console.log(searchInRotatedArray(rotatedArray, 0)); // 출력: 4
```

## 핵심

핵심은 탐색 범위를 올바르게 조정하고 경계 조건을 정확히 처리하는 것.