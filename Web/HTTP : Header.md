`양미화`
<br>

<h1> HTTP : Header </h1>

<h3> 💡 HTTP란? </h3>

- HyperText Transfer Protocol
- 하이퍼텍스트(HTML) 문서를 교환하기 위해 만들어진 통신 규약(protocol)

<h3> 🔍 HTTP 통신 방식 </h3>

![](https://images.velog.io/images/hwaya2828/post/8e7778cf-12d7-46e0-a69b-f3022bf2d473/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-07-26%20%EC%98%A4%ED%9B%84%2012.29.11.png)

- HTTP는 기본적으로 **요청(request)•응답(response) 구조**로 이루어짐
    - 클라이언트가 HTTP request를 서버에 보내면 서버는 HTTP response를 보내는 구조
    - 클라이언트와 서버의 모든 통신이 요청과 응답으로 이루어짐
    
![](https://images.velog.io/images/hwaya2828/post/842a5736-22fc-427d-97fe-3d55a59fff78/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-07-26%20%EC%98%A4%ED%9B%84%2012.29.28.png)

- **Stateless**
    - Stateless란 말그대로 state(상태)를 저장하지 않는다는 뜻
        - 각각의 요청•응답은 독립적인 요청•응답
        - 클라이언트가 요청을 보내고 서버의 응답을 받은 후 다시 요청을 보낼 때, 이전의 요청•응답에 대해 알지 못한다는 뜻
        

<h3> 🎩 HTTP : Header </h3>

- 클라이언트가 서버로 요청을 할 때 혹은 서버가 클라이언트에 응답할 때 **부가적인 정보를 담는 곳이 헤더(header)**라는 곳
-파이썬(Python)의 딕셔너리(Dictionary)와 비슷하게 **키와 값이 쌍을 이루는 값**으로 이루어져 있음
    - 예를 들어 키에는 Content-Type 라는 키와 값에는 application/json 등이 오는데 이 둘을 콜론으로 구분
    - 최종적으로는 `Content-Type: application/json` 형식으로 이루어짐
    

- 헤더는 문맥에 따라 종류를 나눌 수 있음
    - 대표적으로 요청과 응답에 모두 실어나를 수 있는 **General Header**가 존재
    - 클라이언트 자체 정보 등을 담는 **Request Header **
    - 서버의 자체 정보 등을 담는 **Response Header**
    - 컨텐츠 길이 혹은 MIME 타입에 관한 정보를 담는 **Entity Header**

> <span style="color:plum;"> __Tip!__ </span> **MIME**이란?
Multipurpose Internet Mail Extensions의 약자로 간단히 말하면 **파일 변환을 의미**한다.현재는 웹을 통해 여러 형태의 파일을 전달하는데 사용하고 있지만 이 용어가 생길 땐 이메일과 함께 동봉할 파일을 텍스트 문자로 전환해서 이메일 시스템을 통해 전달하기 위해 개발되어 Internet Mail Extensions라고 불리기 시작했다고 한다.


<h3> 📔 General Header </h3>

- **HTTP 공통 헤더**라고도 불림
- HTTP 통신을 하는 서버와 클라이언트 측에서 모두 사용할 수 있는 헤더를 말함
- 이 공통 헤더는 일반적인 목적으로 사용되며 **가장 기본적인 정보** 등을 담는 헤더들이 존재


- **Date**
    - HTTP 메세지를 생성한 일시를 뜻함
    - 키는 Date로 사용되며 `Date: Wed, 20 May 2020 02:44:49 GMT` 형식으로 이루어짐


- **Connection**
    - HTTP 통신이 완료된 후에 네트워크 접속을 유지할지 말지를 결정하는 헤더
    - 값으로는 close와 keep-alive 두 가지가 존재
    - close의 경우 통신이 완료된 후에 바로 연결을 끊겠다는 의미로, HTTP/1.0에서는 이 값이 기본 값
    - keep-alive의 경우에는 연결을 열린 상태로 유지하는 것을 나타내며, HTTP/1.1에서의 기본 값


- **Cache-control**
   - 서버와 클라이언트 요청 응답간의 캐싱 매커니즘을 위해 정의하는 헤더
   - 키:값으로 이루어진 헤더에서 **'값'을 '디렉티브'라는 명칭**으로 사용
   - 이 디렉티브에는 매우 다양한 값이 올 수 있으며 주로 쓰이는 것 몇 가지만 정리
       - _max-age=[seconds]_ : 리소스가 최신 상태라고 판다할 최대 시간을 지정하는 디렉티브, 요청 시간과 관련이 있음
       - _no-store_ : 어떠한 요청과 응답에 대한 정보를 캐시하지 않음
       - _no-transform_ : 응답에 대해 변형이나 변환이 일어나면 안됨. 컨텐츠의 헤더는 프록시에 의해 수정되면 안된다고 명시하고 이를 허용하지 않음
       - _no-cache_ : 캐시된 복사본을 보여주기 전에 재검증을 위한 요청을 서버로 보내도록 강제함
       - _public_ : 응답은 어떠한 캐시에 의해서든 캐시될 수 있음
       - _private_ : 응답은 공유 캐시에 의해 저장되지 않아야 함
       

<h3> 📔 Entity Header </h3>

- 주로 **컨텐츠의 정보를 담기 위한 헤더**
- Content- 로 시작하는 헤더 키들이 존재


- **Content-Type**
    - 응답하는 컨텐츠가 어떤 유형인지 알려주는 헤더
    - 디렉티브에는 media-type, charset, boundary 등이 존재
        - media-type이란 말 그대로 컨텐츠의 유형을 MIME Type으로 작성하면 되며, 주로 사용되는 application/json, text/html, font/woff, image/jpeg, image/png, video/mp4 등이 있음
    

- **Content-Length**
    - 바이트 단위의 컨텐츠 길이를 보냄


- **Content-Location**
    - 컨텐츠의 대체 위치를 가리킴
    - 이 위치는 상대적인 주소가 될 수도 있으며 절대적인 주소가 될 수도 있음 (리다이렉션의 대상을 가리키는 Location 헤더와는 다름) 
    - `Content-Location: https://example.com/index.html` 형식으로 사용


- **Content-Range**
    - 컨텐츠의 부분 위치를 알려줌
    - 예를 들어 총 67800bytes 크기를 가지는 컨텐츠를 부분적으로 보낸다면 `Content-Range: bytes 100-1000/67800`로 표현
        - "이 헤더는 응답으로 내보낸 컨텐츠가 총 컨텐츠 길이는 67800bytes이고, 그 중 100bytes에서 1000bytes까지의 컨텐츠이다." 라고 의미의 헤더


<h3> 📔 Request Header </h3>

- 요청에 실리는 헤더들
- 주로 클라이언트의 자체 정보를 담는 것들이 존재


- **Host**
    - 요청을 하는 주체에 대한 정보를 담는 헤더
    - HTTP/1.1 이후 이 헤더는 필수 항목
    - `Host: developers.facebook.com` 형식으로 사용


- **User-Agent**
    - 클라이언트의 정보를 담고 있음
    - 여기에는 브라우저 엔진, 버전, 운영체제 등이 담길 수 있음
    - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0` 형식으로 사용


- **Accept**
    - 클라이언트가 어떤 컨텐츠 타입을 이해할 수 있는지에 대한 정보를 담는 헤더
    - MIME 타입으로 작성할 수 있으며 서버는 이 헤더를 참고해서 적절하게 응답할 수 있음 
    - Accept 헤더로 클라이언트가 이해할 수 있는 컨텐츠 타입을 나열하고, 서버는 그 중 하나를 선택해 Content-Type 헤더에 컨텐츠 타입을 내보냄


- **Accept-Language**
    - 다국어를 지원해야 하는 서비스를 운영하고 있을 경우 도메인을 다르게 해 각국의 언어로 작성된 페이지를 보여줄 수 있는데, 이런 방법을 사용하지 않는다면 클라이언트가 서버에게 직접 이해할 수 있는 언어를 헤더에 실어서 보낼 수 있음
    - `Accept-Language: ko-KR, ko;q=0.5` 형식으로 사용


- **Accept-Encoding**
    - 요청해서 응답 받을 데이터의 압축 방식을 지정하는 헤더


- <span style="color:tomato;">**Authorization**</span>
    - 주로 인증 토큰을 보낼 때 쓰는 헤더
    - 다양한 언어에서 구현된 JWT 라이브러리로 만들어진 토큰을 이 헤더에 실어서 서버에 보낼 수 있으며, 주로 `Authorization: Type Token` 형식으로 사용
    - 일반적으로는 Type에 Bearer를 쓰고 Token에 Access Token을 담아서 서버에 보내면, 서버는 이러한 토큰을 받아 검증하고 검증된 토큰이면 자원을 내보내고 그렇지 않다면 적절한 응답을 할 수 있음


- **Referer**
    - 이 헤더는 현재 요청된 페이지에서 이전에 방문한, 현재 페이지가 어디로부터 들어오게 되었는지 표시하는 헤더
    - 다양한 애널리틱스 서비스에서는 이러한 헤더를 통해 사이트가 어디로부터 유입되었는지 정보를 얻어냄


<h3> 📔 Response Header </h3>

- 서버 자체의 정보를 담는 헤더, 컨텐츠에 대한 정보를 담을 수도 있음


- **Server**
    - 기본적인 서버의 정보를 담는 헤더
    - 너무 많은 서버의 정보를 담게 되면 공격을 받을 수 있으므로 세부적으로 작성하는 건 피해야함
    - 요청을 처리하는 서버 측이 어떠한 소프트웨어를 사용하고 있는지 혹은 하위 제품에 대한 내용을 담고 있음
    - `server: Netlify` 형식으로 사용


- <span style="color:tomato;">**Access-Control-Allow-Origin**</span>
    - 해당 Origin(주소)으로부터 오는 요청을 허용한다는 정보를 알려주는 헤더
    - `access-control-allow-origin: *` 형식으로 사용
        - 와일드 카드 *가 오게되면 모든 Origin을 허용한다는 의미
        - 그렇지 않고 Origin을 적게 되면 그 Origin으로 오는 요청만 허용한다는 의미
    - 만약 허용되는 Origin이 아닌 다른 곳에서 요청이 오게 된다면 브라우저에서 **CORS 오류**를 냄

> <span style="color:plum;"> __Tip!__ </span> **CORS**란?
Cross-Origin Resource Sharing의 약자로 **추가적인 HTTP header를 사용해서 애플리케이션이 다른 origin의 리소스에 접근할 수 있도록 하는 메커니즘**을 뜻한다. 다른 origin에서 내 리소스에 함부로 접근하지 못하게 하기 위해 사용된다.

- **Expires**
    - 리소스가 지정된 일시까지 유효하다고 나타내는 헤더
    - 캐시와 관련이 있으며 리소스에 대한 캐시가 언제 만료되는지를 알려주는 헤더


- **ETag**
    - HTTP 컨텐츠가 바뀌었는지에 대한 검증을 할 수 있는 태그
    - 응답 본문이 변하지 않는다면 항상 똑같은 값을 내뱉고 변한다면 다른 값을 내뱉기 때문에 이로 인해 컨텐츠가 바뀌었는지 검증이 가능하며 만약 바뀌게 된다면 캐시를 지우고 새로 내려받게 됨
    


