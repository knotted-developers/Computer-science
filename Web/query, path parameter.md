## ⚽️ Path Vaiable & Query Parameter

### 1) Query string

/users?id=123 
위에서 보는 것처럼 ? 뒤에 id란 변수에 값을 담아 백엔드에 전달하는 방식이 Query string이다. users에 담긴 정보 중 id 123번의 자료를 달라는 요청이다.

### 2) Path Variable

/users/123
위와 동일한 요청을 경로를 지정하여 요청할 수도 있는데 이것을 Path Variable이라고 한다.


### 3) Query string과 Path variable은 각각 언제 쓰면 좋은가?

일반적으로 우리가 어떤 자원(데이터)의 위치를 특정해서 보여줘야 할 경우 Path variable을 쓰고, 정렬하거나 필터해서 보여줘야 할 경우에 Query parameter를 쓴다. 아래가 바로 그렇게 적용한 사례이다.

위의 방식으로 우리는 어디에 어떤 데이터(명사)를 요청하는 것인지 명확하게 정의할 수 있다. 하지만, 그 데이터를 가지고 뭘 하자는 것인지 동사는 빠져있다. 그 동사 역할을 하는 것이 GET, POST, PUT, DELETE 메소드이다.

즉, Query string과 Path variable이 이들 메소드와 결합함으로써 "특정 데이터"에 대한 CRUD 프로세스를 추가의 엔드포인트 없이 완결 지울 수 있게 되는 것이다.
(가령, users/create 혹은 users?action=create를 굳이 명시해 줄 필요가 없다.)

```
/users [GET] # Fetch a list of users
/users [POST] # Create new user
/users/123 [PUT] # Update user
/users/123 [DELETE] # remove user
```

## ⚽️ Code & Test
### 1) Query string

[views.py]

```
class CategoryView(View):
	def get(self, request):
		category = request.GET.get('category_id', None)
```
View 클래스에서 위와 같이 작성하면 category_id란 값을 가져올 수 있다.

테스트를 위해 httpie에서 http -v url category_id==4를 입력하면, 장고의 request.GET에서는 <QueryDict: {'category_id': 4}가 들어가게 되고, request 헤더에 엔드포인트 url로 /product?category=4가 찍히게 된다.

만약 테스트를 포스트맨을 통해서 한다면, 파라미터 탭에 키와 밸류를 넣어주면 된다.

### 2) Path variable

[views.py]

```
class ProductView(View):
	def get(self, request, product_id):
		product = Product.objects.filter(id=product_id).values()
```
[urls.py]

```
urlpatterns = [
    path('product/<int:product_id>', ProductView.as_view())
]
```
Path variable는 뷰클래스 함수에서 self, request 외에 별도의 인자를 가지게 되고, 그 인자값이 엔드포인트가 된다. 따라서 path variable은 인자값이 확실하게 부여가 되는 경우(특정 상품의 정보 등)에 주로 사용되며, urls파일에 반드시 반영을 해 줘야 된다.

테스트를 할 때는 간단하게 url에 해당되는 path variable을 추가해 주면 된다. httpie에서는 http -v url/product/4로 하면 된다.

## ⚽️ CONFUNDIDO 헷갈리는 곳!!

### 1) 헷갈린 부분1
 
🏀 **GET 메소드**
클라이언트의 데이터를 URL에 붙여서 보낸다. 위에서 예를 들었던 것 처럼 아이디와 패스워드를 보냈다고 생각하면

```
www.velog.com?id=velog&pass=1234
```
이렇게 보내게된다. URL뒤에 ? 마크를 통해 URL의 끝을 알리면서 데이터 표현의 시작점을 알린다. **데이터는 key와 value 쌍으로 넣어야한다.** 위 예시로 보면 key는 id와 pass 이고, value는 velog와 1234 이다. 중간 & 는 구분자이다. 2개 이상의 key-value 쌍 데이터를 보낼 때 & 마크로 구분하게된다.

