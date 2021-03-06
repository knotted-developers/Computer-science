## 🐤 1. 기본 용어 정리
> 🕸 **웹 서버**
- 웹 브라우저 같은 클라이언트로부터 HTTP 요청을 받아 정적인 웹 페이지를 클라이언트로 보내주는 서버.
- 요청에 필요한 페이지의 로직이나 데이터베이스와의 연동을 위해서 어플리케이션 서버에 이들의 처리를 요청함.
- 대표적으로 Apache, nginx IIS등이 있음.

> 🕸 **웹 브라우저**
- 웹 서버로부터 받은 HTML 문서, 이미지 등을 화면에 표현해주는 소프트웨어.
- 대표적으로 익스플로러, 크롬 등이 있음. 이 브라우저들은 각각의 방식으로 HTML 문서를 해석하고 화면에 나타냄.

> 🕸 **웹 어플리케이션 서버(WAS)**
- HTTP를 통해 컴퓨터나 장치에 어플리케이션을 수행해주는 미들웨어(솝트웨어 엔진)!
- 웹을 기반으로 실행되는 프로그램(웹서버+웹컨테이너).
- 동적인 페이지 처리를 담당함.
- 요청한 페이지의 로직이나 데이터베이스와의 연동을 처리하는 부분.
- 대표적으로 톰캣, WebLogic, WebSphere, iPlanet 등이 있음.

> 🕸 **웹 서버와 웹 어플리케이션 서버의 차이??**
- 웹 서버는 정적 데이터를 처리하고 웹 어플리케이션 서버는 동적 데이터를 처리한다.
- 이 특징으로 실무에서는 이 둘을 연동해서 사용, WAS는 동적 처리에 최적화 되어 있는 서비스이기 때문에 처리 속도를 위해 정적처리는 웹서버, 동적 컨텐츠는 WAS에서 처리.
- 웹 어플리케이션 서버를 사용함으로써 서버에 부담 줄일 수 있고 동적 컨텐츠의 처리 속도가 빨라짐!

