`김경래`

---

**`HTTP란?:`**
HTTP는 하이퍼 텍스트 전송 프로토콜의(Hypertext Transfer Protocol)의 약자이다. 서로 다른 시스템들 사이에서 통신을 주고받게 해주는 가장 기초적인 프로토콜이다. 웹 서핑을 할 때 서버에서 브라우저로 데이터를 전송해 주는 용도로 가장 많이 사용됩니다. 그리고 인터넷의 초기에 모든 웹사이트에서 기본적으로 사용된 프로토콜이다.

**`HTTPS란?:`**
HTTPS는 하이퍼 텍스트 전송 프로토콜 보안(Hypertext Transfer Protocol Secure)의 약자이다. 일반 HTTP 프로토콜의 문제점은 서버에서부터 브라우저로 전송되는 정보가 암호화되지 않았다는 점인데, 데이터가 쉽게 도난에 취약했다. HTTPS 프로토콜은 SSL(Secure Socket Layer/ 보안 소켓 계층)을 사용함으로써 이 문제를 해결했다. SSL은 서버와 브라우저 사이의 연결 암호화를 돕고, 서버 브라우저가 민감한 정보를 주고받을 때 도난을 미연에 방지한다.

**`둘의 개념을 가르는 SSL의 역할은?`**

‘HTTP vs HTTPS 차이’는 바로 이 SSL 인증서의 유무이다. **SSL 인증서는 사용자가 사이트에 제공하는 정보를 암호화하는데, 쉽게 말해서 데이터를 암호로 바꾸는 개념이다. 이렇게 전송된 데이터는 중간에서 누군가 훔쳐 낸다고 하더라도 데이터가 암호화되어있어 해독이 불가하다.** 

요새는 SSL의 업그레이드 버전인 TLS를 더 많이 사용한다. TLS는 데이터 무결성을 제공하기 때문에 데이터 전송 중간 과정에서 데이터가 변형/손실되는 것을 막고, 사용자가 의도한 웹사이트와 통신 중이라는 것을 입증하는 인증 기능도 추가되어있다. 

**`HTTPS를 사용하는 또 다른 장점은?`**

1) **HTTPS를 사용하게 되면 보안외적으로도 검색엔진최적화(SEO)에 유리하다**. 만약 웹사이트에 전자상거래 기능도 없고 방문자들의 민감한 정보를 다루지도 않는다면 보안성을 향상시켜야하는 것에 필요를 느끼지 않을 수 있다 . 하지만 HTTPS로 전환하게 되면 구글이 HTTPS 웹사이트에 가산점을 주어 검색 결과로 더 잘 노출 되는 혜택을 누릴 수 있고, 또 사용자들로 하여금 더 보안 안전성을 느끼게 할 수 있어 검색 및 실제 사이트 사용에 유리한 고지를 점할 수 있다.

2) **또한 가속화된 모바일 페이지(AMP, Accelerated Mobile Pages)를 만들고 싶을 때도 HTTPS 프로토콜을 사용해 한다.** 여기서 AMP란 모바일 기기에서 훨씬 빠르게 콘텐츠를 로딩 하기 위한 방법으로 구글이 만든 것. AMP는 HTML에서 불필요한 부분을 생략한 페이지다. 구글의 SERP(검색 결과 페이지)를 보면 스마트폰과 태블릿의 사용자들이 모바일에서 사용하기 편하도록 AMP 콘텐츠들이 많다는 것을 알 수 있다.

모바일 친화적인 웹사이트를 만드는 것과 모바일 검색순위 및 지역에 SEO를 증가 시킨 HTTP를 HTTPS로 전환하는 것이 필수라고 볼 수 있다.

**`서버와 클라이언트의 연결 원리는?`**

- **1. 지원 가능한 알고리즘 서로 교환**
- **2. 키 교환 및 인증**
- **3. 대칭키 암호로 암호화하고 메시지 인증**

![](https://github.com/knotted-developers/Computer-science/blob/main/Wen/Images/http.png)

이미지 출처: [https://raonctf.com/essential/study/web/ssl_tls](https://raonctf.com/essential/study/web/ssl_tls)

**`SSL/TLS Handshake 개념`**

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/http2.png)

**`HTTP Request vs HTTPs Request  생김새 차이`**

**http 요청 내용** vs **암호화된 https 요청 내용**

아래 해쉬된 내용 확인!

![](https://github.com/knotted-developers/Computer-science/blob/main/Web/Images/http3.png)
