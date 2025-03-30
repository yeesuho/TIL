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


## 생명주기(Lifecycle)란?
React 컴포넌트는 **"생명주기(라이프 사이클)"** 를 가지고 있음 <br>
컴포넌트가 화면에 나타나고, 업데이트되며, 사라지는 과정이 정해져 있음

리액트 생명주기 단계
1. 마운트 (Mount) - 컴포넌트가 처음 화면에 나타남
2. 업데이트 (Update) - 상태(state)나 속성(props)이 변경됨
3. 언마운트 (Unmount) - 컴포넌트가 화면에서 사라짐

### 생명주기 예제 (useEffect 사용)
```tsx
import { useEffect, useState } from "react";

const Timer = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("마운트됨");

    return () => {
      console.log("언마운트됨");
    };
  }, []);

  useEffect(() => {
    console.log("count 변경됨:", count);
  }, [count]);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
};

export default Timer;
```
처음 마운트될 때 ``마운트됨`` 출력<br>
count가 변경될 때 ``count 변경됨`` 출력<br>
컴포넌트가 사라질 때 ``언마운트됨`` 실행<br>
