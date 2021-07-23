`문성호`

---

RDBMS는 관계형 데이터베이스, NoSQL은 SQL만을 사용하지 않는 데이터베이스입니다. 데이터를 저장하는 테이블의 스키마와 Join 여부에 따라 구분되며, 데이터 타입과 처리량 / 서비스 성격 등을 고려하여 상황에 맞는 데이터 베이스를 개별적으로 혹은 혼합하여 도입 할 수 있습니다.

웹 앱을 개발 할 때, 데이터 베이스 선택을 고민하게 됩니다.

> MySQL과 같은 SQL을 사용할까? 아니면 MongoDB와 같은 NoSQL을 사용할까?

보통 Spring에서 개발할 때는 MySQL을, Node.js에서는 MongoDB를 주로 사용했을 것이다.

하지만 그냥 단순히 프레임워크에 따라 결정하는 것이 아니다. 프로젝트를 진행하기에 앞서 적합한 데이터베이스를 택해야 한다. 차이점을 알아보자

### SQL

---

SQL은 '구조화 된 쿼리 언어 (Structured Query Language)'를 말합니다. 따라서 데이터베이스 자체를 나타내는 것이 아니라, 특정 유형의 데이터베이스와 상호 작용하는 데 사용 하는 쿼리 언어입니다.

SQL을 사용하면 **관계형 데이터베이스 관리 시스템(RDBMS)에서 데이터를 저장, 수정, 삭제 및 검색** 할 수 있습니다. 이러한 관계형 데이터베이스에는 두 가지 주요 특징이 있습니다.

- 데이터는 **정해진 데이터 스키마에 따라 테이블에 저장**된다.
- 데이터는 **관계를 통해 여러 테이블에 분산**된다.

> **1. 엄격한 스키마**

데이터는 테이블(table)에 레코드(record)로 저장되며, 각 테이블에는 명확하게 정의된 구조(structure)-테이블에 들어갈 수있는 데이터와 그렇지 않을 수있는 데이터를 정의하는 필드 집합-가 있습니다.

구조는 필드의 이름과 데이터 유형으로 정의됩니다.

