#### 💛 9강 정렬 - ORDER BY
* 실제 연습을 위해 지난 프로젝트였던 wattataxi2 DB를 가지고 연습!
* ORDER BY 구를 사용해서 검색결과의 행 순서를 바꿔보장!
* 정렬(sort) 방법을 공부할꾸~~
```
💛 select 열 from 테이블명 order by 열 💛
```
1) order by로 검색 결과 정렬하기
* tickets 테이블을 price 열을 기준으로 정렬하니 가격이 오름차순으로 정렬돼서 나옴!
```
💛 select * from tickets order by price asc; 💛
```
* 아무것도 지정안해줄 때 기본 값을 오름차순이라는 것을 기억해줭....!
![](https://images.velog.io/images/majaeh43/post/b4d17b2d-919e-49d4-9091-622659dc7819/image.png)

2) order by desc로 내림차순 정렬하기
```
select * from tickets order by price desc;
```
![](https://images.velog.io/images/majaeh43/post/5cff2401-a1ca-4b47-a1e8-13cee82875dd/image.png)

3) 대소관계
* 수치형 데이터라면 대소관계는 숫자의 크기로 판별. 날짜시간형 데이터도 숫자 크기로 판별. 최근 순일 수록 '크다', 과거로 갈 수록 '작다'라고 보면 됨!
* 문자열형 데이터의 대소관계는 사전식 순서에 의해 결정
ex) '나비'와 '가방', '가족'은 '가방'>'가족'>'나비' 순서임!
* 문자열형 열에 숫자를 저장하는 경우는 '문자'로 인식되니까 주의할 것!

4) order by는 테이블에 영향 안줌
* order by를 이용해 행 순서를 바꿀 수 있음. 하지만 이건 그냥 행순서를 단순히 바꿔 결과를 출력하는 것일 뿐 저장장치에 저장된 데이터의 행 순서를 바꾸는 건 아님! **단순 참조!**

#### 💛 10강 복수의 열을 지정해 정렬하기
* 위에서는 열 하나만 정해서 order by 했는데, 그럼 복수의 열도 지정해서 정렬이 가능할까?
```
💛 select 열명 from 테이블명 where 조건식 order by 열명1 [asc/desc], 열명2[asc/desc].. 💛
```
* 가능해! 근데 이럴 때, NULL값에 주의할 필요가 있음!

