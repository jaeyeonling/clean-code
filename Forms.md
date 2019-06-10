# Forms

## Coding Standards

### 조직이 일정 수준의 크기가 되면 관료적인 문서화를 요구한다.

### Coding Standards는 코드 내에서 명확하게 보여져야 한다.

### 코드가 Coding Standards여야 한다.

### 만약 별도의 문서에 Coding Standards를 작성한다면?

* 코드가 Coding Standards의 예로 적합하지 않다는 것을 의미한다.



## Comments should be Rare

### Coding Standards가 코멘트 작성을 강요하면?

* 프로그래머는 필요해서가 아니라 해야 하므로 코멘트를 작성한다.
* 이런 코멘트는 무의미하다.
* 이런 코멘트는 무시의 대상이 된다.
* 가치가 없다.
* Comments should be rare
  * Special Cases
  * Programmer's intent를 위해 반드시 필요할 때
  * 그 코멘트를 읽는 모든 사람들이 감사해야 한다.



## Comments are Failures

### 작성자의 의도가 잘 나타나게 프로그램을 작성한다면 코멘트가 불필요해진다.

### 코드로 의도를 나타낼 수 있을까?

* Assembly의 경우는 불가능하다.
  * 코멘트가 필수적이다.
  * Pascal, Fortran, C도 다소 그런 편이다.
  * 코멘트 없이 표현력이 뛰어난 코드를 작성하는 것은 매우 어렵다.
* Ruby, Java, C# 등은 매우 표현력이 뛰어나다.

### 모든 코멘트는 당신의 코드가 Expressive하지 못하는 것을 나타내는 실패의 상징이다.



## Good Comments

### Legal Comments

### Informative Comments

### Warning of Consequences

### TODO Comments

### Public API Documentation



## Bad Comments

### Mumbling

### Redundant Explanations

### Mandated Redundancy

### Journal Comments 

### Noways Comments

### Big Banner Comments

### Closing Brace Comments

### Attribution Comments

### HTML in Comments

### Non-Local Information

* 멀리 떨어진 곳의 코드를 설명하는 코멘트는 코멘트와 무관하게 변경될 수 있다.
* 그런 코멘트를 작성하지 말자.
* 코멘트를 작성해야만 한다면 코멘트가 설명하는 코드와 밀접한 곳에 작성하라.



## Vertical Formatting

### 공란을 함부로 사용하지 말라.

* 메소드 사이
* private 변수들과 public 변수들 사이
* 메소드 내
  * 변수 선언과 메소드 실행의 나머지 부분 사이
  * if/while 블록과 다른 코드 사이

### 서로 관련된 것들은 Vertical하게 근접해야 한다.

* Vertical한 거리가 그들간의 관련성을 나타낸다.



## Classes

### 클래스란 무엇인가?

* private 변수들을 작성함으로써 클래스를 작성한다.
* 그리고 그 private 변수들을 public 함수들로 조작한다.
* 외부에서는 private 변수들이 없는 것 처럼 보인다.

### 객체의 상태를 외부에서 사용할 수 있도록 하는 getter/setter/property 등을 제공하는 것은 Bad Design

### Tell, Don't Ask

* 객체가 no observable state를 갖는다면
  * 무엇을 하라고 시키기(tell) 쉽고
  * ask할 가치가 없어진다.
* 이 규칙을 따르는 객체들은
  * getter가 많지 않다.
  * getter가 많지 않으므로 setter도 많지 않다.

### Max Cohesive

* 메소드가 모든 변수를 조작하는 경우

### Max Cohesive Class

* Max Cohesive 메소드들로만 구성된 클래스

### getter/setter는 Cohesive하지 않다.

* 하나의 변수만 사용하기 때문이다.
* 클래스가 getter/setter를 많이 가질수록 덜 Cohesive 해진다.
* getter/setter가 없어야만 하는가?
  * 안쓸 수는 없으니 최소화한다.
    * 그래야 Cohesion을 최대화할 수 있다.
  * getter를 쓸 때 본래 변수를 그대로 노출하지 말라.
    * 추상화를 통해 제공하라.

### getter를 추상화하여 제공한다.

### Polymorphism

* 내부 변수를 hide 했을 때의 이점
* 상세 구현을 덜 노출할수록 Polymorphism 클래스를 활용할 기회가 늘어난다.

### Polymorphism은 Independent Deployability와 Plugin Structure의 핵심

* 객체지향의 핵심
  * IoC를 통해 High Level Policy를 Low Level Detail로 부터 보호하는 것



## Data Structures

### Class와 반대되는 개념

