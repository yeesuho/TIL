2025.03.04

## 맥북에서 npm 설치시 매번 권한 오류로 sudo 없인 설치가 안되어서 찾다가 발견한 방법

```
sudo chown -R $(whoami) ~/.npm
```
디렉토리의 소유권 ~/.npm과 모든 내용을 현재 로그인된 사용자로 변경합니다

<br>

```
sudo chown -R $(whoami) /usr/local/lib/node_modules
```
 디렉토리의 소유권 /usr/local/lib/node_modules과 모든 내용을 현재 로그인된 사용자로 변경합니다

 <br>

 [**출처**](https://velog.io/@ddudii/%EB%A7%A5%EB%B6%81%EC%97%90%EC%84%9C-%EA%B6%8C%ED%95%9C-%EC%98%A4%EB%A5%98%EB%A1%9C-npm-%EC%84%A4%EC%B9%98-%EC%95%88%EB%90%A0%EB%95%8C)