![https://blog.kakaocdn.net/dn/pFtj2/btqBWDBNyAx/EafOOvlX67vgJv2DApskGK/img.jpg](https://blog.kakaocdn.net/dn/pFtj2/btqBWDBNyAx/EafOOvlX67vgJv2DApskGK/img.jpg)

여기서는 스키마를 준수하지 않는 레코드는 추가할 수 없습니다. 더 많은 필드를 얻고 싶다구요? 죄송합니다만 다른 테이블을 선택하셔야 합니다. 일부 필드가 누락 되었다구요? 그래도 이 테이블은 안됩니다!

(예를 들어, 위 테이블에서 새로운 필드를 넣고 싶다면, 스키마를 뜯어고치지 않는한 필드를 추가 할 수 없다는 것을 말합니다.)

> **2. 관계**

SQL 기반의 데이터 베이스의 또 다른 중요한 부분은 관계입니다.

**데이터의 중복을 피하기 위해,** 데이터들을 여러 테이블로 나누어 저장합니다. 예를들어  Users(사용자), Products(상품), Orders(주문한 상품)의 여러테이블이 존재할 때, 각각의 테이블들은 서로 다른 테이블에 저장되지 않은 데이터 만을 가지고 있습니다.

![https://blog.kakaocdn.net/dn/FUKub/btqBXFFWOWF/KkS5OIKqa2rsVxWfWjgkPK/img.jpg](https://blog.kakaocdn.net/dn/FUKub/btqBXFFWOWF/KkS5OIKqa2rsVxWfWjgkPK/img.jpg)

이런 명확한 구조는 장점이 있습니다. 데이터가 항상 하나의 테이블에서만 관리되기 때문에 잘못된 데이터가 테이블 전체에 복제되어 발생하는 문제가 없습니다.

### NoSQL (Not only SQL)

---

NoSQL은 기본적으로 SQL데이터베이스와 반대되는 접근방식을 따르기 때문에 붙여진 이름입니다.

- 스키마가 없거나 느슨함
- 관계(Join) 없음

이 두가지가 NoSQL을 요약한 것입니다.

- NoSQL 데이터베이스는 여러 종류가 있습니다.

    기반으로하는 데이터 모델 별 대표 NoSQL데이터베이스

    - Document Store
        - 문서모델 NoSQL 은 하나의 키에 구조화된 문서를 저장하고 조회한다.  문서모델에서 의미하는 구조화된 문서란 가장 대표적으로 JSON이 있으며, XML과 같이 구조를 갖는 문서를 말한다.
        - 저장된 문서를 컬렉션으로 관리하고, 저장과 동시에 문서 ID에 대한 인덱스를 생성한다.  문서모델의 키는 문서에 대한 ID로 표현됨.
        - 키-값 및 컬럼 모델에 비하여 많은 종류의 기능을 제공하며, RBMS와 유사한 검색조건을 포함한 쿼리를 처리할 수 있다.  이러한 특징 덕분에 문서모델 NoSQL은 많은 인기를 얻고 있다.
        - 대부분의 문서 모델 NoSQL은 B트리 인덱스를 사용하여 2차 인덱스를 생성한다. 그러나 B트리는 크기가 커질수록 새로운 데이터를 입력하거나 삭제할때 성능이 떨어지게 된다. 이러한 이유로 B트리를 사용하는 문서 모델 NoSQL은 읽기와 쓰기 비율을 7:3 이상으로 유지할때 더 좋은 성능을 보인다. 결국 사용하는 문서 모델 NoSQL의 특징을 파악하고 사용하자.
        - B트리의 특성 떄문에 한 번 작성되면 자주 변하지 않는 정보를 저장하고 조회하는데 적합하며, 로그저장, 타임라인 저장, 채팅로그 기록이나 조회에 적합하다.
        - 문서 모델 NoSQL : MongoDB
    - Key-Value Store
        - 키 값 모델의 가장 큰 특징은 단순한 저장구조를 갖으며, 복잡한 조회 연산을 지원하지 않는다.
        - 저장되는 값을 단지 의미 없는 바이너리 데이터로 처리.
        - 고속 읽기와 쓰기에 최적화된 경우가 많다.
        - 키-값 모델 NoSQL 예 : Redis, Riak 등

        키-값 모델의 특징을 고려해 볼때, 단일 연산에 처리할 수 있는 데이터들을 저장하는데 적합하다.

        참여한 프로젝트의 경우는 자주검색되는 데이터를 Redis에 set하고,

        RDBMS 조회전에 Redis를 먼저 바라봄으로서 검색속도를 비약적으로 개선했다.

        결론, 하나의 서비스 요청에 단일 연산 처리로 대응할수 있는 시스템에 적합하다.

    - Wide Cloumn Store
    - Graph Store

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0cdbd9e-106a-4455-919d-e2cb9d69587c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0cdbd9e-106a-4455-919d-e2cb9d69587c/Untitled.png)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6429bc26-1d03-499b-8d15-67f8da556391/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6429bc26-1d03-499b-8d15-67f8da556391/Untitled.png)

    **간략한 DB 성능비교**

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/decdfd2a-07f1-4bbb-bc66-4373e469b85e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/decdfd2a-07f1-4bbb-bc66-4373e469b85e/Untitled.png)

**[monogoDB와 같은 Document store 양식의 NoSQL 기준으로 설명드리겠습니다]**

> **1. 스키마가 없거나 느슨함**

NoSQL은 테이블(table)을 컬렉션(Collection)으로,  레코드(record)를 문서(documents)라고 부릅니다.

단순히 이름만 다른 것이 아니라, 핵심적인 차이가 있습니다. 

SQL 세계에서는 정해진 스키마를 따르지 않는다면 데이터를 추가 할 수 없었지만, NoSQL에서는 다른 구조의 데이터를 같은 컬렉션(= SQL에서의 table)에 추가할 수 있습니다.