![](https://images.velog.io/images/majaeh43/post/f26791b4-fe2a-4028-a18b-7d78fa35fc01/image.png)
> 🕸 **데이터베이스**
- 데이터 정보를 저장하는 곳.

## 🐤 2. 전체적인 웹 동작 방식
![](https://images.velog.io/images/majaeh43/post/2007debb-06cf-41c4-96b9-26cd15993966/image.png)
* 기본적으로 클라이언트 - 서버 방식으로 이루어짐.
* 클라이언트(웹브라우저)가 특정 페이지를 웹 서버에 요청(Request)하게 되면 웹 서버가 이를 처리한 후 결과를 클라이언트(웹브라우저)에게 응답(Response)을 하게 되는 구조.

![](https://images.velog.io/images/majaeh43/post/d8d31acf-356e-4333-9982-d44571e48c2b/image.png)

**🕷 1,2 **사용자가 웹 브라우저를 통해 찾고 싶은 웹 페이지의 URL 주소를 입력.
**🕷 3** 사용자가 입력한 URL 주소 중에서 도메인 네임(domain name) 부분을 DNS 서버에서 검색.

🕸 DNS(Domain Name System)는 인터넷 전화번호부. 사용자가 nytimes.com 또는 espn.com과 같은 도메인 이름을 입력하면, DNS에서 해당 IP주소(컴터 친화적인)를 찾아쥼.

**🕷 4** DNS 서버에서 해당 도메인 네임에 해당하는 IP주소를 찾아 사용자가 입력한 URL 정보와 함께 전달.

**🕷 5, 6** 웹페이지 URL 정보와 전달받은 IP 주소는 HTTP 프로토콜을 사용해 HTTP 요청메시지 생성. 이렇게 생성된 HTTP 요청 메시지는 TCP 프로토콜을 사용해 인터넷을 거쳐 해당 IP 주소의 컴퓨터로 전송.

🕸 IP는 데이터 조각들을 **최대한 빨리 보내는 역할**을 한다.
🕸 TCP는 대용량의 데이터를 보내기 쉽게 작게 분해하여 상대에게 보내고, **정확하게 도착했는지 확인하는 역할**을 한다. 도착한 조각들을 점검하고 하자가 있으면 다시 요청한다.

**🕷 7** 이렇게 도착한 HTTP 요청메시지는 HTTP 프로토콜을 사용하여 웹페이지 URL 정보로 변환됨
**🕷 8** 웹서버는 도착한 웹페이지 URL 정보에 해당하는 데이터를 검색함.

**🕷 9,10** 검색된 웹 페이지 데이터는 또 다시 HTTP 프로토콜을 사용해 HTTP 응답 메시지를 생성. 이렇게 생성된 HTTP 응답 메시지는 TCP 프로토콜을 사용해 인터넷을 거쳐 원래 컴터로 전송.

**🕷 11** 도착한 HTTP 응답 메시지는 HTTP 프로토콜을 사용해 웹페이지 데이터로 변환됨.
**🕷 12** 변환된 웹 페이지 데이터는 웹 브라우저에 의해 출력되어 사용자가 볼 수 있음.

## 🐤 3. HTTP 프로토콜
🕸 **HTTP ?** (HyperText Transfer Protocol)
- 인터넷상에서 데이터를 주고받기 위한 서버-클라이언트 모델을 따르는 프로토콜.
- OSI 7계층의 어플리케이션 레밸의 프로토콜로 TCP/IP 위에서 작동.
- 우리가 웹 브라우저를 통해 페이지들을 볼 수 있게 해쥼.

🕸 **구조**
- 서버-클라이언트 모델
- 일반적으로 클라이언트는 서버에서 요청(Request)하고, 서버는 그 요청에 대한 응답(Response)을 돌려줌.
- 요청을 할 때에는 URL로 요청.
- 사용자가 웹 페이지의 링크 클릭-> 브라우저는 http 형태로 메시지를 작성해서 웹 서버에 전송.
- 웹 서버에서는 받은 메시지에 대해 HTTP 응답 형태로 메시지를 작성해 브라우저에 보내면, 브라우저는 이를 해석해 화면에 보여주게 됨.
- HTTP 동작 방식은 TCP 3-Way-Hanshake 과정으로 브라우저와 웹 서버 간 Connection이 이루어지고, 이후 브라우저의 요청에 의한 웹 서버의 응답이 이루어짐.

🕸 **HTTP 특찡**
- 비연결(Connectionless)&비상태(Stateless) 프로토콜
비연결: 클라이언트의 요청에 응답한 후 바로 연결을 끊음
비상태: 서버의 상태가 어떤지 간에 상관없이 요청을 함
- 장점: 불특정 다수를 대상으로 하는 서비스에 적합. 많은 유저의 요청을 처리 할 수 있음!
- 단점: 연결을 끊어버리니까 클라이언트의 이전 상태를 알 수 없음.
ex.인터넷에 로긴하면, 쿠키나 세션의 방식이 없다면 로긴을 한 정보가 바로 사라짐! 그래서 서버와 계속해서 통신이 필요한 경우에는 Ajax나 Web Socket 등의 특수한 방법들을 사용함. 혹은 cookie를 이용해 이 문제를 해결!

🕸 **HTTP 메시지 구조**
- Header + Body로 나누어짐
- Header: 주소 정보, 어떤 메서드 방식을 썼는지, 클라이언트 정보, 브라우저 정보, 접속 URL 등의 정보를 담음.
- Body: 보통 비어있다가 필요시 데이터 정보가 포함.
![](https://images.velog.io/images/majaeh43/post/2128e3ff-b880-4a0d-874f-12f782df1975/image.png)

🕸 **HTTP Method**
![](https://images.velog.io/images/majaeh43/post/0b03185a-1d65-40e1-8c7a-0dde2a37f11e/image.png)

🕸 **HTTP GET&POST**
> 🕷 GET
- 데이터에 대한 인수를 URL에 포함하여 전송
- URL 뒤에 ? 마크를 통해 URL의 끝을 알리고, Key-Value의 쌍으로 인수 앞에 & 을 붙여서 구분하고 글자수는 255자로 제한.
* google.co.kr/? <- 요기까지가 URL이고 뒤로부터는 키-밸류 쌍.
* 본문에 있어야할 값이 ? <- 요거 뒤에 다 나오기때문에 헤더에 값이 따로 필요가 없음.
* 
![](https://images.velog.io/images/majaeh43/post/dab750c5-fd2c-4ea3-a914-aa5e86cb963e/image.png)
**- URL에 포함되기 때문에 HTTP 패킷의 헤더에 포함되어 서버에 요청!
**- 그래서 GET 요청할 때 HTTP 패킷의 바디는 비어있다!!🤗🤗
- 요청 후에는 **멱등성**을 가지며, 조작 대상의 자원의 상태를 변화시키지 않아 안정적임.

😯 **근데 멱등성이 무엇?**
연산을 여러번 적용하더라도 결과가 달라지지 않는 성질. 그러니까 해당 메소드로 동일한 요청을 서버에 여러번 호출한 효과가 한번만 요청한 효과와 동일하면 '멱등성'.
- GET은 캐시가 되는 특징이 있음 !(멱등이기 때문에!)

😯 **캐시는?**
한번 접근 후, 또 요청할 시 빠르게 접근하기 위해 데이터를 저장시켜 놓는 것! 
**(GET (O), POST (X))**

> 🕷 POST
- URL에 요청 데이터를 기록하지 않고 데이터를 HTTP 바디에 넣어 전송.
- 내부의 구분자가 각 파라미터를 구별하여 서버가 해석하기때문에 속도가 GET에 비해 느림.
- 데이터 전송에 대한 제한이 없으므로 글 쓰는 것 같은 많은 양의 데이터를 전송할 수 있음.

> 🕷 GET&POST
- Get은 서버에서 어떤 데이터를 가져와서 보여줄 때 사용함. 주로 조회할 때 사용.
- 즉 서버의 어떤 값이나 내용, 상태 등을 바꾸지 않는 경우에 사용.
- POST는 서버의 값이나 상태를 바꾸기 위해서 사용함.
- DB에 저장/수정 시 DB의 값이 변경되게 하는 경우에 사용됨.

🤔 면접 질문?
**🕷 POST 방식이 GET방식보다 보안 측면에서 더 좋을까?**
- POST든 GET이든 보내는 데이터는 전부 클라이언트측에서 볼 수 있음. 단지 GET방식은 URL에 데이터가 표시되어 별다른 노력없이 볼 수 있음. 두 방식 전부 보안을 생각한다면 암호화해야함.

**🕷 GET방식이 POST방식보다 속도가 빠른가?**
- 빠름. GET방식의 요청은 캐싱때문에 빠른 것. POST는 캐싱기능이 없어...^^





🕸 출처: https://m.blog.naver.com/jh_p0415/221360954467

🕸 참고: https://binux.tistory.com/32
