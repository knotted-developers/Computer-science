
## Cache
> non-Persistence 한 메모리 저장
> 
> 동작: 첫 로드에서 캐시했다가 다시 접근할 때 캐시를 이용해 빠르게 로드한다.



### 캐시는 약방의 감초 역할 
![image](https://user-images.githubusercontent.com/79136484/126867153-e3f9f327-4e8a-4a32-bf0b-256733483bb0.png)

구간 별 캐싱 정리 예정

1.
2.
3.
4.
5.

### server-side

server caching

In memory cache를 통한 IO load 감소 및 속도 향상

대표예시:

1. CPU 캐시 적용, 주기억장치 및 cpu 효율성 향상

2. CDN, 장거리 혹은 오지 web user의 web 이용성능 및 효율 향상 위한 Content caching server 이용

해외 통신망,해저케이블 등을 직접 이용하지 않고 Content Delivery Network 진행

전송속도 향상, load 감소, 원가 감소

유튜브에서는, 인기있는 동영상은 캐시하여 미국서버까지 올 필요없이 국내 캐싱 서버로 처리

3. Database(SSD,HDD), Cache memory 적용, 효율성 향상

write보다 read가 많은 특성 이용

### Browerside caching

 local host caching

4.웹캐시[Front단] 

- 브라우져 캐시

### HTTP cache[browser 상, front 단 cache = 브라우져 캐시]

web browser 상에서 캐시

웹의 성격/보안중요성/동적웹/정적웹/신선도 상황을 고려하여 캐시 정책을 디테일하게 조절해야한다

-장점

web(최신상태를 유지)과 app(빠른 속도와 접근성)의 특징을 모두 갖춘 webapp에 사용하자

최초 load 후에는 동일 request에 대해 매우 빠르게 반응

-단점보완

contents update시 반영 안 될 수 있다.

캐시정책: max_age = 짧게 혹은 no(캐시할 때마다 update 여부 묻겠다) 

+ Etag 적용

으로 캐시의 단점인 신선도 유지를 보완한다

```python
브라우져 request에서 현재 캐시내용이 바뀐게 있는지 물어보고(moify 시간 + Etag in 헤더 담아서 물어봄) 
-> 서버는 modify 시간 / Etag(content고유 태그, 내용수정 시 바뀜) request와 현재 update된 contene 비교
→ 서버가 response로 바뀐게 없다(헤더에 status304담음)고하면, 헤더 - 헤더 통신만으로 캐시급으로 빠르게 통신 진행
→ 서버가 response로 바뀐게 있다(헤더에 status200, 바뀐 content 보냄)보낼 때만, load 적용하여 통신 재진행
```

- 응답 캐시

- 프록시 캐시