![https://blog.kakaocdn.net/dn/bSSWP6/btqBXGLB9Lu/2KzkbOA3FZPr76ICfJeRR1/img.jpg](https://blog.kakaocdn.net/dn/bSSWP6/btqBXGLB9Lu/2KzkbOA3FZPr76ICfJeRR1/img.jpg)

문서는 약간 JSON 데이터와 비슷한 형태를 가지고 있습니다. 그리고 앞서 연급한것 처럼, 스키마에 대해서는 걱정할 필요가 없습니다. 또한 일반적으로 관련 데이터를 동일한 컬렉션에 넣습니다. 

> **2.관계(Join) 없음**

NoSQL 데이터베이스에는 조인이라는 개념이 없습니다.

대신 데이터가 중복되더라도 컬렉션마다 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 생성합니다.

따라서 여러 테이블 / 컬렉션을 조인(join) 할 필요없이 이미 필요한 모든 것을 갖춘 문서를 만들게 됩니다.

![https://blog.kakaocdn.net/dn/S6STz/btqBW1oUQsg/WI86GuQUWhsXj8R4V7YRG0/img.jpg](https://blog.kakaocdn.net/dn/S6STz/btqBW1oUQsg/WI86GuQUWhsXj8R4V7YRG0/img.jpg)

데이터 복제의 개념은 처음에는 혼란스러울 수 있습니다.

**단점** : 컬렉션 B에서는 데이터를 수정하지 않았는데, 컬렉션 A에서만 실수로 데이터를 수정하게 될 위험

특정 데이터를 함께 사용하는 모든 컬렉션에서, 똑같은 데이터 업데이트가 수행되도록 하는 것이 우리의 임무

**장점:** 그럼에도 불구하고, NoSQL의 가장 큰 장점은 복잡한 조인문으로 작업 할 필요가 없다는 것입니다.

필요한 모든 데이터가 이미 저장되어 있기 때문입니다.

NoSQL은 특히 데이터 수정작업이 필요없는 자주 바뀌지 않는 데이터 일때 좋습니다.

- SQL vs NoSQL Data 예시

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c303ad5-a23e-45cb-bce3-0d4338da4790/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c303ad5-a23e-45cb-bce3-0d4338da4790/Untitled.png)

    RDBMS 상에서 JOIN을 통한 데이터 정렬

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c125b70-3544-4440-88cc-fa75b9f6b904/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c125b70-3544-4440-88cc-fa75b9f6b904/Untitled.png)

    NoSQL에서 JSON 형태를 이용한 데이터 나열

### **수직 및 수평 스케일링**

---

두 데이터베이스를 비교할 때 살펴 봐야할 또 하나의 중요한 개념은 스케일링(Scaling: 확장)입니다.

데이터베이스를 어떻게 확장 시킬 수 있을까요? 

(데이터베이스에서 처리 할 수있는 읽기 및 쓰기 요청 수를 의미합니다)

확장은 수직확장(Scale up)과 수평확장(Scale out)으로 구별 할 수 있습니다.

- **수직 확장**이란 데이터베이스 서버의 성능을 향상시키는 것입니다. (예를 들어, CPU를 업그레이드)
- **수평 확장**은 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미합니다. 따라서 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동합니다.

