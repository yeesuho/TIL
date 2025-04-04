2025.03.05

NestJS의 기본 파일 구조는 모듈(Module) 기반 아키텍처를 따릅니다

## NestJS 기본 파일 구조
```
my-nest-app/
│── src/                  # 주요 애플리케이션 코드
│   ├── app.controller.ts # 기본 컨트롤러
│   ├── app.module.ts     # 루트 모듈
│   ├── app.service.ts    # 기본 서비스
│   ├── main.ts           # 애플리케이션의 진입점
│
├── test/                 # 테스트 코드
├── node_modules/         # 프로젝트 의존성
├── .eslintrc.js          # ESLint 설정 파일
├── .gitignore            # Git에서 무시할 파일 목록
├── package.json          # 프로젝트 기본 설정 및 의존성
├── tsconfig.json         # TypeScript 설정 파일
└── nest-cli.json         # Nest CLI 설정 파일

```

2025.03.18 

CRUD 보일러플레이트 자동 생성 기능
``` 
$ nest g resource [name]
```
예를 들어 **nest g resource Users** 명령으로 Users 리소스를 생성했다면 module, controller, service, entity, dto 등의 코드와 테스트 코드를 자동 생성해줍니다