URL에 붙이므로 🍒**HTTP 패킷의 헤더에 포함되어 서버에 요청**🍒을 보내게된다. 그래서 🍒**GET 메소드로 요청을 보낼때는 HTTP패킷의 BODY가 빈 상태**🍒로 보내지게된다. 그러므로, 헤더의 내용 중 BODY데이터를 설명하는 Content-Type 이라는 헤더필드도 들어가지 않는다.

URL 형태로 표현되므로, 특정 페이지를 다른 사람에게 접속하게 할 수 있고, 간단한 데이터를 넣도록 설계되어서 데이터를 보내는 양의 한계가 존재한다.

🏀 **POST 메소드**
POST 방식은 GET방식가 달리 **데이터 전송을 기반으로 한 요청 메소드**이다. GET 방식은 URL에 데이터를 붙여서 보내는 반면, POST 방식은 URL이 아니라 **BODY에 데이터를 넣어서 보내게된다.** 따라서 헤더필드중 BODY의 데이터를 설명하는 Content-Type 이라는 헤더필드가 들어가고 어떤 데이터 타입인지 명시해야한다.
Content-Type 으로는 여러가지가 있지만 대표적으로

```
1. application/x-www-form-urlencoded
2. text/plain
3. multipart/form-data
```
등이 있다.
따라서 POST 방식으로 데이터를 보낼때는 위와 같이 Content-Type 을 꼭 명시해줘야한다.

보통 작성하지 않으면 1번으로 셋팅되는데, GET 방식과 마찬가지로 BODY에 key-value 쌍으로 데이터를 넣는다. 구분자는 똑같이 &이다.
2번은 BODY에 단순 txt를 넣는다.
3번은 파일전송 할 때 많이 쓰는데, BODY의 데이터를 바이너리 데이터로 넣는다는 걸 알려준다.

