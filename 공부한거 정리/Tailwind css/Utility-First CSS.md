2025.04.24

# Utility-First CSS란
CSS를 작성하는 하나의 방식<br>
이 방식은 작은 단위의 클래스들(유틸리티 클래스)을 사용해서 스타일을 구성해나가는 것

### 기존 CSS 
```css
/* 전통적인 방식 */
.card {
  background-color: white;
  padding: 1rem;
  border-radius: 0.5rem;
}
```

### HTML에 사용하는 방식
```html
<div class="card">Hello</div>
```

### Utility-first CSS
```html
<div class="bg-white p-4 rounded-md">Hello</div>
```