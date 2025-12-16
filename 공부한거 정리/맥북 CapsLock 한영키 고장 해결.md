2025.04.23

이전까지는 잘 됐는데 갑자기 capslock 한영키가 씹힘과 동시에 잘 작동을 안해서(딜레이도 걸림) 해결한 방법을 적어보겠습니다

## 카라바이너 설치(Karabiner Install)
찾아본 결과 이게 사람들이 가장 많이 쓰는 방법인 것 같고<br>처음엔 프로그램을 깔고 세팅하기 싫었지만 막상 하고 나니 오히려 좋습니다

https://karabiner-elements.pqrs.org/ <br>
위 url에 들어가서 자신에게 맞는 카라바이너를 설치해줍니다

## 카라바이너 세팅(Karabiner Setting)
설치된 카라바이너에 들어가 Add Item을 클릭 <br>
카라바이너 설치 시 맨 처음 뜨는 세큐리티 해제 설정을 해 줘야합니다<br>
권한 설정을 다 해주고 나서 
**From key에 Modifier Keys -> caps_lock, To key에 Function Keys -> f19 를 설정해주기만 하면 됩니다**

![img](/img/karabiner_setting.png)

## 키보드 설정(Keyboard Setting)
좌측 상단에 보이는 사과 로고 -> 시스템 환경설정 -> 키보드를 클릭

키보드를 클릭<br>
키보드 단축키 -> 입력 소스로 들어가서

![img](/img/karabiner_setting2.png)
입력 메뉴에서 다음 소스 선택 부분을 선택<br>
Caps Lock 키로 눌러주면 위 사진들처럼 F19로 바뀌는 것을 볼 수 있습니다<br>
(이 과정에서 진행되지 않을 경우 카라바이너 권한이 없는지를 확인)<br>
이후에는 우리가 평소 한영키 쓰듯이 문제 없이 한/영이 바뀌는 것을 볼 수 있죠<br>
**단, 주의할 점은 caps lock 고유의 기능인 대문자를 유지한 채로 출력하는 것은 할 수 없습니다**<br>
입력할 때에 shift를 누르고 사용하면 되긴 함

[참고한 블로그](https://velog.io/@pocpoc0202/%EB%A7%A5%EB%B6%81-%ED%95%9C%EC%98%81%ED%82%A4-%EB%A7%A5%EB%B6%81-Caps-Lock-%ED%95%9C%EC%98%81%EC%A0%84%ED%99%98-%EB%94%9C%EB%A0%88%EC%9D%B4-%EC%97%90%EB%9F%AC%EB%A7%A5%EB%B6%81-%ED%95%9C%EC%98%81%ED%82%A4-%EA%B3%A0%EC%9E%A5-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0)


<br>

2025.04.27

추가로 vscode에서 한글이 씹히는 문제가 있어서 간단하게 해결한 방법입니다<br>
[참고](https://velog.io/@fnqhdtm/issu)