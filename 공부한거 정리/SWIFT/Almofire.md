2025.06.20

Alamofire는 Swift로 만든 HTTP 네트워크 통신 라이브러리입니다

복잡한 URLSession 코드를 더 간단하게 만들어주죠

### Alamofire 설치

Swift Package Manager (Xcode 메뉴에서)
- File → Add Packages...
- URL: https://github.com/Alamofire/Alamofire


## 기본 GET 요청
예시)
```swift
import Alamofire

AF.request("https://jsonplaceholder.typicode.com/posts/1").response { response in
    if let data = response.data {
        print(String(data: data, encoding: .utf8)!)
    }
}
```

## JSON 디코딩
예시)
```swift
struct Post: Decodable {
    let userId: Int
    let id: Int
    let title: String
    let body: String
}

AF.request("https://jsonplaceholder.typicode.com/posts/1")
    .responseDecodable(of: Post.self) { response in
        switch response.result {
        case .success(let post):
            print("제목: \(post.title)")
        case .failure(let error):
            print("에러: \(error)")
        }
    }
```

## POST 요청 (body 담기)
예시)
```swift
let parameters: [String: Any] = [
    "title": "foo",
    "body": "bar",
    "userId": 1
]

AF.request(
    "https://jsonplaceholder.typicode.com/posts",
    method: .post,
    parameters: parameters,
    encoding: JSONEncoding.default
).response { response in
    debugPrint(response)
}
```

## 헤더 추가하기
예시)
```swift
let headers: HTTPHeaders = [
    "Authorization": "Bearer YOUR_TOKEN",
    "Accept": "application/json"
]

AF.request("https://api.example.com/user", headers: headers)
    .responseJSON { response in
        print(response)
    }
```
## 파일 업로드
예시)
```swift
AF.upload(multipartFormData: { multipartFormData in
    multipartFormData.append(Data("value".utf8), withName: "param")
    multipartFormData.append(yourImageData, withName: "file", fileName: "image.jpg", mimeType: "image/jpeg")
}, to: "https://example.com/upload")
.response { response in
    debugPrint(response)
}
```

## 응답 코드/데이터 확인
예시)
```swift
AF.request("https://api.example.com/data")
    .response { response in
        if let statusCode = response.response?.statusCode {
            print("응답 코드: \(statusCode)")
        }
        if let data = response.data {
            print("응답 데이터: \(String(data: data, encoding: .utf8)!)")
        }
    }
```

## 에러 처리
예시)
```swift
AF.request("https://api.example.com/data")
    .validate(statusCode: 200..<300) // 200~299만 성공
    .responseDecodable(of: MyModel.self) { response in
        switch response.result {
        case .success(let data):
            print(data)
        case .failure(let error):
            print("실패: \(error.localizedDescription)")
        }
    }
```