![https://blog.kakaocdn.net/dn/bZNmsQ/btqBVLNRwpD/lRKnntxIQODQBfliwWAOOK/img.jpg](https://blog.kakaocdn.net/dn/bZNmsQ/btqBVLNRwpD/lRKnntxIQODQBfliwWAOOK/img.jpg)

데이터가 저장되는 방식 때문에 SQL 데이터베이스는 일반적으로 수직 확장만을 지원합니다. 

수평 확장은 NoSQL 데이터베이스에서만 가능합니다.

SQL 데이터베이스는 **'샤딩(Sharding)'**의 개념을 알고 있지만 특정 제한이 있으며 일반적으로 구현하기가 어렵습니다. NoSQL 데이터베이스는 이를 기본적으로 지원하므로 여러 서버에서 데이터베이스를 보다 쉽게 분할 할 수 있습니다.

### **올바른 선택**

---

둘 중 어떤 데이터베이스 솔루션을 사용해야 할까요?

확실한 정답은 없습니다. SQL과 NoSQL은 모두 가능한 솔루션입니다. 

결국 어떤 데이터를 다루는지, 어떤 애플리케이션에서 사용되는에 따라 결정됩니다.

두 가지 접근 방식의 주요 장단점을 요약 해 보겠습니다.

> **SQL의 장점**

- 명확하게 정의 된 스키마, 데이터 무결성 보장**(ACID 기반 Transaction 가능)**
- 관계를 통해 각 데이터를 중복없이 한 번만 저장할 수 있습니다

> **SQL의 단점**

- 상대적으로 덜 유연하며, 데이터 스키마는 미리 알고 계획해야합니다. (나중에 수정하는 것이 어렵거나 불가능 할 수 있습니다.)
- JOIN문이 많은 매우 복잡한 쿼리가 만들어 질 수 있습니다.
- 수평 확장이 어렵고, 보통 수직 확장만 가능합니다. 즉 어느 시점에서 처리량/처리 능력과 관련하여 성장 한계에 직면하게 될 수 있습니다.

> **NoSQL의 장점**

- 스키마가 없기때문에, 유연성이 높습니다

    즉, 저장된 데이터를 언제든지 조정하고 새로운 "필드"를 추가할 수 있습니다.

- 데이터는 애플리케이션에 필요한 형식으로 저장됩니다. 데이터를 가져오는 속도가 빨라집니다.
- 수직 및 수평 확장이 가능하므로 데이터베이스가 애플리케이션에서 발생시키는 모든 읽기 / 쓰기 요청을 처리 할 수 있습니다.
- 비정형 데이터 저장에 유리합니다(이미지, IoT 데이터 등)

> **NoSQL의 단점**

- 유연성 때문에, 데이터 구조 결정을 늦어질 수 있습니다.(바로 계획, 결정해야하는 것이 아니기 때문에)
- 복사된 데이터가 변경되면 여러 콜렉션과 문서를 수정해야 합니다.

> **그렇다면 언제 SQL이 가장 좋을까요?**

- 앱의 여러 부분에서 관련 데이터가 처리량은 작으나 비교적 자주 변경되는 경우
- 명확한 스키마가 중요하며, 데이터구조가 극적으로 변경되지 않을 때
- Transaction 사용이 필요할 때(은행 등)

> **그렇다면 NoSQL은 언제 가장 좋을까요?**

- 정확한 데이터 요구사항을 알 수 없거나 데이터 간 관계가 자주 변경(수정)/확장되는 경우
- 읽기(read)/쓰기(write)처리를 자주하지만, 데이터를 자주 변경하지 않는 경우
- 데이터 간 관계가 중요하지 않은 경우(즉, 한번의 변경으로 수십 개의 문서를 수정 할 필요가 없는 경우)
- 데이터베이스를 수평으로 확장해야 하는 경우

    즉, 막대한 양의 데이터를 다뤄야 하는 경우, 읽기/쓰기 처리량이 큰 경우

    초당 데이터가 수 십만개 씩 쌓이는 서비스가 많아짐(소셜, 온라인 서비스 등)

> **어떤 NoSQL을 선택할까요?**

- 일관성 모델 : 서비스에서 저장하려는 데이터가 어느 정도의 일관성이 필요한지 확인하여야한다.
- 데이터 모델 : 저장하려는 데이터가 키-값 모델과 같은 간단한 데이터 모델로 처리가 가능한지 또는 문서 모델과 같이 중첩된 구조를 지원해야 하는지 판단해야 한다.
- 읽기 쓰기 성능 : 읽기와 쓰기 비율에 따라서 적합한 NoSQL이 다르다. 빠른 응답시간 필요 시, 인메모리 NoSQL이 적합하며, 상대적으로 읽기 비율이 높다면 Document NoSQL이 후보가 될 수 있다.
- 원자성 지원 : 선택한 NoSQL의 트랜잭션 지원 여부, 단일 연산에 대한 원자성 지원 여부 등

하나의 제시 방법이지 완전한 정답이 정해져 있는 것은 아니다.

SQL을 선택해서 복잡한 JOIN문을 만들지 않도록 설계하여 단점을 없앨 수도 있고

NoSQL을 선택해서 중복 데이터를 줄이는 방법으로 설계해서 단점을 없앨 수도 있다.

일반적으로 기업들은 Relational 데이터베이스와 NoSQL 데이터베이스를 혼합하여 사용하고 있습니다.

정확하고 빠른 분석이 필요한 중요 데이터의 경우에는 RDBMS를 사용하고 관리하고 있으며,

비정형의 정재가 필요한 데이터는 NoSQL 데이터베이스를 사용하여 관리하고 있습니다.

---

`참고자료`

[https://devuna.tistory.com/25](https://devuna.tistory.com/25)

[https://gyoogle.dev/blog/computer-science/data-base/SQL & NOSQL.html](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)

[https://www.samsungsds.com/kr/insights/1232564_4627.html](https://www.samsungsds.com/kr/insights/1232564_4627.html)

[http://www.codingworldnews.com/news/articleView.html?idxno=1934](http://www.codingworldnews.com/news/articleView.html?idxno=1934)

[https://seohs.tistory.com/462](https://seohs.tistory.com/462)