1) 복수 열로 정렬 지정
* price 기준으로 오름 or 내림차순으로 정렬을 해주었어도 나머지 열은 그렇지 않은 경우가 있음. 이런 경우 order by로 복수 열을 지정할 수 있음.
```
💛 select * from tickets order by price, seat_remain; 💛
```
![](https://images.velog.io/images/majaeh43/post/61e606f3-633f-41e2-b656-461c3fff2c68/image.png)
* price로 오름차순이 되어있는데 각 가격별로 seat_remain이 오름차순 정렬되어있는 것을 확인할 수 있다!
* 그럼 order by에서 열의 순서를 바꿔볼까? 위에서 order by a, b였다면 이번에는 order by b, a로!!
```
💛 select * from tickets order by seat_remain, price; 💛
```
![](https://images.velog.io/images/majaeh43/post/c33f5f99-5071-403c-989b-77b39274a8e4/image.png)
* 요렇게 바뀐당! 신기해...🍩
* 그렇다면 하나는 asc로 다른하나는 desc로 해볼까?
```
💛 select * from tickets order by price desc, seat_remain asc; 💛
```
![](https://images.velog.io/images/majaeh43/post/c80394ac-05cd-4702-95c5-70965f03136f/image.png)크크 신기하쥐....🐣

3) NULL 값의 정렬순서
* NULL 값은 그 특성상 대소비교를 할 수 없어 정렬 시에는 1. 특정 값보다 큰 값, 2. 특정 값보다 작은 값. 이렇게 두 가지로 나뉨.
* order by로 지정한 열에서 NULL 값을 가지는 행은 가장 먼저 표시되거나 가장 나중에 표시.
* **MySQL의 경우 NULL값을 가장 작은 값으로 취급**...! 그래서 asc에서는 가장 먼저, desc에서는 가장 나중에 표시!

#### 💛 11강 결과 행 제한하기 - LIMIT
* LIMIT구로 결과 행을 제한하는 방법?
```
💛 select 열명 from 테이블명 LIMIT 행수 [OFFSET 시작행] 💛
```
1. 행수 제한
* LIMIT구는 select 명령 마지막에 지정, where구나 order by 구 뒤에 지정.
```
💛 select 열명 from 테이블명 where 조건식 order by 열명 LIMIT 행수 💛
```
* 만약 LIMIT을 행수를 10으로 지정하면 최대 10개의 행이 반환! 고러면.. 연습해보장...!
* locations 테이블: 행이 13개인데, 이걸 5개만 추려보장!
![](https://images.velog.io/images/majaeh43/post/aa4d5640-f46b-4a6a-a813-69a74965ad2c/image.png)
* limit 사용해서 행 5개 추리기- 쨔란-!
![](https://images.velog.io/images/majaeh43/post/cca9b441-4d45-462a-ba14-6c4fd93ec9f5/image.png)

* 정렬한 후 제한하기
그렇다면 where id <= 5로 명령을 준거랑 limit = 5로 준거랑 뭐가 다른걸까?
-> limit은 반환할 행수를 제한하는 기능, where은 구로 검색한 후 order by로 정렬된 뒤 최종적으로 처리.(limit은 정렬 기능이 없으니까 정렬기능을 지정해줘야함!)

2. 오프셋 지정
* 웹 시스템에서는 페이지 단위로 화면에 표시할 내용을 처리. 🍄페이지 나누기🍄기능을 활용하는 것. -> 커뮤니티 사이트 등에서 게시판 하단 부분에 '1 2 3 4 5 다음' 등으로 표시된 것이 그 예시!
-> 이 페이지 나누기 기능은 limit을 통해 간단히 구현 가능!
ex. 한 페이지 당 5건의 데이터를 표시하도록 한다면, 첫 번째 페이지의 경우 limit 5로 결괏값을 표시하면 됨. 그 다음 페이지에서는 6번째 행부터 5건의 데이터를 표시하도록 하는거쥐. 이 때 '6번째 행부터'라는 표현은 결괏값으로부터 데이터를 취득할 위치를 가리키는 것으로 **limit구에 offset으로 지정 가능**!
```
💛 select * from locations limit 3 offset 0; 💛
```
![](https://images.velog.io/images/majaeh43/post/b4cbaa18-4c2d-43df-ab58-64974839bd01/image.png)
```
💛 select * from locations limit 3 offset 3; 💛
```
![](https://images.velog.io/images/majaeh43/post/38977f27-eab7-4f4a-bbd4-8a6fdef204a6/image.png)
```
💛 select * from locations limit 3 offset 6; 💛
```
![](https://images.velog.io/images/majaeh43/post/eac63432-2537-40a5-b6ca-f3ac25ff5cbf/image.png)

* 여기서 **offset은 그 숫자 다음부터 화면에 출력해준다는 뜻인 것 같음**.. 아직 쪼오금 감이 안옴..!🐤

#### 💛 12강 수치 연산
* SQL은 기본적으로 계산기능을 포함함. 수치의 연산 방법에 대해 공부를 해볼까...?🐤
```
💛 +-*/%MOD 💛
```
* % 대신 MOD함수를 사용하는 경우도 있음!

1. 연산자의 우선순위
우선순위 1번은 * /. 
우선순위 2번은 +-
* select 구나 where 구 안에서도 연산할 수 있음!

2. select 구로 연산하기
```
💛 select 식1, 식2... from 테이블명 💛
```
* 일단, ticket 테이블을 참고할거야.
![](https://images.velog.io/images/majaeh43/post/212868a2-b18b-49e1-be48-c2cd121ed2e9/image.png)
* 말도 안되지만 price와 seat_remain을 연산해보자.^^
* 계산식을 total = price * seat_remain으로 잡기. select구로 지정해서 계산 가능.
![](https://images.velog.io/images/majaeh43/post/a4bb3db9-47f9-41d6-9131-4614cf255a9d/image.png)

3. 열의 별명
* 계속 price * seat_remain 이렇게 쓰면 너무 길고 알아보기 힘드니까...! 별명을 지어줄까? 😇 total이라는 별명을 지어주장..!
```
💛 select *, price * seat_remain AS total from tickets; 💛
```
![](https://images.velog.io/images/majaeh43/post/fc9a5928-08fc-4d70-bddf-b58b65ef1b0c/image.png)
* 요런식으로 AS total을 넣어주면 별명을 만들어 줄 수 있찌~~~ 근데 AS도 생략가능!
* 단, 한글로 지정하는 경우에는 더블쿼트("")를 둘러싸서 지정해주기.(숫자는 안돼!)

4. WHERE 구에서 연산하기
* 아까 위에서 만든 total 값을 검색해보장!
```
💛 select price*seat_remain AS total from tickets where price*seat_remain >= 40000.000; 💛
```
![](https://images.velog.io/images/majaeh43/post/dfa8305c-f136-4aa8-b145-046c83497c70/image.png)

* 근데 왜 select total로 열이름을 안해준거니?...?
-> 왜냐면! select 명령을 실제로 실행해보면 total이란 열은 존재하지 않는다는 에러가 발생함 ^^
![](https://images.velog.io/images/majaeh43/post/becce554-eac9-4cc2-8ca1-01f33678343c/image.png)
-> where구에서의 행 선택, select 구에서의 열 선택은 **🐤 데이터베이스 서버 내부에서 where구 -> select구의 순서로 처리가 됨 🐤**.(신기해!넘중요!) 그래서 where구로 행이 조건에 일치하는지 아닌지 먼저 조사한 후에 select구에 지정된 열을 선택해 결과로 반환하는 식으로 처리.
-> 별명은 select 구문을 내부 처리할 때 붙여짐. 그니까 where구의 처리는 select구보다 선행되므로 wherer구에서 사용한 별칭은 아직 내부적으로 지정되지 않은 상태가 되니까 에러발생!

5. NULL 값의 연산
* NULL값은 연산이 안돼...😇
```
NULL + 1 = NULL
1 + NULL = NULL
1 + 2 * NULL = NULL
1 / NULL = NULL
```
* 얘네 다 모두우 NULL이야 ^^

6. ORDER BY 구에서 연산하기
* order by구에서도 연산가능하고 그 결괏값들을 정렬 가능! 내가 했던 total을 정렬 한 번 해볼까?.? 힣ㅎ...
```
💛 select price * seat_remain AS total from tickets order by total desc; 💛
```
![](https://images.velog.io/images/majaeh43/post/eb60ca00-e216-4d6b-83ea-cf6aee796fa6/image.png)
* order by는 서버에서 내부적으로 가장 나중에 처리됨. 그니까 select 구보다 나중에 처리되기 때문에 select 구에서 지정한 별명을 order by에서도 사용할 수 있는거쥐.
* 근데, where 구에서는 별명을 사용할 수 없어.... 왜냐면 서버에서 내부처리 순서가 있기 때문이지....🐼
## 🌱 where 구 -> select 구 -> order by 구 🌱

7. 함수
연산자 외에 함수를 사용해 연산도 가능해!
```
함수명(인수1, 인수2...)
```

8. round함수
* 소수점을 가지는 값이 있는 경우, 반올림을 위해 round함수를 사용함.
```
💛 select price*seat_remain, round(price*seat_remain) from tickets; 💛
```
![](https://images.velog.io/images/majaeh43/post/680a01b3-4d0b-4974-a229-8b8a78580e46/image.png)
* round함수는 integer형의 자료형을 decial 형의 자료형으로 바꿔주는 역할!(**decimal은 정수부와 소수부의 자릿수를 지정할 수 있는 자료형임!**)
```
💛 select price*seat_remain, round(price*seat_remain,1) from tickets; 💛
```
![](https://images.velog.io/images/majaeh43/post/d14c910b-2b43-4fa3-8679-058f2ce6643f/image.png) 요거슨 소수점 둘째자리에서 반올림한 것!

#### 💛 13강 문자열 연산
* 문자열형 연산 -> 문자열결합이란? 문자열 데이터를 결합하는 연산!
1. 문자열 결합
* MySQL에서는 CONCAT함수로 문자열을 결합함.
* seattypes 테이블로 연습을 해보장..!
![](https://images.velog.io/images/majaeh43/post/bfe2ee09-b894-4664-aed7-eb437e9c4beb/image.png)

* type열과 rate열을 합쳐보는 것이야!
![](https://images.velog.io/images/majaeh43/post/5b10c3a4-8fba-4740-b84d-ba1a31571e35/image.png) 신기해...🦖

2. substring 함수
* substring 함수는 문자열의 일부분을 계산해서 반환해주는 함수!
```
💛 substring('20140125001',1,4) -> '2014' # 여기서 1,4는 ''안에 있는 문자열에서 첫번째부터 4개를 뽑을거라는 말! 💛
```

3. Trim 함수
* 문자열의 앞뒤로 여분의 스페이스가 있을 경우 이를 제거해주는 함수. 근데 문자열 중간에 있는 공백은 제거 안돼. 고정길이 문자열 형에 대해 많이 사용하는 함수!
* 앞서 배운 것처럼 CHAR VS VARCHAR의 차이점은 CHAR은 최대길이가 주어지면 그걸 공백으로 채워서라도 다 사용하는 문자열형이고 VARCHAR은 최대길이가 주어져도 데이터 길이 만큼만 사용하는 문자열형이었어! (기억나니?...?)
* 이렇듯 CHAR형의 문자열형에서 문자열의 길이가 고정되고, 남은 공백을 없앨 때, 이렇게 TRIM 함수를 사용하는거지!
```
💛 Trim('ABC    ') -> 'ABC' 💛
```

4. Character_length 함수
* character_length함수는 문자열의 길이를 계산해 돌려주는 함수. 문자열의 길이는 **문자 단위로 계산**되어 수치로 반환됨. 줄여서 char_length로 사용가능.
* octet_length함수는 문자열의 길이를 **바이트 단위로 계산**해 돌려주는 함수.

* 문자세트(character set)
- 한 문자가 몇 바이트인지는 쓰이는 문자세트에 따라 다르다.-> 이게 왜 중요한데?
- char_length 함수를 사용하는 경우에는 아무런 문제가 되지 않아! (한글이든 ASCII문자이든 문자 단위로 계산되니까!) 그치만 octet_length함수의 경우 문자 수가 아닌 바이트 단위로 길이를 계산하기 때문에 주의할 필요가 있음! 

#### 💛 14강 날짜 연산
* 날짜 연산?
```
💛 current_timestamp current_date interval 💛
```
1. SQL에서의 날짜
* 날짜나 시간 데이터는 수치 데이터와 같이 사칙 연산 가능. 날짜시간 데이터를 연산하면! 결괏값으로 동일한 날짜시간 유형의 데이터를 반환하는 경우도 있으며 기간의 차를 나타내는 기간형(interval) 데이터를 반환하는 경우도 있음! 
* 시스템 날짜: RDBMS에서도 시스템 날짜와 시간을 확인하는 함수를 제공함.
* 'Current_timestamp'라는 긴 이름의 함수로 실행했을 때를 기준으로 시간을 표시. 인수 필요없뜸!
```
💛 select current_timestamp; 💛
```
![](https://images.velog.io/images/majaeh43/post/342f0da8-9e7a-4370-affe-816ddcac528f/image.png) 신긔하즤...? 🦕 ㅎㅎ

* 날짜 서식
임의의 날짜를 저장하고 싶을 경우에는 직접 날짜 데이터를 지정해야함.
어떻게?
```
2021/08/14
2021-08-14
14 Aug 2021
```

2. 날짜의 덧셈과 뺄셈
* 날짜시간형 데이터는 기간형 수치데이터와 덧셈 및 뺄셈을 할 수 있음. 날짜시간형 데이터에 기간형 수치데이터를 더하거나 빼면 날짜시간형 데이터가 반환됨.
```
💛 select current_date + interval 1 day; 💛
# current_date는 시스템 날짜의 날짜만 확인하는 함수. interval 1 day는 '1일 후'라는 의미의 기간형 상수.
```
![](https://images.velog.io/images/majaeh43/post/15164425-d2ad-4379-a7b0-f282ad90c57f/image.png)

* 일주일을 더해줘볼까?
```
💛 select current_date + interval 7 day; 💛 
```
![](https://images.velog.io/images/majaeh43/post/9935555a-27ab-4526-8e7e-26aae4b69b31/image.png) 따란~!

* 그럼 날짜형 간의 뺼셈도 가능?
날짜시간형 데이터 간에 뺼셈 가능! datediff 함수를 쓰면 뺀 '기간'이 나옴!
```
💛 select datediff('2021-08-14', '2021-01-01'); 💛
```
![](https://images.velog.io/images/majaeh43/post/fba2710a-e5e0-455a-a919-98793c6c36af/image.png)

#### 💛 15강 CASE 문으로 데이터 변환하기
1. case문
* RDBMS에서는 사용자가 함수를 작성할 수 있음! 어떻게? **CASE 문을 활용해서!**
```
💛 case when 조건식 then 식1      #1
   	[when 조건식2 then 식2...]   #2
   	[else 식3]                 #3
   end 💛
```
* #1 먼저 when 절에는 참과 거짓을 반환하는 조건식을 기술함! 참이면 then 뒤의 식이 처리됨.
* #1 when 절의 조건식을 차례로 평가해 나가다가 가장 먼저 조건을 만족한 when 절과 대응하는 then절 식의 처리결과를 case 문의 결괏값으로 반환.
* #2 그 어떤 조건식도 만족하지 못한 경우에는 else 절에 기술한 식이 채택됨. (else는 생략가능하고 생략할 경우에는 'else null'로 간주됨.

* 그렇다면...😇 **NULL값을 0으로 반환하는 case식 구현사례**를 살펴볼까...?^^
```
💛 select address, case when address IS NULL then 0 else address end "address(null=0)" from orders; 💛
```
* ![](https://images.velog.io/images/majaeh43/post/11f05e00-be5b-403d-ab33-86226ee70039/image.png) NULL값이 0으로 바뀌었따! 
 
* 🪓 **근데 다시 select 구문을 쳐보면 NULL 값은 여전히 NULL 값이다. 이건 어쩔 수 없는 것일까? 궁금..**
![](https://images.velog.io/images/majaeh43/post/03b977bd-b368-4074-b9f1-d11b8fa3a7a2/image.png)

* COALESCE
요기서 NULL값을 변환하는 경우라면 COALESCE 함수를 사용하는 편이 더 쉽다고 한다^^
```
💛 select address, coalesce(address,0) from orders; 💛
# address가 null이 아니면 address값을 그대로 출력, 그렇지 않으면(address가 null이면 0 출력!)
```
* 🪓 **근데 이것도 마찬가지로... NULL값은 여전히 NULL 값이다. 아예 바꿀 수는 없는 거신가!!!**
![](https://images.velog.io/images/majaeh43/post/7d3da761-b753-41ea-be01-050839b02cf5/image.png)

2. 또 하나의 CASE 문
* 숫자로 이루어진 코드를 알아보기 더 쉽게 문자열로 변환하고 싶은 경우 case문을 많이 사용함.
* 예를 들어, '남자는 1, 여자는 2'라는 코드 체계가 있다면 1,2라고 설명하는 것보다 남자/여자 라고 표시하는게 더 이해가 쉽겠지. 이렇게 **🌱'문자화'하는 것을 '디코드'**라고 부르고 반대로 수치화 하는 것을 '인코드'라고 부름!🌱

```
when a = 1 then '남자'
when a = 2 then '여자'
```

* case문에는 '검색case'와 '단순case'의 두 개 구문으로 나눌 수 있음!
- 검색case: 'case when 조건식 then 식...' 구문
- 단순case: 'case 식 when 식 then 식...' 구문 <- 요기는 case뒤에 먼저 식을 기술함!
```
case 식1
	when 식2 then 식3
    [when 식4 then 식5...]
    [else 식6]
end
```
* 이걸 적용해보장...!
* 검색 case
```
select address AS "코드",
case
	when address = 1 then '남자'
    when address = 2 then '여자'
    else '미지정'
end as '성별' from orders;
```
![](https://images.velog.io/images/majaeh43/post/ed365023-c87a-4bb9-a0dc-d03b0505633c/image.png)
* 단순 case
```
select address AS "코드",
case address		  # case 뒤에는 대상을 적기
	when 1 then '남자' # when 뒤에는 값만 적기
    when 2 then '여자' # 요기도 마찬가지
    else '미지정'
end as '성별' from orders;
```
![](https://images.velog.io/images/majaeh43/post/aa0c3db9-8fee-48fc-9fad-b2b9c2c86582/image.png)

3. CASE를 사용할 경우 주의 사항
* else 생략
else를 생략하면 else null이 되는 것에 주의해야함. 대응하는 when이 하나도 없으면 else 절이 사용됨. 이때 else를 생략하면 상정한 것 이외의 데이터가 왔을 때 Null이 반환됨. 따라서 else를 생략하지 않고 지정하는 편이 나음. **-> case 문의 else는 생략하지 않는 편이 낫다는 말...!**
* when에 Null 지정하기
```
case address
	when '대구 어딘가' then '남자'
    when '서울 어딘가' then '여자'
    when NULL then '데이터 없음'
    else '미지정'
end
```
이럴때는 1. address = '대구 어딘가', 2. address = '서울 어딘가', 3. address = NULL 이 순서로 처리됨! 요때 중요한 것은 2가지! 
❣️ NULL 값인지 아닌지 판정하기 위해서는 **IS NULL**을 사용함. 
❣️ NULL 값인지를 판정하려면 검색 CASE문을 사용해야함. (왜냐면 단순 CASE문은 특성상 = 연산자로 비교하니까!) 밑에 참조!
```
case
	when '대구 어딘가' then '남자'
    when '서울 어딘가' then '여자'
    when address IS NULL then '데이터 없음'
    else '미지정'
end
```
**-> 단순 case문으로는 NULL 값 비교 불가!**

🍩 3장 뒷부분 case문 다시 한 번 복씁하기...🍩 힘!
