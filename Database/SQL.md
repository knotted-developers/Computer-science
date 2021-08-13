
* select 명령은 '질의'나 '쿼리'라 불리기도 함.
* select 명령을 실행하면 표 형식의 데이터가 출력됨. 행(레코드)과 열(컬럼/필드)

#### 💙 6강 검색 조건 지정하기
* 데이터 검색에는 열을 지정하는 방법과 행을 지정하는 방법이 있따!
* 열은 오른쪽으로 쭈욱 된 것, 행은 밑으로 쭈욱 된 것!
* 열을 선택할 때는 **select구**를 사용, 행을 선택할 때는 **where구**를 사용!
```
💙 select 열1, 열2 from 테이블명 where 조건식; 💙
```
* tickets tables을 가지고 연습을 할것임!
![](https://images.velog.io/images/majaeh43/post/dc3a1e26-649f-4db6-87f9-0536a2e9bf07/image.png)

1) select 명령을 통해 두가지 열만 가져와보장!(price 열과 taxi_company_id열!)
![](https://images.velog.io/images/majaeh43/post/a735d5a7-0fc8-4c9b-9936-f6c87ab6874e/image.png)

2) where 구를 통해 행 지정하기
(where 구의 위치는 from 뒤이고, 생략가능!)
```
💙 select * from 테이블명 where 조건; 💙
```
* 조건식
* where no = 2 라고 만약 적었다면, no 열 값이 2일 경우에 참이 되는 조건.
* taxi_company_id = 1 인 조건인 데이터들만 불러들이기!
```
💙 select * from tickets where taxi_company_id = 1; 💙
```
![](https://images.velog.io/images/majaeh43/post/cef87ea0-0c55-4e9a-a6ff-cab09c73d6f5/image.png)

* taxi_company_id <> 1 인 조건인 데이터들만 불러들이기!
```
💙 select * from tickets where taxi_company_id <> 1; 💙
```
(요기서 <> 는 '='의 반대! '값 <> 1' -> 값이 1이 아닐 때!)
![](https://images.velog.io/images/majaeh43/post/188493e6-8767-41da-a06a-498f226ba2d1/image.png)

* 몇개 더 연습을 해보자앙 ❣️
1) seat_remain=9 인 데이터들만 츄츌~~~
```
💙 select * from tickets where seat_remain = 9; 💙
```
![](https://images.velog.io/images/majaeh43/post/20ad5877-e21f-42e2-a77a-c450c13f5a53/image.png)

2) seat_remain=9 가 아닌 데이터들만 츄츌~~~
```
💙 select * from tickets where seat_remain <> 9; 💙
```
![](https://images.velog.io/images/majaeh43/post/c1d6b214-ecac-422a-9af6-6e33b3b49022/image.png)

3) 이번에는 문자열을 추출! 문자열을 찾을 때는 싱글쿼트('')를 넣어주기!
```
💙  select * from locations where name = '당산역'; 💙 
```
![](https://images.velog.io/images/majaeh43/post/278ee115-f1b9-4ad0-bb38-7eaea03fa03b/image.png)

4) 날짜시간형도 추출해보장! (이것도 싱글쿼트('') 넣어줘야행!)
```
💙 select * from tickets where arrival_time = '2021-07-01 09:30:00.000000'; 💙
```
![](https://images.velog.io/images/majaeh43/post/89f67718-8bd5-484b-b5aa-5b8292688538/image.png)

* NULL값 검색
```
💙 select * from tickets where price = NULL; 💙
```
* 이게 안먹는이유? **'=' 연산자로는 NULL 값을 검색 못해!**
* NULL값을 검색하려면? **IS NULL** 사용하기!
```
💙 select * from tickets where price IS NULL; 💙
```
* 테이블 내 price 열에는 NULL 값이 없어서 검색이 안됐지만, NULL 값을 검색할 때는 IS NULL을 사용해쥬기~~!

#### 💙 7강 조건 조합하기
* AND / OR / NOT
1) AND로 조합하기
```
💙 조건식1 AND 조건식2 💙
* name이 망원이 아니면서 AND code도 'SUD'도 아닌 데이터를 추출할거야!
select * from locations where name <> '망원' AND code <> 'SUD';
```
![](https://images.velog.io/images/majaeh43/post/8eeae51a-f66e-4a7f-9c6e-91a23597c1a4/image.png)

2) OR로 조합하기
```
💙 조건식1 OR 조건식2 💙
* name이 망원이 아니거나 OR code가 'SUD'가 아닌 데이터를 추출할거야!
select * from locations where name <> '망원' OR code <> 'SUD';
```
![](https://images.velog.io/images/majaeh43/post/8472c3ab-c574-4b4e-b06d-7152f5e0701d/image.png)

3) AND와 OR로 조합해 사용하기
* 연산자의 우선순위를 따져봐야함!
```
💙 where a = 1 or a=2 and b=1 or b=2; 💙
```
* 이렇게 명령을 해주면 and 연산자가 or 연산자보다 우위에 있기때문에 'a=2 and b=1' 이 부분이 먼저 처리 되어버림. 그래서!
```
💙 where (a=1 or a=2) and (b=1 or b=2); 💙
```
* 이렇게 괄호를 통해 내가 연산해줄 명령어들을 먼저 처리할 수 있도록 해주는 것이 필요함!

4) not 조합
```
NOT 조건식
💙 select * from tickets where not (price <> 45000 or seat_remain <> 9); 💙
```

