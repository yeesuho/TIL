2025.04.02

# Props란?
**Props (Properties)** 는 React에서 컴포넌트 간 데이터를 전달하는 방법 <br>
부모 컴포넌트가 자식 컴포넌트로 값을 넘겨줄 때 사용<br>
Props는 읽기 전용(immutable)이며, 자식 컴포넌트에서 변경할 수 없다

## Props 기본 사용법
```tsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Greeting name="Alice" />;
}
```
``name="Alice"``를 ``props``로 전달 → ``props.name``을 통해 사용

<br>

## 여러 타입의 Props 전달
```tsx
function UserInfo({ user, hobbies }) {
  return (
    <div>
      <h2>{user.name} ({user.age} years old)</h2>
      <p>Hobbies: {hobbies.join(", ")}</p> 
    </div>
  );
}

function App() {
  const user = { name: "Bob", age: 25 };
  return <UserInfo user={user} hobbies={["Reading", "Gaming"]} />;
}
```
``join()``배열의 모든 요소를 하나의 문자열로 합치는 JavaScrip <br>
객체, 배열도 props로 전달 가능

<br>

## Props 기본값 설정 (Default Props)
```tsx
function Greeting({ name = "Guest" }) {
  return <h1>Hello, {name}!</h1>;
}

function App() {
  return <Greeting />;
}
```
``name`` 값이 없으면 ``"Guest"``가 기본값으로 사용됨

<br>

## Props의 단점 (Props Drilling)
``부모 → 자식 → 손자 → ... ``식으로 불필요하게 많은 컴포넌트를 거쳐야 하는 문제
```tsx
function GrandChild({ message }) {
  return <p>{message}</p>;
}

function Child({ message }) {
  return <GrandChild message={message} />;
}

function Parent() {
  return <Child message="Hello from Parent!" />;
}
```

해결 방법: [Context API 사용](./useContext.md) (``useContext``)

<br>

## TypeScript와 함께 사용하기
타입을 명확하게 지정하여 props를 안전하게 사용할 수 있음
```tsx
interface GreetingProps {
  name: string;
}

function Greeting({ name }: GreetingProps) {
  return <h1>Hello, {name}!</h1>;
}

function App() {
  return <Greeting name="Alice" />;
}

```
name이 string이 아니라면 컴파일 에러가 발생해서 안전한 코드 작성 가능하죠