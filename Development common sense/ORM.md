`문성호`

---

**ORM 역할**

 **객체 관계 매핑**(Object-relational mapping)의 약자로, 서로 다른 Langauge와 OOP를 사용하는데 제약 받지않으면서 RDBMS를 이용하기 위한 Framework입니다. 

**ORM 정의**

**Persistence layer 구간**에 위치하며, DBMS(MySQL, MSSQL 등)를 자동 mapping해 리소스(데이터)를 **객체화**하여 Query를 수행하는 공통된 접근기법으로 사용합니다.

- `Persistence`(영속성)

    데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성

    ORM은 프로그램 아키텍처 MVC 구조에서 

    데이터에 영속성을 부여해주는 계층인 Persistence layer에 위치한다

    ![](https://github.com/knotted-developers/Computer-science/blob/0a66fd079dd3f39c7934a354aca29be4cfcffad9/Development%20common%20sense/ORM.md)

> **ORM 장점**

1) DBMS에 대한 큰 고민없이, ORM에 대한 이해만으로 웬만한 CRUD를 다룰 수 있기 때문에, 비즈니스로직에 집중할 수 있으므로 **개발 생산성을 증가**시킬 수 있다.

2) 객체를 통하여 대부분의 데이터를 접근 및 수정을 진행하므로, **코드 가독성**이 좋다.

3) 데이터 구조 변경시, 객체에 대한 변경만 이루어지면 되므로, **유지보수성**이 좋다.

> **ORM 단점**

1) **Complex Query에 대한 대응 어렵다.**

---

## **Python의 대표 ORM인 `DjangoORM`과`SQLalchemyORM(SQLA)` 비교**

> **Django ORM과 SQLalchemy ORM 비교**

- `Django ORM`

    Django에 내장되어있는 ORM으로, **active record implementation** 을 바탕으로 한다.

    - **Active record implementation**
        1. Database의 schema(=Model class)와 Mapping 된 Domain 내의 데이터 객체 간 모든 field가 동일해야한다.

            Persistant Layer와 Domain Layer가 가깝다.

        2. Autocommit되어 직관적이다.

- `SQLalchemy ORM`

    Python으로 사용가능한 ORM으로, **Data Mapper implementation** 을 바탕으로 한다.

    - **Data Mapper implementation**
        1. Database의 schema(=Model class)와 Mapping 된 Domain 내의 데이터 객체 간 분리되어있다.

            Persistant Layer와 Domain Layer가 멀다.

            Session으로 연결해줘야 한다.

        2. Autocommit되지 않아 직관적인 CRUD 구현되지 않으나 정형적이다.

**결론**

전제: 절대적으로 유리한 ORM은 없다

SQLalchemy ORM 우위

- 규모가 크고 복잡하며(Skinny contorller,Fat model)
- READ query 위주이며
- 비즈니스 로직 상 Constraint가 확연하고
- 유지보수가 중요할 시
- 

Django ORM 우위

- 규모가 크지 않으나
- CRUD query가 다수이며
- 비즈니스 로직 상 Constraint가 강하지 않을 시

**차이점**

- DataStructure 과 ObjectStructure 간 분리도

    Django ORM uses the active record implementation

    SQLAlchemy uses the Data Mapper implementation

    - SQLalchemy model(Database 관점)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c08e93f1-db3b-4a28-9600-f82b224c588b/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c08e93f1-db3b-4a28-9600-f82b224c588b/Untitled.png)

    - Framwork schema(Domain 관점)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c04aad33-b66c-4ebb-bfea-414ac246115a/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c04aad33-b66c-4ebb-bfea-414ac246115a/Untitled.png)

    - Framwork View

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc155073-c814-4bed-9fba-171db0206b95/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc155073-c814-4bed-9fba-171db0206b95/Untitled.png)

    1. response schema / 2. input schema                                    3. db와 직접 연결 / 4. 직접 commit

Complex Queries 적합도

Autocommit 여부

- Primary Key 자동생성

    **Django orm**

    Table modeling 시, Primary Key가 Autoincrement로 정의된다.

    **SQLA** 

    Primary Key가 자동생성되지 않아, Table modeling 시 class에 직접 정의해 준다.

    Table간 관계가 복잡해질수록 SQLA의 유연성이 더 커진다...?

---

`참고자료`

[https://ebs-integrator.com/blog/django-orm-vs-sql-alchemy/](https://ebs-integrator.com/blog/django-orm-vs-sql-alchemy/)

[https://culttt.com/2014/06/18/whats-difference-active-record-data-mapper/](https://culttt.com/2014/06/18/whats-difference-active-record-data-mapper/)
