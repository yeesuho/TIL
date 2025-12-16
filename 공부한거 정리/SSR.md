2025.03.10

## SSR 프레임워크란?
**SSR(Server-Side Rendering)** 프레임워크는 서버에서 HTML을 미리 생성한 후, 브라우저로 전달하는 방식을 지원하는 웹 프레임워크
<br>

일반적인 클라이언트 사이드 렌더링(CSR)과 비교했을 때, 초기 로딩 속도가 빠르고 SEO(검색 엔진 최적화)에 유리

## SSR vs CSR 차이점
|  방식 |  설명 | 장점 | 단점 | 
|:------:|:----:|:----:|:----:|
CSR (Client-Side Rendering) | 브라우저에서 JS로 HTML을 동적으로 생성 | - 사용자 경험(UX) 좋음<br>- 서버 부하 적음 | - 초기 로딩 속도 느림<br>- SEO 불리함
SSR (Server-Side Rendering) | 서버에서 HTML을 미리 생성 후 브라우저에 전달 | - 초기 로딩 속도 빠름<br>- SEO 유리 | - 서버 부하 증가<br>- 구현 난이도 있음


### 대표적인 SSR 프레임워크
|프레임워크|기반|특징|
|:------:|:----:|:----:|
Next.js | React | 가장 인기 있는 SSR 프레임워크, 정적 & 동적 페이지 지원
Nuxt.js | Vue.js | Vue.js 기반의 SSR 지원 프레임워크
NestJS (SSR 모드) | Node.js | 기본적으로 백엔드 프레임워크지만 SSR도 가능

## SSR 동작 예제

### CSR 방식 (React)
``` js
function Page() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data')
      .then(res => res.json())
      .then(setData);
  }, []);

  return <div>{data ? data.message : 'Loading...'}</div>;
}
```
브라우저가 처음에는 빈 HTML을 받고, 이후 JS가 실행되면서 데이터가 로드됨.<br>
초기 로딩이 느리고, 검색 엔진이 HTML을 제대로 읽지 못할 수도 있음.

### SSR 방식 (Next.js)
```
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}

export default function Page({ data }) {
  return <div>{data.message}</div>;
}
```
서버에서 데이터를 미리 가져와서 HTML을 생성한 후, 브라우저로 보냄.<br>
초기 로딩이 빠르고, SEO(검색 엔진 최적화)에 유리함.


##  SSR 프레임워크를 언제 써야 할까?
• SEO가 중요한 서비스 ex.블로그, 뉴스 사이트, 쇼핑몰 등 <br>
• 초기 로딩 속도가 중요한 경우 ex.광고, 랜딩 페이지 등 <br>
• 자주 변하는 데이터를 표시해야 할 때 ex.실시간 데이터 기반 웹앱


## 요약
• SSR(Server-Side Rendering): 서버에서 미리 HTML을 생성해서 보내는 방식 <br>
• CSR(Client-Side Rendering): 브라우저에서 JS가 HTML을 렌더링하는 방식<br>
• Next.js / Nuxt.js 같은 프레임워크가 대표적인 SSR 프레임워크


<br>

**SEO** = SEO(검색 엔진 최적화, Search Engine Optimization) 는 웹사이트가 구글, 네이버 같은 검색 엔진에서 더 잘 검색되도록 최적화하는 작업