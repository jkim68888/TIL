# 스프레드 연산자와 Rest 파라미터 활용하기

<div align="right">2025.06.16</div>

<br/>

## 1. 스프레드 연산자(Spread Operator)란?

스프레드 연산자(`...`)는 ES6에서 도입된 문법으로, 배열이나 객체를 펼쳐서 개별 요소로 분리할 수 있게 해주는 연산자입니다.

### 1.1 배열에서의 사용
```javascript
const numbers = [1, 2, 3];
const moreNumbers = [...numbers, 4, 5]; // [1, 2, 3, 4, 5]

// 배열 복사
const original = [1, 2, 3];
const copy = [...original]; // [1, 2, 3]
```

### 1.2 객체에서의 사용
```javascript
const person = { name: 'John', age: 30 };
const updatedPerson = { ...person, age: 31 }; // { name: 'John', age: 31 }

// 객체 복사
const original = { a: 1, b: 2 };
const copy = { ...original }; // { a: 1, b: 2 }
```

## 2. Rest 파라미터란?

Rest 파라미터는 함수의 매개변수에서 사용되는 문법으로, 나머지 매개변수들을 하나의 배열로 모아줍니다.

### 2.1 기본 사용법
```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2, 3, 4); // 10
```

### 2.2 객체 구조 분해 할당에서의 사용
```javascript
const { name, age, ...rest } = person;
// name과 age를 제외한 나머지 속성들이 rest 객체에 할당됨
```

## 3. 실제 사용 예시

### 3.1 React/React Native 컴포넌트에서의 활용
```typescript
interface ButtonProps {
  style?: StyleProp<ViewStyle>;
  onPress?: () => void;
  title: string;
  // ... 기타 props
}

function CustomButton({ style, onPress, title, ...rest }: ButtonProps) {
  return (
    <TouchableOpacity
      style={[styles.button, style]}
      onPress={onPress}
      {...rest}
    >
      <Text>{title}</Text>
    </TouchableOpacity>
  );
}
```

### 3.2 상태 업데이트에서의 활용
```javascript
const [user, setUser] = useState({
  name: 'John',
  age: 30,
  preferences: {
    theme: 'dark',
    notifications: true
  }
});

// 특정 속성만 업데이트
setUser(prev => ({
  ...prev,
  age: 31
}));

// 중첩된 객체 업데이트
setUser(prev => ({
  ...prev,
  preferences: {
    ...prev.preferences,
    theme: 'light'
  }
}));
```

## 4. 주의사항

### 4.1 얕은 복사(Shallow Copy)
스프레드 연산자는 얕은 복사를 수행합니다. 중첩된 객체나 배열의 경우 내부 요소들은 참조가 복사됩니다.

```javascript
const original = {
  user: {
    name: 'John',
    age: 30
  }
};

const copy = { ...original };
copy.user.age = 31; // original.user.age도 31로 변경됨
```

### 4.2 성능 고려사항
대규모 객체나 배열을 스프레드 연산자로 복사할 때는 성능에 영향을 줄 수 있습니다. 이 경우 `Object.assign()`이나 `Array.from()`을 고려해볼 수 있습니다.

## 5. 장점

- 코드의 가독성이 향상됩니다
- 불변성을 유지하기 쉬워집니다
- 코드의 재사용성이 높아집니다
- 더 선언적이고 함수적인 프로그래밍이 가능해집니다
