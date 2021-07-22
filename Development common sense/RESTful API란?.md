> REST API가 무엇인가요? (단답 서술형)

- 추후 완성 예정..

> REST API는 누가 왜 발명했지?

- REST는 Representational State Transfer라는 용어의 약자로서 2000년도에 로이 필딩 (Roy Fielding)의 박사학위 논문에서 최초로 소개되었다. 로이 필딩은 HTTP의 주요 저자 중 한 사람으로 그 당시 웹(HTTP) 설계의 우수성에 비해 제대로 사용되어지지 못하는 모습에 안타까워하며 웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표하였다.

> REST의 3대 구성은**?**

- 자원(Resource) - URI
- 행위 (Verb) - HTTP METHOD
- 표현(Representation) - 주고받는 데이터 내용

> REST의 특징은?

1) Uniform (유니폼 인터페이스)

Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말함.

2) Stateless (무상태성)

REST는 무상태성 성격을 갖는다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해진다.

3) Cacheable (캐시 가능)

REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. 따라서 HTTP가 가진 캐싱 기능이 적용 가능하다.

4) Self-descriptiveness (자체 표현 구조)

REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 점이다.

5) Client - Server 구조

REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어든다.

6) 계층형 구조

REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 된다.

> **REST API 디자인시 유념해야할 점은?**

**첫 번째,**

URI는 정보의 자원을 표현해야 한다.

**두 번째,**

자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

### REST API 중심 규칙

---

### 1) URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용)

```
https://www.notion.so/HaMin-Kim-b5d1f5a1c8bb44baabb55def086b911dhttps://www.notion.so/HaMin-Kim-b5d1f5a1c8bb44baabb55def086b911d    GET /members/delete/1

```

위와 같은 방식은 REST를 제대로 적용하지 않은 URI입니다. URI는 자원을 표현하는데 중점을 두어야 합니다. delete와 같은 행위에 대한 표현이 들어가면 안된다!

### 2) 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

위의 잘못 된 URI를 HTTP Method를 통해 수정해 보면

```
    DELETE /members/1

```

으로 수정할 수 있겠습니다.회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현한다.

**회원정보를 가져오는 URI**

```
    GET /members/show/1     (x)
    GET /members/1          (o)

```

**회원을 추가할 때**

```
    GET /members/insert/2 (x)  - GET 메서드는 리소스 생성에 맞지 않습니다.
    POST /members/2       (o)

```

[[참고]HTTP METHOD의 알맞은 역할](https://www.notion.so/f1c0c9b5d3c14471b40feb570845c68e)

### URI 설계 시 주의할 점

---

### 1) 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

```
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales

```

### 2) URI 마지막 문자로 슬래시(/) 미포함

URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

```
    http://restapi.example.com/houses/apartments/ (X)
    http://restapi.example.com/houses/apartments  (0)

```

### 3) 하이픈(-)은 URI 가독성을 높인다.

URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있음.

### 4) 밑줄(_)은 URI에 사용하지 않는다.

글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려진다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋다.(가독성)

### 5) URI 경로에는 소문자가 적합하다.

URI 경로에 대문자 사용은 피하도록 해야 합니다. 대소문자에 따라 다른 리소스로 인식하기 때문...

```
    RFC 3986 is the URI (Unified Resource Identifier) Syntax document

```

### 6) 파일 확장자는 URI에 포함시키지 않는다.

```
    http://restapi.example.com/members/soccer/345/photo.jpg (X)

```

REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다. Accept header를 사용하여 이를 해결해야함.

```
    GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```
