2025.12.17

### withOpacity is deprecated in Flutter 3.27.0 update

- flutter 3.27.9 업데이트로 withOpacity를 이제 사용할 수 없다고 합니다
- 공식 문서에 따르면 이전에는 Color 클래스에 opacity 개념이 있어서 `opacity`와 `withOpacity()` 메서드로 나타났고 Opacity는 Color alpha 채널을 부동 소수점 값으로 조정하기 위해 도입된 개념이었다고 합니다
- 이제 alpha 값 자체가 부동 소수점 값으로 처리되면서 opacity는 불필요하게 되었고 이에 따라 opacity와 withOpacity 메서드는 더 이상 사용되지 않으며 제거될 예정이라고 하네요

## 변경 전
```dart
final x = color.withOpacity(0.55);
```

<br>

## 변경 후
```dart
final x = color.withValues(alpha: 0.55);
```

<br>

# 결론
### withOpacity -> withValue로 수정요