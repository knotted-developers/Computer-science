#### 💚 20강 COUNT로 행 개수 구하기
* 실제 연습을 위해 지난 프로젝트였던 hoxylush DB를 가지고 연습! 🦖
* 대표적인 집계함수는 5개! COUNT, SUM, AVG, MIN, MAX
* SQL은 데이터베이스라 불리는 '데이터 집합'을 다루는 언어. 이 같은 집합의 개수나 합계가 궁금하다면 SQL이 제공하는 집계함수를 사용해 간단하게 구할 수 있씀!
1. COUNT로 행 개수 구하기
* SQL은 집합을 다루는 집계함수를 제공함! -> 인수로 **'집합'을 지정**함!
```
💚 select count(*) from locations; 💚
```
![](https://images.velog.io/images/majaeh43/post/07e3b183-e646-4fc5-84a7-9904d90659a9/image.png)
![](https://images.velog.io/images/majaeh43/post/970ec8dc-c6e7-4c8e-a814-682d74e4234c/image.png) -> 16개의 행 반환
* 집계함수의 특징은 복수의 값(집합)에서 하나의 값을 계산해내는 것.
* where 구 지정하기
```
💚 select count(*) from locations where name LIKE ='%역%'; 💚
# locations 테이블에서 '역'이 들어가있는 행들만 추출해서 몇개인지 세어보기! 
# 앞에서 like 배운거 응용했는데 ㅠㅠ 대박쓰 진짜 나옴..
```
![](https://images.velog.io/images/majaeh43/post/d87d40fe-9f08-4afa-a929-08a399376013/image.png)

2. 집계함수와 NULL 값
* COUNT의 인수로 열명을 지정할 수 있음. 열명을 지정하면 그 열에 한해서 행의 개수를 구할 수 있음! 특히, '*'를 인수로 사용할 수 있는 것은 COUNT 함수 뿐!
* 여기서! **👊NULL값을 어떻게 취급할것인가!!!!👊** En general, SQL에서는 NULL값을 고려해야함. 집계함수는 집합 안에 NULL값이 있을 경우 이를 제외하고 처리함.
* **NULL이 있는 열명을 언급해서 count명령어로 불러내면 NULL값은 제외하고 계산됨. 하지만 count(*)의 경우 모든 열의 행수를 카운트하기 때문에 NULL값은 셈에 들어간다.**
![](https://images.velog.io/images/majaeh43/post/a2af42e6-ab6d-4c99-bcc4-131ca3531455/image.png)
![](https://images.velog.io/images/majaeh43/post/45c0ce10-206e-407f-8e96-aee92cee10cf/image.png)
![](https://images.velog.io/images/majaeh43/post/5c988989-b443-4203-bb58-40ba38c1b05f/image.png)
* 왜냐면 phone_number에는 null값이 19개나 되기때문에 이걸 다 제하고 8개만 카운트돼서 나오는 것!
3. DISTINCT로 중복제거
* 집합 안에 중복된 값이 있는지 여부가 문제될 때도 있음!
![](https://images.velog.io/images/majaeh43/post/0f9efa67-0534-482b-a070-e6e2104f09c6/image.png)
-> 이런식으로 선릉역이 두개가 중복됨! 그럴 때 사용하는 것이 DISTINCT!
* DISTINCT는 예약어로 열명이 아님. select구에서 distinct를 지정하면 중복된 데이터를 제외한 결과를 클라이언트로 반환. 중복 여부는 select구에 지정된 모든 열을 비교해 판단!
```
💚 select all name from locations; 💚
💚 select distinct name from locations; 💚
```
![](https://images.velog.io/images/majaeh43/post/dbfabc5b-e302-4bf3-9988-0787255203ae/image.png) 신기해...! 🦖

4. 집계함수에서 DISTINCT
* SQL에서는 NULL을 처리하는 것이 무엇보다 중요!
* 그렇다면 !!! 열에서 NULL값도 제외하고, 중복하지않는 데이터를 구할 수는 없을까?
-> **우리는 집계함수의 인수로 DISTINCT를 사용할 수 있어!**
```
💚 select count(all phone_number), count(distinct phone_number) from users; 💚
# count(all 열명)로 phone_number의 null값만 제거,
# distinct에서 phone_number의 중복값 제거 + null 제거!
```
![](https://images.velog.io/images/majaeh43/post/f9c5b697-6f42-4518-bad2-6342835877bf/image.png)

* 다시 말해 all은 null값만 제거해주고, distinct는 중복값제거+null제거라는 것 !

#### 💚 21강 COUNT 이외의 집계함수
* 집계함수는 COUNT만 있는 것이 아니야! SUM 집계함수를 사용해 집합의 합계치를 구할 수 있씀!
* 최솟값, 최댓값을 찾는 경우에도 집계함수를 사용해 처리할 수 있뜸!

1. SUM으로 합계 구하기
![](https://images.velog.io/images/majaeh43/post/a00f8eba-c4ba-4c4d-8308-9c88346ff7c7/image.png)
```
💚 select sum*age) from owners; 💚
```
![](https://images.velog.io/images/majaeh43/post/10011fa6-a72d-4555-ab7e-3a8d5c688671/image.png)
* SUM 집계함수에 지정되는 집합은 수치형 뿐! 문자열형이나 날짜시간형의 집합에서는 합계를 구할 수 없써...
* SUM 집계함수도 COUNT와 마찬가지로 NULL값을 무시함. NULL값을 제거한 뒤 합계를 냄.

2. AVG로 평균내기
* 아까 위에서 구한 SUM을 개수로 나누면 평균! -> SUM / COUNT
* 하지만 굳이, sum, count 쓰지 않더라도 AVG라는 집계함수를 통해 평균값을 구할 수 있음!
![](https://images.velog.io/images/majaeh43/post/40755fce-a105-493d-bead-d89ed3de6530/image.png)
```
💚 select avg(age), sum(age)/count(age) from owners; 💚
```
![](https://images.velog.io/images/majaeh43/post/9ae132c8-a922-4e33-b3e2-ec5d8b7a3db5/image.png)
* 근데 간단하게 요렇게만해도 나옴!
![](https://images.velog.io/images/majaeh43/post/7a6db7a0-78fb-4e9b-be15-8a29c443ab64/image.png)
* AVG 집계함수도 NULL값은 무시. 즉, NULL값을 제거한 뒤 평균값을 계산.
* NULL을 0으로 간주해서 평균을 내고 싶다면 case를 사용해서 NULL을 0으로 변한한 뒤 AVG 사용하기!

3. MIN, MAX로 최솟값, 최댓값 구하기
* MIN, MAX도 집계함수! 이들 함수는 문자열형과 날짜시간형에도 사용가능!
* NULL값을 무시하는 기본규칙은 다른 집계함수와 같음!
![](https://images.velog.io/images/majaeh43/post/e29533f1-81f0-4f8e-8340-075595b970ad/image.png)
```
💚 select min(running_time), max(running_time), min(release_date), max(release_date) from movies; 💚
```
![](https://images.velog.io/images/majaeh43/post/de262e42-c597-4b00-afab-d99dcef7dec4/image.png)
* 신기하다! 진짜 날짜시간형에도 최솟값, 최댓값을 구할 수 있다니 🦖

