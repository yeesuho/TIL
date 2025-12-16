2025.04.01

[공식사이트](https://styled-components.com/)

<br>

컴포넌트가 많은 경우 스타일링을 하다보면 불편함이 생기는데<br>
class 만들어놓은걸 까먹고 중복해서 또 만들거나<br>
갑자기 다른 이상한 컴포넌트에 원하지않는 스타일이 적용되거나<br>
CSS 파일이 너무 길어져서 수정이 어렵거나<br>
이런 경우가 있죠<br>
그래서 스타일을 바로 입혀서 컴포넌트를 만들어버릴 수도 있는데<br>
바로 styled-components 라는 라이브러리입니다

<br>

> 일단 설치부터 <br>

터미널에서
```less
npm install styled-components
```
이거 써주고


```tsx
import styled from 'styled-components'
```
그리고 사용하고 싶은 컴포넌트 맨위에 이런걸 import 해줍니다 그럼 일단 셋팅 끝

## styled-components 기본적인 사용법 
이 라이브러리를 이용하면 컴포넌트를 만들 때 스타일을 미리 주입해서 만들 수 있습니다<br>

 예시로 padding : 20px인 div박스를 styled-components를 이용해 만들어보면
```tsx
import styled from 'styled-components';

let Box = styled.div`
  padding : 20px;
  color : grey
`;
let YellowBtn = styled.button`
  background : yellow;
  color : black;
  padding : 10px;
`;

function App(){
  return (
    <div>
      <Box>
        <YellowBtn>버튼</YellowBtn>
      </Box>
    </div>
  )
}

```
``<div>``를 하나 만들고 싶으면 저렇게 styled.div 라는걸 사용하면 되고 예를 들어 ``<p>`` 만들려면 styled.p 이런 식 

오른쪽에 `` backtick(백틱) 기호를 이용해서 CSS 스타일을 넣을 수 있고 그 자리에 컴포넌트가 남아서 변수에 저장해서 사용할 수 있죠

### 장점

**장점1.** CSS 파일 오픈할 필요없이 JS 파일에서 바로 스타일넣을 수 있습니다

**장점2.** 여기 적은 스타일이 다른 JS 파일로 영향을 주지 않습니다

**장점3.** 페이지 로딩시간 단축됩니다

왜냐면 저기 적은 스타일은 html 페이지에서 
``<style>``태그에 넣어줘서 그렇죠

### 실은 일반 CSS 파일도 가능

 App.css 파일을 만들어서 App.jsx에서 import해서 쓴다고 해도 거기 적은 클래스명들은 다른 jsx 파일에서 사용이 가능합니다<br>
 하지만 프로젝트 사이즈가 작을 땐 편리하겠지만 사이즈가 커지면 관리하기 힘들어지죠

그럴 땐 styled-components 써도 되지만 그냥 CSS파일에서도 다른 JS 파일에 간섭하지 않는 '모듈화' 기능을 제공하는데
```less
컴포넌트명.module.css
```
이런식으로 CSS 파일을 작명하면 됩니다<br>
그리고 컴포넌트명.jsx 파일에서 import 해서 쓰면 그 스타일들은 컴포넌트명.jsx 파일에만 적용됩니다


## 추가 문법 : props로 재활용가능
여러가지 비슷한 UI가 필요한 경우 어쩔까요<br>
예를 들어 지금 노란 버튼말고 오렌지색 버튼이 필요해진다면<br>
props 이용하면 기존 컴포넌트를 살짝씩 다르게 이용할 수 있고 여기서도 props 문법을 지원해서 사용할 수 있습니다
```tsx
import styled from 'styled-components';

let YellowBtn = styled.button`
  background : ${ props => props.bg };
  color : black;
  padding : 10px;
`;

function Detail(){
  return (
    <div>
        <YellowBtn bg="orange">오렌지색 버튼</YellowBtn>
        <YellowBtn bg="blue">파란색 버튼</YellowBtn>
    </div>
  )
}
```
``${ props => props.bg }`` 이게 styled-components 에서의 props를 사용하는 문법입니다<br>
그럼 이제 위에 코드처럼 bg부분에 자유롭게 작명하면되고<br>
이제 컴포넌트 쓸 때 bg라는 props를 입력가능합니다

물론 CSS 쓴다고 이게 불가능한건 아닙니다<br> 
class 더 만들면 되는 것

<br>

```tsx
let YellowBtn = styled.button` 
  background : ${ props => props.bg };
  color : ${ props => props.bg == 'blue' ? 'white' : 'black' };
  padding : 10px; 
`; 
```
자바스크립트 적는 공간이다보니까 이런 식의 스타일 프로그래밍도 가능합니다<br>
삼항 연산자를 사용해서 배경색이 파란색이면 글자색을 흰색으로 아니라면 검은색으로<br> 이런식으로 사용 가능합니다



## 장점만 있는게 어딨을까요
물론 단점도 있습니다<br>

**단점1.** JS 파일이 매우 복잡해지죠<br>
그리고 이 컴포넌트가 styled 인지 아니면 일반 컴포넌트인지 구분도 어려울 수 있습니다

**단점2.** JS 파일 간 중복 디자인이 많이 필요하면 어쩔까요?<br>
다른 파일에서 스타일 넣은 것들 import 해와서 쓰면 됩니다
<br>
근데 그럼 CSS파일 쓰는거랑 차이가 없을 수 있죠

**단점3.** CSS 담당하는 디자이너가 있다면 협업시 불편할텐데 <br>
그 사람이 styled-components 문법을 모른다면 
<br>
그 사람이 CSS로 짠걸 styled-components 문법으로 다시 바꾸거나 그런 작업이 필요하겠군요
<br>
그래서 신기술같은거 도입시엔 언제나 미래를 생각해보아야합니다