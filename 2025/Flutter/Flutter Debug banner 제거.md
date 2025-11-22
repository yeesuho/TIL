2025.11.23

플러터 빌드나 디버깅시에는 우측 상단에 디버그 배너가 표시되는데요
<br>
저는 보기에 안예쁘니까 없애줍니다

아래처럼 return 머리티얼앱 바로 밑에 `debugShowCheckedModeBanner: false` 코드삽입후 저장시 디버그 배너가 표시되지 않습니다

debug만 쳐도 자동완성이 되네요

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      debugShowCheckedModeBanner: false, // 디버그 배너삭제
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
```