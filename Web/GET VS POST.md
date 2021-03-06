`정운산`

</br>

 **사용목적에 따라 쓰임이 다르다 GET은 서버의 리소스를 요청할 떄 POST는 서버의 리소스를 변경할 떄 사용한다**
 **GET은 파라미터를 통해 전송이 되기 때문에 Body안에 데이터가 없지만 POST는 Body를 통해 전송이 된다**

</br>

> GET

- 쿼리 파라미터로 전송
- url의 길이제한이 있어서 테이터를 전송하는 것에 대해 한계가 있다
- 퍼머링크(permalink) 존재
- 보안성에 문제(파라미터에 변수의 키와 값이 보여짐)
- 캐싱이 가능하다

Cache : 웹 자원에 낭비를 줄이기 위해 웹 헤더에서 받아서 서버의 리소스를 복사본을 만든다

HTTP 헤더에서 cache-control 헤더를 통해 캐시 옵션을 지정할 수 있다

</br>

> POST

- Header안에 Body가 담겨져서 전송(body 의 타입은 Content-Type 헤더에 따라 결정 된다)
- 데이터 전송에 한계가 없다
- 퍼머링크가 존재하지 않는다
- GET에 비하여 보안성이 좋다(차이는 크게 없음)

</br>

`추가 조사`

**쿠키  vs 스토리지**

> 쿠키 : 서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각

- 암호화가 불가능해 보안적인 부분에서 취약하다
- 서버와 클라이언트에 저장
- 용량이 작다 최대 (4Kb)
- 모든 브라우저에서 사용가능
- 매번 요청할 때마다 포함이 된다(Header로 전송)
- 브라우저가 종료되면 삭제된다 (만료일자 설정가능)

쿠키는 보통 세션과 함께 사용이 된다

세션 : 세션은 쿠키와 달리 브라우저에서 관리하지 않고 서버에서 저장된다

세션 ID(서버가 클라이언트에게 부여하는 ID)를 저장해서 브라우저가 종료될 때까지 인증상태 유지

사용자의 정보를 서버에서 두기 때문에 쿠키만으로 사용할 때와 달리 보안성에 좋다 하지만 사용자가 많아질수록 서버의 부담이 커진다

</br>

> 스토리지 : 웹 브라우저의 임시 저장소

- 클라이언트에 저장
- 용량이 크다 5Mb
- HTML5를 지원하는 브라우저에서 사용가능
