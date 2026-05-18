2026.05.07

n8n은 여러 서비스를 노드로 연결해서 자동화하는 도구라는데

대충 사람이 반복해서 하던 작업을 자동으로 실행할 수 있게 해준답니다



## n8n 핵심 개념
### Workflow
자동화 전체 흐름

예시
```
쇼츠 대본 자동 생성 워크플로우
```

### Node
자동화 안에서 하나의 작업 단위

예시
```
Manual Trigger
Google Sheets
Message a model
Edit Fields
```


### Trigger
워크플로우를 시작하는 노드

오늘은 직접 버튼을 눌러 실행하는:
``Manual Trigger``를 사용해보았습니다

### Credential
외부 서비스에 로그인하거나 권한을 연결하는 설정

오늘은 Google Sheets를 사용하기 위해 Google 계정을 연결헤보았습니다
사실 그냥 GPT가 하라는대로 따라해서 제가 크게 한건 없습니다

<br>

# 처음 만든 자동화 구조
처음에는 n8n 안에서 직접 주제를 만들어보았습니다
```
Manual Trigger
↓
Edit Fields
↓
Message a model
↓
Edit Fields1
↓
Google Sheets Append Row
```

동작 방식
```
직접 topic 입력
↓
OpenAI가 쇼츠 대본 생성
↓
script 값만 추출
↓
Google Sheets에 새 행으로 저장
```

### 사용한 데이터 구조

처음에는 이런 데이터를 만들었습니다
```json
{
  "topic": "앱 개발을 시작해야 하는 이유"
}
```

n8n에서는 노드끼리 데이터를 JSON 형태로 주고받는데요

크게 막 코드를 짜는건 없고 JSON 필드의 값을 사용하기 위한 기본적인 문법만 알면 됐습니다

### n8n Expression 문법

앞에 있는 노드의 값을 가져올 때 이런 문법을 씁니다
```
{{ $json.topic }}
```
>뜻: 현재 입력 데이터에서 topic 값을 가져와라

<br>

OpenAI 결과 안에 있는 텍스트를 꺼낼 때는 이렇게 써줬습니다
```
{{ $json.output[0].content[0].text }}
```
>뜻: OpenAI 응답 안에 들어 있는 실제 대본 텍스트만 꺼내라

<br>

특정 노드의 값을 직접 가져올 수도 있는데요
```
{{ $('Get row(s) in sheet').item.json.topic }}
```
>뜻: Get row(s) in sheet 노드에서 topic 값을 가져와라

<br>

### Google Sheets에 저장하는 자동화

구글시트에 이런 컬럼을 만들어주고
```
topic | script | status | createdAt
```
처음에는 Append Row를 사용해서 새 행을 추가했습니다

```
topic = {{ $json.topic }}
script = {{ $json.script }}
status = generated
createdAt = {{ $now }}
```

결과적으로 AI가 만든 쇼츠 대본이 구글시트에 자동으로 저장됐습니다

# 두번째 자동화 구조

두 번째 버전에서는 n8n 안에서 주제를 직접 입력하지 않고, Google Sheets에서 가져오게 만들었습니다

구글시트에 이렇게 입력해주고
```
topic: AI 자동화가 앞으로 중요한 이유
status: pending
```
따로 내용을 안쓰고 n8n에서 status = pending인 행만 가져오도록 설정했습니다
```
Column: status
Value: pending
```

또 여러 pending 행 중 하나만 처리하기 위해 옵션을 켰습니다

``Return only First Matching``

### 1. 최종 워크플로우 구조

현재 완성한 구조
```
Manual Trigger
↓
Google Sheets Get Row(s)
↓
Message a model
↓
Edit Fields
↓
Google Sheets Update Row
```
동작 방식
```
Google Sheets에서 pending 상태인 주제 1개 가져오기
↓
OpenAI가 그 주제로 쇼츠 대본 생성
↓
script, status, createdAt 값 정리
↓
기존 행을 업데이트
```
### 최종 결과

구글시트에서 이 상태였던 행이:
```
topic: AI 자동화가 앞으로 중요한 이유
script:
status: pending
createdAt:
```
이제 n8n 실행하면 밑에 처럼 결과가 나옵니다
```
topic: AI 자동화가 앞으로 중요한 이유
script: (AI가 만든 쇼츠 대본)
status: generated <- pending에서 generated로 수정됨
createdAt: (생성 시간)
```
구글시트에 주제만 적고 pending으로 표시하면 n8n이 자동으로 대본을 만들어서 같은 행에 저장하는 시스템을 만들어보았습니다


## 소감
일단 오늘은 여기까지 만들어봤는데 생각보다 크게 어렵지 않고 눈에 결과가 바로바로 보이니까 재밌었습니다

그냥 버튼 딸깍 누르니까 내용 생성되고 구글시트에 정리되는거 보고 뭔가 도파민 느껴졌고 세상 참 좋아졌다고 느꼈습니다

아직 쇼츠 자동화까진 못했지만 앞으로 더 공부하고 기회가 되면 강의도 사서 보면서 계속해서 만들어볼 생각입니다!!