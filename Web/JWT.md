`박은혜`

## 🍋 면접 질문용 🍋

1. **JWT란 무엇인가?** 

Access token을 생성하는 방법 중 가장 널리 사용되는 기술 중 하나가 바로 JWT(JSON Web Tokens)이다. JWT는 말 그대로 json 데이터를 token으로 변환하는 방식이다.

1. **JWT를 사용한 경험이 있는가, 사용했다면 왜 사용했는가?**

1차 프로젝트에서 사용한 경험이 있다. `수많은 프로그래밍 언어에서 지원`되고, `필요한 모든 정보를 자체적으로` 지니고 있다. (ex. 토큰 기본정보, 전달할 내용, 유저정보 등) 또한, `두 객체 사이에서 쉽게 전달` 될 수 있다(ex. http 헤더에 넣어서 전달 가능, url 파라미터로 전달 가능)는 장점때문에 JWT를 사용했다.

(🍇 JW에 대한 장점을 먼저 말해주고 사용했던 경험이 있다고 말해주기 - 장점은 하단에 적어둠)

1. **보안에 취약하다는 단점이 있는데 어떻게 생각하는가? 대처방안도 함께 말해주세요.**

🍑 첫번째) 실제로 JWT가 보안에 완벽한 것은 아니다. 누군가가 토큰을 탈취한다면, 그 토큰을 이용하여 권한을 수행할수 있기때문이다. `사용 중인 Access Token의 만료시간을 줄여주어야한다.` 언제 토큰 만료 시간을 늘려줄 지는 각각 비즈니스 로직에 따라 구현해야 한다. access token의 시간을 줄여준만큼 다른 보조적인 방법이 동원되어야하는데, 그중 하나가 refresh token을 사용하는 것입니다.

 보통 20 ~ 30분 정도인 access token을 만료 시간으로 설정한다. 이 시간 동안만 토큰을 유지하고 Access Token 이 만료되면 Refresh Token 으로 다시 Access Token 을 발급 받아서 로그인 한다. 이 과정에서는 사용자가 별도로 로그인 절차가 없게 된다. Refresh Token 은 보통 한달 정도로 만료 시간을 설정하고 db에 저장되기 때문에 서버쪽에서 제어가 가능하다.

🍑 세션.....? 

**(추가설명)**

1. 클라이언트가 서버로 로그인 한다. (ID, PW)
2. 서버에서 사용자를 확인하고 `Access Token` 과 `Refresh Token` 을 함께 전송한다. `Access Token` 과 `Refresh Token` 모두 DB에 저장 한다.
3. 클라이언트는 `Refresh Token` 는 (로컬 스토리지에) 저장하고 `Access Token` 을 사용하여 서버로 로그인 한다.
4. 서버는 토큰을 검증하여 요청에 응답한다.
5. 만약 `Access Token` 이 만료가 된 경우면 서버에는 Unauthorized 응답을 준다.
6. 서버로 부터 Unauthorized 응답을 받으면 `Refresh Token` 으로 `Access Token` 을 재발급 한다.
7. `Refresh Token` 이 만료 되었다면 클라이언트에게 다시 로그인 할 수 있도록 응답해야 한다. 기존 `Access Token` 과 `Refresh Token` 을 비우고 다시 로그인 하게 해야 한다.
8. 로그아웃을 누르면 `Refresh Token` 으로 `Access Token` 을 모두 제거한다.

1. **JWT의 작동 방법을 알고있는가?**

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/jwt.png)

1. client가 서버에 http요청(로그인)하면, 
2. 유저정보 확인 후 서버의 secret key를 활용해 jwt를 생성 및 발행
3. 프론트에서 jwt를 브라우저(로컬 스토리지)에 저장하고
4. jwt를 포함한 http를 요청(헤더에 담아서)
5. 백에서 jwt의 signature 부분을 확인 후, 해당 유저의 정보를 가져온다
6. 확인 후 유저의 정보가 일치하면!!
7. payload부분에 담아서 http 응답! 완료~!

1. **JWT은 어떻게 만들어지는가?**

파이썬에서는 PyJWT 라이브러리를 사용해서 구현할 수 있다. JWT를 생성하고 복화하도 할 수 있게 해주는 라이브러리이다.  JWT는 `header, payload, signature` 세 부분으로 구성되어 있다.

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/jwt2.png)

서버는 토큰 안에 들어있는 정보가 무엇인지 아는게 중요한게 아니라 `해당 토큰이 유효한지 확인하는 것이 중요`하기 때문에 클라이언트로부터 받은 JWT의 헤더, 페이로드를 서버의 key값을 이용해 시그니처를 다시 만들고 이를 비교해 일치할 경우 인증을 통과 시킨다.

- **추가로 읽어보면 좋을 것**

🫐 **과거의 통신 방법**

HTTP는 Stateless , Connectionless 특징이 있기 때문에, 사용자 인증을 유지할 수 있는 기능이 필요함. 그래서 클라이언트가 로그인 등으로 한 번 사용자 인증을 하면, 그 인증을 유지할 수 있도록 **쿠키**와 **세션**이라는 기술을 지금껏 사용해 왔음. 그러나 **쿠키**는 브라우저에 사용자 정보가 기록되기 때문에 위변조의 가능성이 높아 보안에 취약하며, **세션** 또한 서버의 메모리를 차지하고 있기 때문에 동접자가 많은 웹 사이트일 경우 서버 과부화의 원인이 되며, 또한 세션 정보가 중간에 탈취 당할 수 있기 때문에 보안에 완벽하다고 할 수가 없다. 또한, client 하나에 서버가 여러개있는 경우, 각자 메모리에 저장하기 때문에 서버끼리 공유가 안된다. 메모리를 다 따로 관리해주어야하는 단점이 있다. **`쿠키와 세션의 문제점 및 다양한 단점들을 보완하기 위해 토큰(Token)기반의 인증 방식이 도입되었음.`**

🫐 **그럼 JWT는?**

서버가 여러개라고 하더라도(100개라고 하더라도) 서버는 secret key만 알고 있으면 JWT 시그니처만 검증해주면 된다. `**각 해당 서버에서 똑같은 secret key를 공유**`하면되니까! 그럼 계속 똑같은 값을 확인할 수 있기때문에 따로 관리해줄 필요가 없음.

🫐 **JWT 장점**

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/jwt3.png)

🫐 **JWT 단점**

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/jwt4.png)

## 🥑 참고: [JWT 공식 사이트](https://jwt.io/introduction)
