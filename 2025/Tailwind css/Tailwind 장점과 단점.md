2025.04.25
## Tailwind의 
### 실제 창립자의 의도
Tailwind의 창립자인 Adam Wathan이 처음 만들 때 이런 얘길 했답니다

>“I wanted something that didn’t get in your way, but helped you move faster — like a tailwind.”

>“나는 방해하지 않고, 더 빨리 움직이게 도와주는 무언가를 원했어 — tailwind처럼.”

일단 이름의 뜻은 뒷바람? 이라는 뜻으로 비행기나 배가 진행 방향으로 불어주는 바람<br> 즉 "도와주는 바람" 을 말하는 것 같습니다<br> 이름은 멋있다고 생각합니다
### 장점
- Utility-First의 편리함과 빠른 개발
    - 스타일 코드가 HTML 코드 안에 있기 때문에 HTML와 CSS 파일을 별도로 관리할 필요가 없음
    - 원하는 태그의 스타일을 변경하기 위해 클래스명을 검색해가며 일일이 필요한 CSS 코드를 찾을 수고가 사라짐
- 일관된 디자인
  - 모든 곳에서 동일한 색상이나 사이즈, 간격 등의 유틸리티 클래스를 사용하므로 일관된 스타일로 구현하기가 수월
- 쉽고 자유로운 커스텀
  - Tailwind CSS는 다른 프레임워크들에 비해 기본 스타일 값을 디테일한 부분까지 쉽게 커스텀이 가능
- UI component 제공
  - [tailwindUI](https://tailwindcss.com/plus)<br>
  - [tailwindcomponents(무료)](https://www.creative-tim.com/twcomponents/)<br>
  - [Material Tailwind](https://www.material-tailwind.com/)

### 단점
- 코드의 가독성이 떨어짐
- 초반 클래스명 러닝 커브
  - 초반에는 각 스타일의 클래스명을 익히느라 개발하는 내내 공식 문서를 참고해야 하는 번거로움이 있음
- JavaScript 코드 사용 어려움
    - styled-components와 같이 JavaScript 변수 값에 따라 가로 길이를 설정하는 등의 구현은 가능하기는 하지만 무척 번거로운 설정이 필요
    - 커스텀디자인을 하려면 tailwind.config.js에서 직접 스타일을 지정해야 하는 경우가 많음