# Context와 Provider

<div align="right">2025.06.04</div>

## Context
  - 데이터의 "형태"를 정의
  - 어떤 데이터와 함수들이 있는지 명시
  - TypeScript에서는 인터페이스나 타입으로 정의
  - `useContext` 훅으로 접근

## Provider
  - 실제 데이터와 로직을 구현
  - 상태 관리 및 업데이트 담당
  - 하위 컴포넌트들을 감싸는 컴포넌트
  - Context의 `value` prop으로 데이터 제공

<br/>

## 코드와 함께 설명
### Context (공유 저장소)
```typescript
interface TodoContextProps {
  todos: Todo[];
  addTodo: (text: string, priority: Priority) => void;
  toggleDone: (todo: Todo) => void;
  deleteTodo: (todo: Todo) => void;
  reorderTodo: (newTodos: Todo[]) => void;
}

const TodoContext = createContext<TodoContextProps | undefined>(undefined);
```
- Context는 데이터를 담고 있음
- 여러 컴포넌트에서 공유해야 하는 데이터나 함수들을 정의
- `createContext()`로 생성되며, 초기값을 설정할 수 있음
- Context 자체는 데이터의 형태(타입)만 정의하고 있음

<br/>

### Provider (제공자)
```typescript
const TodoProvider = ({ children }: { children: ReactNode }) => {
  const [todos, setTodos] = useState<Todo[]>(initialTodos);

  const addTodo = (text: string, priority: Priority) => {
    // ... 구현 ...
  };

  return (
    <TodoContext.Provider value={{ todos, addTodo, deleteTodo, toggleDone, reorderTodo }}>
      {children}
    </TodoContext.Provider>
  );
}
```
- Provider는 Context에 실제 데이터를 제공하는 컴포넌트
- 상태(state)와 그 상태를 변경하는 함수들을 구현
- `children`을 감싸서 하위 컴포넌트들에게 데이터를 제공
- 실제 데이터의 관리와 업데이트를 담당


<br/>

## 차이점과 관계
```typescript
// App.tsx 등에서
function App() {
  return (
    {/* Provider로 감싸기 */}
    <TodoProvider>      
      {/* 이 안에서는 Todo 관련 데이터/함수 사용 가능 */}
      <HomeScreen />    
      <SettingsScreen />
    </TodoProvider>
  );
}

// 어떤 하위 컴포넌트에서
function TodoList() {
  // Context 사용
  const { todos, toggleDone } = useContext(TodoContext);  
  
  // ... 구현 ...
}
```

<br/>

## Context와 Provider의 장점
- Props Drilling 문제 해결 (여러 단계의 컴포넌트를 거치지 않고 직접 데이터 접근)
- 전역 상태 관리 가능
- 관련 로직을 한 곳에서 관리 가능
- 컴포넌트 간 데이터 공유가 쉬워짐
