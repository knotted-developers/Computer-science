> **웹서버 조감도**

- `이미지 보기 토글 클릭`

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c86452d9-e654-4e74-9f7d-45e2aa4e927c/webserver_.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c86452d9-e654-4e74-9f7d-45e2aa4e927c/webserver_.png)

> **CGI란 무엇일까?**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/035d1964-cf57-4b69-b172-02f9eb8e5591/cgi_single.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/035d1964-cf57-4b69-b172-02f9eb8e5591/cgi_single.png)

1. CGI (Common Gateway Interface)
외부 어플리케이션과(Python 등) 웹서버(nginx, Apache 등)를 연결할 때 사용하는 표준화된 프로토콜이다. 과거에는 정적 HTML 파일로 웹서버를 구동하였기 때문에 CGI의 개념이 필요 없었지만, 웹서버가 처리할 수 없는 정보를 주고 받아야하는 경우가 점점 생겨남에 따라서 외부 어플리케이션이 이 기능을 해줄 수 있게 웹서버와 어플리케이션의 중개역할을 한다.

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ae7520e0-976e-4b1a-9ac6-9ea1973a771c/cgi_multi.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ae7520e0-976e-4b1a-9ac6-9ea1973a771c/cgi_multi.png)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/865c3f9a-4ed4-42a7-86ac-96601b2ee4da/fast_cgi.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/865c3f9a-4ed4-42a7-86ac-96601b2ee4da/fast_cgi.png)

2. FastCGI
다수의 클라이언트가 요청했을시 위 1번 이미지처럼 다수의 사용자가 동시 요청을 하게 되면 매번 새로운 프로세를 생성하고 삭제 해야한다. 이는 성능 저하를 유발(오버헤드 상승)하기도 한다.  REST API를 사용하는 현대의 웹서비스에서, 즉 요청과 응답이 수시로 반복 처리 되는 환경에서 이러한 구조는 적합하지 않다. 이를 보완하고자 만든 것이  FastCGI 이다. 다수의 요청이 들어와도 하나의 프로세스만을으로 해당 요청들을 처리하고, 메모리에 단 하나의 프로그램만을 만들어 계속 재활용하기 때문에 CGI에 비해 오버헤드(어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리 등을 말한다.)가 월등히 감소한다.

> **WSGI란 무엇일까?: "Python에서 운용가능한 CGI 확장판"**

- Python으로 선택할 수 있는 웹 프레임워크에서 사용할 수 있는 기존 웹서버는 CGI, FastCGI, mod_python, 또는 커스텀으로 만들어진 API 등으로 상당히 제한되어 있었다. 또 반대로 웹서버를 선택하는 것이 파이썬 웹개발환경을 제한하기도 하였다. 이러한 제한점을 극하기 위해 개발 된 것이 WSGI이다.
- WSGI는 한 프로세스에서 모든 요청을 받는다는 점에서, 매 요청마다 프로세를 생성하는 CGI와는 다르고, 한 프로세스를 사용하는  FastCGI의 장점을 계승했다고 볼 수 있다.
- **WSGI의 역할:** 웹 서버가 어플리케이션의 코드를 직접 읽을 수 없기 때문에, 어플리케이션의 코드를 읽고 결과를 대신 반환하는 (웹 서버와 어플리케이션을 사이를 이어주는) 매개체가 필요해지는데, WSGI가 이러한 미들웨어 기능을 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b8d7881-9be9-498d-9e6c-5982c1c966bc/wsgi.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b8d7881-9be9-498d-9e6c-5982c1c966bc/wsgi.png)

- **미들웨어란?:    
- h**ttp 요청 / 응답 처리 중간에서 작동하는 시스템이다
**-** DJango는 http 요청이 들어오면 미들웨어를 거쳐서 해당 URL에 등록되어 있는 뷰로 연결해주고, http 응답 역시 미들웨어를 거쳐서 내보낸다

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43a9b0f5-6cbd-49e5-9915-155844055a16/middleware2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43a9b0f5-6cbd-49e5-9915-155844055a16/middleware2.png)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1390ec4-755d-467d-a07c-987cec4da537/middleware.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1390ec4-755d-467d-a07c-987cec4da537/middleware.png)
