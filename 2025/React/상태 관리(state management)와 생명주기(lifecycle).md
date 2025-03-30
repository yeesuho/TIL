2025.03.30
## 상태 관리(State Management)란?
React에서 상태(state) 는 컴포넌트가 가지고 있는 동적인 값 <br>
예를 들어 버튼 클릭 수, 입력 폼의 값, 체크박스 상태 등이 상태에 해당된다<br>
### 상태(state)의 특징
상태가 변경되면 자동으로 리렌더링됨<br>
useState 또는 useReducer를 사용해서 상태를 관리할 수 있음
```tsx
import { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0); // count 상태

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
};

export default Counter;

```
버튼을 누르면 count 값이 증가하고, 컴포넌트가 다시 렌더링됨