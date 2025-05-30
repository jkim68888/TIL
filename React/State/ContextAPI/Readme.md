# Context API

Context API는 React에서 제공하는 전역 상태 관리 도구입니다. 컴포넌트 트리에서 데이터를 "prop drilling" 없이 전달할 수 있게 해줍니다.

## Prop Drilling 문제

일반적으로 React에서 데이터는 부모에서 자식으로 props를 통해 전달됩니다.

```jsx
// 문제: 깊은 컴포넌트까지 props를 계속 전달해야 함
App → Header → UserInfo → UserName → DisplayName
```

이렇게 되면 중간 컴포넌트들이 실제로는 사용하지 않는 props를 단지 전달하기 위해서만 받아야 합니다.

## Context API 해결책

Context API는 "전역 저장소"를 만들어서 어떤 컴포넌트든 직접 데이터에 접근할 수 있게 합니다.

## Context API의 핵심 개념

### 1. **createContext**
```typescript
const MyContext = createContext<ContextType | undefined>(undefined)
```
- 새로운 Context 객체를 생성
- 초기값을 설정할 수 있음 (보통 undefined 사용)

### 2. **Provider**
```tsx
<MyContext.Provider value={contextValue}>
  {children}
</MyContext.Provider>
```
- Context 값을 하위 컴포넌트들에게 제공
- `value` prop으로 전달할 데이터 지정

### 3. **useContext**
```typescript
const contextValue = useContext(MyContext)
```
- 컴포넌트에서 Context 값을 읽어옴
- Provider 내부에서만 사용 가능

## 장점과 단점

### 장점
- **Prop Drilling 해결**: 중간 컴포넌트를 거치지 않고 직접 데이터 접근
- **React 내장**: 별도 라이브러리 설치 불필요
- **간단한 API**: 배우기 쉽고 사용하기 직관적
- **TypeScript 지원**: 타입 안정성 보장

### 단점
- **성능 이슈**: Context 값이 변경되면 모든 하위 컴포넌트가 리렌더링
- **디버깅 어려움**: Redux DevTools 같은 고급 디버깅 도구 없음
- **복잡한 로직 한계**: 매우 복잡한 상태 로직에는 부적합

## 언제 사용하면 좋을까?

### 적합한 경우
- 사용자 정보, 테마, 언어 설정 등 전역 상태
- 여러 컴포넌트에서 공유하는 간단한 데이터
- Prop drilling이 3단계 이상 발생하는 경우

### 피해야 할 경우
- 자주 변경되는 데이터 (성능 문제)
- 매우 복잡한 상태 로직
- 시간 여행 디버깅이 필요한 경우

<br/>

Context API는 Redux와 useState 사이의 중간 단계로, 적당한 복잡도의 전역 상태 관리에 매우 유용합니다.