* Class
  * private 변수들 + 이를 다루는 함수들
  * cohesive groups of variables를 조작하는 메소드
  * 구현을 hide, abstract
  * Tell이 가능
    * 객체에 generic한 일을 수행하라고 tell 할 수 있다.
    * 그러면 자동으로 타입에 맞는 적절한 행위가 발생한다.
    * polymorphically dispatch to appropriate methods.
* Data Structure
  * public 변수들 + getter/setter
  * 개별 변수들을 조작 (getter/setter)
  * 구현을 노출
  * Tell은 불가, Ask만 가능
    * generic한 행위를 수행하라고 tell 할 수 없다.
    * type에 기반하여 메소드 호출을 해야한다.
      * switch 문장을 사용해야 한다.



## Boundaries

### Main 파티션과 App 파티션과 어떻게 분리할 것인가?

* Main이 App 파티션의 플러그인

###Main/App 파티션을 나누는 것은 Boundary의 일예

*  다른 2가지 예로 Model/View, DB/Domain Object 등이 존재

### 각 Boundary에서 한쪽은 Concrete(Main)하고, 다른 한쪽은 Abstract(App)하다.

### Boundary 사용시 항상 Concrete에서 Abstract로 소스 코드 의존성이 있어야 한다.

* 예) DB(Concrete)와 Domain Object(Abstract)의 소스 코드 의존성 방향

### Database

* DB Interface Layer -> Database는 이해가 용이
* DB Interface Layer -> Application and Domain Objects는 납득이 안된다.
  * DB Interface Layer가 concrete하고 Application and Domain Objects는 abstract하니 이론상은 맞는 말이다.
  * OOD에선 런타임 의존성을 변경하지 않고, 소스 코드 의존성을 inversion
  * DIP
    * Application이 DB Interface Layer의 존재를 모르고도 DB Interface Layer를 호출할 수 있다는 것을 의미



## The Impedance Mismatch

### OOP에서 RDB를 사용할 때 발생하는 일련의 개념적/기술적 어려움

* 특히 객체나 클래스의 정의가 데이터베이스 테이블이나 관계 스키마에 직접 매핑될 때 발생한다.

### DB Table은 DS이다.

* Data를 노출하고, 메소드는 없다.
* class와 반대다.
* DB 테이블은 너무나 concrete해서 polymorphic 할 수 없다.

### DB는 도메인 객체, 비즈니스 객체, 어떤 객체도 포함할 수 앖다.

* 오직 DS만 포함한다.
* 강제로 DS를 객체화 할 수 없다.

### ORM

* Hibernate?
* 진정한 Object-Relational Mapper는 아니다.
* DB row와 객체간의 직접적인 매핑이 없기 때문이다.
  * 하나는 DS이고 다른 하나는 객체이기 때문이다.
* 실제로 이런 툴은 RDB 테이블 -> DS르의 매퍼이다.
* Hibernate는 DB의 DS를 메모리의 DS로 매핑한다.

### Application/Domain Objects의 메소드들이 비즈니스 규칙이다.

* 일련의 비즈니스 규칙들을 도메인 객체에 구현하여 클래스를 만든다.
* 이 클래스들은 DB의 구조나 스키마와는 다른 모습으로 갖는다.
* 이게 RDB와 OOD 간의 진정한 임피던스 불일치이다.
* DB는 특정 Application을 위해서가 아니라 Enterprise를 위해서 최적화된다.
  * DB 스키마는 Enterprise의 security, performance를 위해 설계된다.
    * 개별 Application은 다른 스키마 디자인을 원할 것이다.
    * 하지만 Enterprise 전체의 combined needs에 순응해야만 한다.

### Application Boundary 측면에서는 Enterprise 스키마를 객체 설계를 통해 분리할 수 있다.

* 이게 진짜 객체이다.
  * 메소드를 노출하고 데이터를 감춘다.
* 테이블 row를 조작하는 대신 비즈니스 객체를 조작함으로써 애플리케이션을 보다 자연스럽게 하고 이해하기 쉽게 한다.

### DB Interface Layer는 DB에 존재하는 DS를 Application이 사용하고자 하는 비즈니스 객체로 전환하는 책임을 갖는다.

* Application은 DB Interface Layer의 존재 조차도 모르게 한다.
* 모든 소스 코드 의존성은 DB에서 Application으로 행해야 하기 때문이다.
* 이 말은 Application 계층에 데이터 액세스를 제공하는 인터페이스를 갖게된다는 것을 의미한다.
* 비즈니스 객체가 이 인터페이스를 이용해서 자기 자신이 원하는 데이터에 접근한다.

### View와 Application의 관계도 마찬가지다.

* View가 Concrete이므로 Application에 의존성을 가져야 한다.





