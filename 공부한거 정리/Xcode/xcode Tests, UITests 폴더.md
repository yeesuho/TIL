2025.06.11

Tests랑 UITests 폴더는 각각<br>
단위 테스트(Unit Tests)와 UI 테스트(User Interface Tests)를 작성하는 공간입니다

여기서 단위 테스트란<br>
앱이나 프로그램의 가장 작은 조각(함수, 메서드, 클래스 등)이 제대로 작동하는지 검사하는 테스트

### Tests 폴더 (앱이름Tests)
- 무엇을 위한 폴더인가요

  - 앱의 로직, 즉 함수나 모델, 컨트롤러 등이 제대로 동작하는지 확인하는 테스트 코드를 넣는 폴더

- 어떤 테스트를 하냐면

  - 예를 들어 계산기 앱이라면 add(2, 3) 함수가 진짜 5를 반환하는지 테스트하는 코드

  - 데이터 저장 로직, 네트워크 응답 처리 등도 여기서 테스트할 수 있음
```swift
func testAdd() {
    let result = add(2, 3)
    XCTAssertEqual(result, 5)
}
```

### UITests 폴더 (앱이름UITests)
- 무엇을 위한 폴더인가요

  - 앱의 **화면(UI)** 이 실제로 사용자처럼 작동하는지 확인하는 테스트를 넣는 곳

- 어떤 테스트를 하냐면

  - 버튼을 누르면 화면이 전환되는지?

  - 텍스트 필드에 입력하면 레이블이 바뀌는지?

  - 전체적인 사용자 흐름(예: 로그인 -> 다음 화면 이동)이 잘 되는지?
```swift
func testLoginButton() {
    let app = XCUIApplication()
    app.launch()
    
    let loginButton = app.buttons["Login"]
    loginButton.tap()
    
    XCTAssert(app.staticTexts["Welcome"].exists)
}
```

필요 없으면 삭제해도 앱 실행은 잘 되지만, 앱을 테스트하고 안정적으로 유지보수하고 싶을 때 매우 유용한 폴더들입니다

처음엔 안 써도 되지만 프로젝트가 커지면 배우는 게 좋다고 하네요