2025.04.24

Talwind에 기본 문법에 대해 정리해보려고 합니다<br>
React와 vite 기반으로 작성합니다

# Tailwind
간단하게 Tailwind css에 대해서 설명하자면
- [Utility-First](./Utility-First%20CSS.md) 컨셉을 가진 CSS 프레임워크

# Tailwind CSS 기본 문법

### Tailwind CSS 설치(Vite)
```bash
npm install tailwindcss @tailwindcss/vite
```

### Vite 플러그인 구성
``` bash
//vite.config.ts
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'
export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```
@tailwindcss/viteVite 구성에 플러그인을 추가


### Tailwind CSS 가져오기
```css
@import "tailwindcss";
```
`@import`Tailwind CSS를 가져오는 CSS 파일에 을 추가합니다 .


### 빌드
```bash
npm run dev
```

추가 예정