* 연습을 해보장!
![](https://images.velog.io/images/majaeh43/post/f5ee940f-e69d-4737-803e-1790567b9798/image.png)

* price가 45000원이 아니거나 seat_remain이 9가 아닌 데이터들이 아닌 것 ! 
* 좀 헷갈리지만 앞에다가 not을 붙여줌으로써 그렇게 명령이 처리됨 ! 
결국 price가 45000원이 아니거나 seat_remain이 9인 데이터들이 추출됨!

#### 💙 8강 패턴 매칭에 의한 검색
* 패턴 매칭으로 검색하는 방법 -> "LIKE"를 써보자!
```
💙 열 LIKE 패턴 💙
```
* '=' 연산자로 검색하는 경우 셀의 데이터 값이 완전 같은지 비교를 하쥐.
* 그렇지만 '특정 문자나 특정 문자열이 포함되어 있는지 검색하고 싶을 수'도 있쥐.
* 그런 경우 사용하는 방법으로 '패턴 매칭' 또는 '부분 검색'이 있따~~~

1) LIKE로 패턴 매칭하기
```
💙 %_ 💙
```
* 요렇게 특수문자 퍼센트(%)는 임의의 문자열을 의미하고, 언더스코어(_)는 임의의 문자 하나를 의미함. 요 두개를 사용해서 LIKE를 사용할 수 있음.
* locations 테이블에서 '역'이 들어가 있는 행을 패턴 매칭으로 검색해보장.
![](https://images.velog.io/images/majaeh43/post/443cc3b9-6c24-443e-8d47-f4bc432c3b8e/image.png)
* '~역'을 찾을거니까 앞에 당산, 여의나루, 동작 등등 무슨 역인지 나오는데, 그 앞에 문자열들을 %가 처리해준다고 보면됨.
* 그럼 '역' 뒤에 문자열이 있는 경우에는? '역%' 라고 검색하면 되게찌...! 결국 %역% 이렇게 검색하면 '역'이 들어간 데이터들을 다 추출할 수 있뜸!

2) LIKE로 %를 검색하기
* HOXY 그럼 "%"를 검색하고 싶을 때는 어떡하지? ㅎㅎㅎ 그럴때는~~~
```
💙 where 열 LIKE '%\%%' 💙
```
* 포인트!
* '\%'을 통해 %을 검색가능 /. '\_'를 통해 _도 검색가능!

3) 문자열 상수 '의 이스케이프
* '을 문자열 상수 안에 포함할 경우는 '를 2개 연속해서 써쥬기!
```
💙 It's -> 'It''s' 💙
```

힣.. 2장 완료..... 잘하구이따~~~~ 🍒