🏀 포인트!
![](https://images.velog.io/images/majaeh43/post/8d810f33-4cac-4a18-96c4-f7699a031a1f/image.png)

* 요청 라인의 메서드 값이 'POST'로 지정되어 있음.
Content-Length: 22
Content-Type: application/x-www-form-urlencoded
Content-Length : 보내는 데이터의 길이를 알려주는 헤더
Content-Type : 보내는 데이터의 형식을 알려주는 헤더
application/x-www-form-urlencoded : form 태그의 입력값의 기본 인코딩 형식

* 서버에 보내는 데이터는 🍉**공백 라인 다음에 '메시지 본문(Message Body)'라고 불리는 부분에 위치**🍉함

![](https://images.velog.io/images/majaeh43/post/36c319b3-24bb-4821-884b-6ca591608eda/image.png)
### 2) 헷갈린 부분2
> **request.GET vs request.GET.get()**
request.GET은 GET으로 받는 파라미터들을 다 포함하는 딕셔너리 객체이다.
get() 메서드는 key 값이 딕셔너리 안에있으면 value값을 리턴해준다. 키 값이 존재하지 않으면 디폴트값인 None을 리턴한다.
request.GET.get()은 위 두 개념을 합친것으로 GET 요청이 접근할 수 있는 key와 value 값을 이용한다.

### 3) 헷갈린 부분3
🥅 GET - 쿼리스트링으로 요청이 왔을 시 처리방법
백엔드에서 받는 방법은?
예를 들어서
```
http://localhost:8000/example?sort_by=price-ascending
```
라는 형식의 주소가 있다면, key값이 sort_by이며 value값에 price-ascending 를 넣어서 example 이라는 엔드포인트에 요청을 보낸것이다.

여기서 중요한 점은 장고 기능으로 인해 query parameter의 key와 value는 request의 GET 객체로 쿼리 딕셔너리로 담겨서 들어온다는 점이다.

#views.py
```
class ExamView(View):
	def get(self, request):
    	sort_by = request.GET.get('sort_by', None)
        data = Exam.objects.get(sort=sort_by)
        
        return JsonResponse(...)
```
그러므로 위와같이 request의 GET객체에서 get메소드를 이용해서 key 값인 sort_by에 해당하는 value를 갖고오면 된다. 없으면 None을 갖고와서 에러를 줄여주자.
그리고서 데이터베이스에서 필요한 데이터를 갖고와서 가공해준 뒤 반환해주면 된다.

🥅 GET - Path parameter (url parameter)
요청이 쿼리스트링이 아니라 Path parameter(url parameter)로 들어올수도 있다.
백엔드에서 특정 endpoint를 지정하지 않고, 프론트엔드가 보내는 특정 string이나 int를 path안의 parameter로 받아 view로 보내는 방식이다.

```
urlpatterns = [
    path('/<str:target_code>', AreaView.as_view())
]
```
당연히 위에 처럼 urls 파일에도 반영해줘야한다.

```
class AreaView(View):
    def get(self, request, target_code=''):
```
view 클래스 함수에서 self와 request외에 다른 인자를 갖게되며 처리해줘야한다. 그 인자값이 endpoint가 된다.

url parameter는 인자가 없으면 안되고, 인자값으로 확실한 구분이 가능한 경우에 주로 사용한다. 그에 반해 query parameter는 여러개의 조건이 결합될 때 주로 사용한다.

🥅 POST - JSON 으로 요청이 왔을 시 처리방법
이번에는 POST 메소드로 요청이 왔을 시에는 어떻게 처리하는지 알아보자.
위에서도 알아봤지만 보통 POST 메소드는 HTTP의 BODY에 내용을 담아서 요청(request)을 보낸다.

아래와 같이 프론트엔드에서 바디에 json 객체 형태로 요청(request)를 보내게된다. 여기서 주의할 점은 프론트와 백엔드가 같이 데이터를 어떤식으로 보내고 어떤 식으로 받을지 잘 소통해야된다는 것이다. 객체로 보낼지, 리스트로 보낼 지, 키 값을 어떻게 보낼지 등 소통이 굉장히 중요하다.

```
{
	"user_id": "test1",
	"password": "qwer1234!",
	"name": "test",
	"birth_date": "2020-05-01",
	"phone": "010-0000-0000",
	"email": "test@naver.com"
}
```
위와같이 json 형식으로 요청이 들어왔다고 생각하고 진행할 것이다.

🥅 json 형식?
JSON 형식을 자바스크립트의 객체와 마찬가지로 key:value 가 존재할 수 있음, key값이 문자열이면 항상 쌍따옴표를 이용하여 표기해야한다.
객체나 배열 등의 표기를 사용할 수 있다. ({key:value} / [30,40])
또한 null, number, string, array, object, boolean 을 사용할 수 있다.
백엔드는 그럼 저 json 형식의 request를 어떻게 처리해야할까?

#views.py

```
data = json.loads(request.body)
```
위 코드의 의미는 request의 바디에 담겨서 오는 내용이 json 형식이면, json 형식의 string을 python dictionary 형식으로 변경해서 data라는 변수에 저장해줘 라는 의미이다.

```
data = json.loads(request.body)
            if len(data.keys()) < 6:
                return HttpResponse(status=400)
            for value in data.values():
                if value in "":
                    return HttpResponse(status=400)
```
위 코드는 그룹프로젝트 중에 회원가입 코드의 일부분이다.
변수에 저장한 뒤 data의 key 수가 6개 이하면 에러코드를, 그리고 value에 빈값이 들어왔다면 에러코드를 보내준다는 의미이다.
회원가입 시 필수사항이 6개이기에 혹시라도 그 이하의 값이 들어오거나, 아예 아무런 값도 넣지 않았을 때 에러코드를 반환한다는 의미이다.


🥅 참고: https://velog.io/@jcinsh/Query-string-path-variable
🥅 참고: https://velog.io/@magnoliarfsit/ReDjango-3.-GET-POST-메소드-차이점-및-api-설계

