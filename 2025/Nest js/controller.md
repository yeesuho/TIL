2025.04.20

# Controller 란
컨트롤러는 들어오는 요청을 처리하고 클라이언트에 응답을 반환합니다<br>
더 정확하게 말하면 사용자의 요청을 받고 그에 맞는 **핸들러 함수(메서드)** 로 연결해주는 클래스

![img](/img/Nestjs%20Controllers.png)
사진에서 보면 Client에서 Http Request를 주면 알맞은 Controller를 반환 하는거죠<br> 예를 들어 사용자면 user 컨트롤러 게시판이면 board 컨트롤러 이런식

컨트롤러는 ``@Controller`` 데코레이터로 클래스를 데코레이션하여 정의 됩니다<br>
board 컨트롤러면 ``@Controller('/boards')``<br>
user면 ``@ontroller('/user')``


<br>

### 쉽게 말하면
컨트롤러는 문지기 같음 <br>
누군가 주소(URL)를 두드리면<br>
컨트롤러가 "어떤 함수로 보내야 할지" 정해줍니다

