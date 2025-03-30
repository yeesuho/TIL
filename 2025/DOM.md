2025.03.30
# DOM이란?
DOM(Document Object Model)은 HTML 문서를 구조화해서 브라우저가 이해할 수 있도록 만든 객체 모델 <br>
쉽게 말해서: HTML을 브라우저가 읽고, 트리 구조로 변환한 것

## HTML과 DOM 구조 비교
### HTML 코드
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello, DOM!</h1>
    <button>Click Me</button>
  </body>
</html>
```

### 브라우저가 이해하는 DOM 구조 (트리 형태)
```less
document
 ├── html
 │    ├── head
 │    │    └── title ("My Page")
 │    └── body
 │         ├── h1 ("Hello, DOM!")
 │         └── button ("Click Me")
```
브라우저는 HTML을 객체(Tree 구조)로 변환해서 조작할 수 있도록 함

# DOM 조작이란?
DOM을 변경하는 걸 **DOM 조작(DOM Manipulation)** 이라고 한다<br>
일반적인 JavaScript에서는 document 객체를 사용해서 DOM을 조작할 수 있음

### DOM 조작 예제 (Vanilla JS)
```js
// 버튼 요소 가져오기
const button = document.querySelector("button");

// 클릭하면 텍스트 변경
button.addEventListener("click", () => {
  document.querySelector("h1").textContent = "DOM 변경됨";
});
```
``querySelector("h1")`` → ``<h1>`` 요소를 가져와서<br>
``textContent = "DOM 변경됨"`` 으로 내용을 바꿈