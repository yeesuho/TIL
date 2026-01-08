2026.01.08

먼저 본론으로 들어가기 전에 고수 개발자는 이 내용을 보면 안됩니다 저는 고등학생 아기 개발자이기 때문에 고수개발자님들은 뭐야 이걸 몰랐어? 라는 말이 나올 수 있기 때문에 뒤로가기를 눌러주시길 바랍니다

<br>


기능대회 문제 푸는데 api와 연결하면서 겪은건데요 연습용 서버니까 localhost로 접속하려고 했는데 

```cmd
Reloaded 1 of 1072 libraries in 729ms (compile: 43 ms, reload: 308 ms, reassemble: 191 ms). E/flutter (21641): [ERROR:flutter/runtime/dart_vm_initializer.cc(40)] Unhandled Exception: ClientException with SocketException: Connection refused (OS Error: Connection refused, errno = 111), address = localhost, port = 57064, uri=http://localhost:3000/auth/login E/flutter (21641): #0 IOClient.send (package:http/src/io_client.dart:227:7) E/flutter (21641): <asynchronous suspension> E/flutter (21641): #1 BaseClient._sendUnstreamed (package:http/src/base_client.dart:93:32) E/flutter (21641): <asynchronous suspension> E/flutter (21641): #2 _withClient (package:http/http.dart:170:12) E/flutter (21641): <asynchronous suspension> E/flutter (21641): #3 AuthController.login (package:connex_chat/controller/auth.dart:9:22) E/flutter (21641): <asynchronous suspension> E/flutter (21641): #4 _LoginPageState.build.<anonymous closure> (package:connex_chat/ui/view/login.dart:163:58) E/flutter (21641): <asynchronous suspension> E/flutter (21641):
```
이런식으로 오류 메세지가 뜨는거에요<br>
해석을 하자면 대충 Flutter앱이 localhost:3000에 접속하려 했는데<br>
그 주소/포트에 서버가 안떠있어서 거절 됐다는겁니다

```dart
import 'package:connex_chat/data/model/conversation.dart';
import 'package:connex_chat/data/model/employee.dart';
import 'package:connex_chat/data/model/unread_chat.dart';

class DataController {
  static final baseUrl = 'http://localhost:3000';
  static final headers = {'Content-Type' : 'aplication/json'};

  static List<Employee> employee = [];
  static List<UnreadChat> unreadChat = [];
  static List<Conversation> conversation = [];
}
```

그래서 DataController에 가서 baseUrl을 확인했는데 엥? 난 로컬호스트 잘 넣었는데 왜 이런거지? 라고 생각했는데 찾아보니까

### 에뮬레이터에서는 localhost가 "내PC"가 아니라는 겁니다
Android 에뮬레이터에서 `localhost` = **에뮬레이터 자기 자신**
실제폰도 마찬가지로 `localhost` = **폰 자기 자신** 이기 때문에 PC에서 localhost로 서버가 켜져있어도 앱은 그걸 보지 못하는겁니다

### Android 에뮬레이터
그래서 만약 <b>Android 에뮬레이터</b>라면 `http:// 10.0.2.2:3000`로 바꿔야 하고

### 실제 폰
<b>실제폰</b>이라면 PC의 로컬 IP로 접속해줘야 합니다<br> 예시: `http://192.168.0.23:3000`

물론 여러분은 진짜로 서버가 안켜져있을 수 있으니 잘 확인하세요 안그러면 탈모옵니다

<br>

## 그래서 왜 10.0.2.2 인데??
Android 에뮬레이터는 당신 PC 위에서 돌아가긴 하지만<br> 네트워크는 에뮬레이터만의 가상 LAN이 안에 따로 있습니다<br>
그래서 에뮬레이터에서 localhost(127.0.0.1) => 에뮬레이터 자기 자신이고<br> PC에서 실행중인 서버(=PC의 localhost:3000)로 가야합니다

>이때 에뮬레이터는 `호스트 PC(당신 컴퓨터)`를 가리키는 게이트웨이 주소를 하나 제공하는데 그게 바로 `10.0.2.2` 입니다

<br>

### 요약하자면
10.0.2.2 = 내 에뮬레이터가 돌아가는 PC(호스트)의 localhost

오늘도 저는 지식을 얻어가네요