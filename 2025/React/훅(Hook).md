2025.03.30

#  훅(Hook)이 등장한 이유
React에서는 함수형 컴포넌트가 가볍고 사용하기 편리하지만, 예전에는 상태 관리와 생명주기 기능이 부족했다<br>
이 문제를 해결하기 위해 **React 16.8(2019년)** 에서 **"Hooks(훅)"** 이 등장

### 훅이 필요한 이유
1. 클래스형 컴포넌트 없이도 상태(state)와 생명주기(lifecycle)를 다룰 수 있다
2. 코드가 더 간결하고 가독성이 좋아짐
3. 재사용성과 유지보수가 쉬움

<br>

# useState, useRef, useEffect
### useState – 상태(state) 관리
컴포넌트 내부에서 상태를 만들고 변경할 수 있음
```tsx
import { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0); // 상태 선언

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
};

export default Counter;
```
```useState(초기값)``` → 상태 변수 ```count```와 변경 함수 ```setCount``` 생성 <br>
setCount(newValue)를 호출하면 컴포넌트가 다시 렌더링됨

<br>

### useRef – 참조(reference) 저장 (DOM 조작 가능)
useRef는 렌더링 없이 값을 저장하는 용도<br>
document.getElementById()처럼 DOM을 직접 조작할 수도 있음!
```tsx
import { useRef } from "react";

const InputFocus = () => {
  const inputRef = useRef(null); // ref 생성

  const handleFocus = () => {
    inputRef.current.focus(); // input에 포커스 주기
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="입력하세요" />
      <button onClick={handleFocus}>포커스 이동</button>
    </div>
  );
};

export default InputFocus;
```
```inputRef.current.focus()```를 호출하면 input에 포커스가 감!<br>
``useRef``는 렌더링되지 않기 때문에 상태 관리보다 가벼움

<br>

### useEffect – 사이드 이펙트 관리 (라이프사이클 대체)
useEffect는 컴포넌트가 마운트, 업데이트, 언마운트될 때 특정 동작을 수행할 수 있게 해줌
```tsx
import { useState, useEffect } from "react";

const Timer = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("마운트 & 업데이트 실행됨", count);

    return () => {
      console.log("언마운트됨");
    };
  }, [count]); // count가 변경될 때마다 실행됨

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
};

export default Timer;
```
useEffect(() => { 실행할 코드 }, [의존성])<br>
[count] → count 값이 변경될 때만 실행됨<br>
언마운트 시 return 내부 코드 실행 (클린업 함수)