2026.03.06

벌써 3월이네요 시간 참 빨리 갑니다

오늘은 SharedPreferences 패키지의 사용법을 기록해보겠습니다<br>
전부터 자주 썼는데 자주 까먹어서 기록을 해놔야겠다 싶어서 이제야 기록합니다

## SharedPreferences란?
Flutter 앱에서 간단한 데이터를 디스크에 저장하고 불러올 수 있는 유용한 키-값 저장소(key-value store) 도구입니다 (예를 들어 자동 로그인, 여부, 토큰, 마지막으로 본 페이지, 설정값(다크모드 ON/OFF) 같은 것들)

내부적으로는 안드로이드의 SharedPreferences, iOS의 NSUserDefaults를 사용해 작은 데이터를 로컬에 저장합니다

데이터베이스 없이도 앱 종료 후에도 데이터를 유지할 수 있어, 설정 값, 사용자 선호, 앱 상태 등을 저장할 때 자주 사용합니다

웹에서는 localstorage랑 비슷하다고 볼 수 있습니다

### SharedPreferences에 저장할 수 있는 타입
SharedPreferences는 밑에 타입만 저장됩니다
- `int`
- `double`
- `bool`
- `String`
- `List<String>`

객체(Map, class)는 직접 저장 못함 -> JSON String으로 바꿔서 저장 해야함<br>
SharedPreferences는 원래 단순한 key-value 저장소라서 타입 지원이 제한되고 리스트도 예외적으로 문자열 리스트만 지원하는 구조입니다


그럼 바로 사용법으로 넘어가보죠

## 사용법

[pub.dev](https://pub.dev/packages/shared_preferences)
최신내용은 공식문서


먼저 사용하기 위해선 패키지를 설치 해줘야겠죠

### 패키지 설치
pubspec.yaml에 `dependencies:` 밑에 `shared_preferences:(^버전)` 코드 추가 후 console 에서 `flutter pub get` 입력해주면 설치는 끝입니다


### 기본 문법

### 1. 인스턴스 가져오기
```dart
final prefs = await SharedPreferences.getInstance();
```
### 2. 저장하기 (setX)
```dart
await prefs.setString('token', 'abc123');
await prefs.setBool('autoLogin', true);
await prefs.setInt('launchCount', 5);
await prefs.setStringList('recent', ['a','b']);
```

### 3. 불러오기 (getX)
```dart
final token = prefs.getString('token'); // 없으면 null
final autoLogin = prefs.getBool('autoLogin') ?? false // null이면 기본값 false
```

### 4. 삭제 / 전체 삭제
```dart
await prefs.remove('token'); // 특정 키 삭제
await prefs.clear();
```

SharedPreferences는 비동기라서 항상 await가 들어갑니다

비동기 방식을 사용하는 이유는 SharedPreferences는 파일 시스템에 접근하고 파일을 읽고 쓰는 작업에 시간이 걸립니다<br> 그래서 UI가 멈추지 않도록 Future(비동기) 방식으로 작동합니다<br> (await 키워드를 사용해서 저장/불러오기 작업이 끝날때까지 기다렸다가 다음 작업을 수행)

### 사용할 때 주의점
- 많은 양의 데이터를 저장하는 것은 적합하지 않습니다
- `int, double, bool, String, List<String>`만 가능
- 보안이 필요한 데이터는 사용 금지

## 앱 시작할때 초기화
자주 하는 실수: `main()`에서 `SharedPreferences` 쓰는데 `WidgetsFlutterBinding.ensureInitialized()` 안해줌
```dart
Future<void> main() async {
    WidgetsFlutterBinding.ensureInitialized();
    final prefs = await SharedPreferences.getInstance();

    final isLoggedIn = prefs.getBool('isLoggdIn') ?? false;
}
```
여기서 `WidgetsFlutterBinding.ensureInitialized()`를 왜 해줘야 하는지 궁금할수있는데요<br> `WidgetsFlutterBinding.ensureInitialized()`는 내부적으로 플러그인(네이티브:Android / iOS)을 호출해줍니다<br> 이 호출이 Platform Channel을 통해서 이루어지는데 그 채널을 쓰려면 Flutter 쪽에서 `바인딩(binding)`이 먼저 준비돼 있어야합니다

`runApp()`을 호출하면 Flutter가 보통 바인딩을 자동으로 초기화해주는데<br>
`runApp()` 이전에 `await SharedPreferences.getInstance()`를 해주게 되면??

네 안되겠죠

그래서 `main()`에서 이런 순서가 되면

1. 바인딩 준비 안됨
2. 플러그인 호출(SharedPreferences)해버림
3. `응 아직 초기화 안됐는데 플러그인 쓰지마~` 같은 에러가 날 수 있습니다

### 그럼 모든 곳에서 다 해줘야하나요?
아니요 `runApp` 이후에 SharedPreferences를 쓰면 보통 괜찮습니다<br>
ex.어떤 위젯의 `initState()` 안에서 `SharedPreferences.getInstance()` 호출하는 경우 (이미 runApp이 바인딩을 초기화했기 때문에)

`runApp` 전에 플러그인을 쓰고 싶을때만 `ensureInitialized()`는 필수에 가깝습니다


## 실전 예시) 자동 로그인 (로그인 유지)
### 로그인 성공시 저장
```dart
Future<void> saveLogin(String token) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool('isLoggedIn', true);
    await prefs.setString('token', token);
}
```

### 앱 시작시 분기
```dart
Future<void> isLoggedIn() async{
    final prefs = await SharedPreferences.getInstance();
    return prefs.getBool('isLoggedIn') ?? false;
}
```

### 로그아웃 시 삭제
```dart
Future<void> logout() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.remove('token');
    await prefs.setBool('isLoggedIn');
}
```


## 자주하는 실수
### 1. getX는 null일 수 있음
```dart
prefs.getBool('x') ?? false
```
기본값 처리 습관을 들이는걸 추천합니다

### 2. build() 안에서 계속 getInstance() 호출하지 말기
`build()`는 엄청 자주 호출돼서 느려집니다<br>
보통 `initState()`나 `FutureBuilder`에서 1번만 불러옵니다

### 3. SharedPreferences는 보안 저장소가 아님니다
토큰 / 비밀번호 같은 민감한 정보는 원칙적으로 flutter_secure_storage 같은걸 쓰는게 안전하답니다 (근데 대회/제한이 있는 곳에선 SharedPreferences 쓰는거 추천)