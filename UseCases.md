# UseCases

## Architecture

### Web 기반 Accounting 시스템의 아키텍처에서 주목할 부분

* Accounting 시스템?
* Web 시스템?

## SW 아키텍처

* Accounting Issue를 드러내야 한다.
* Web에 대해서는 거의 언급하지 않아야 한다.

### 하지만 대개의 Web 시스템은 반대

* Web Issue에 대해서는 고함치고,
* 비즈니스 의도에 대해서는 거의 언급하지 않는다.



## Web System에 만연하는 MVC Architecture

### View/Controller

* 강하게 HTML과 연관된다.
* 강하게 모델에 coupling
  * 모델의 구조에 많은 영항을 미친다.

### Model

* Controller에 강하게 연관된다.



## Accounting System Architecture

### Architecture 변경 없이 delivery 메커니즘을 변경할 수 있어야 한다.

* 동일한 시스템을 웹과 콘솔에 deliver할 수 있어야 한다.
* 이 두 시스템의 아키텍처는 동일해야 한다.



## Use Cases

### "Object-Oriented Software Engineering - A Use Case Driven Approach", Ivar Jacobson

* Delivery 문제를 우아한 아키텍처로 해결
* Delivery와 무관한 방식으로 사용자가 시스템과 상호작용하는 방식을 이해하는 것
* 링크, 버튼, 클릭 등의 용어를 사용하지 않고 표현
* Delivery 메커니즘을 나타내지 않는 용어를 사용
* 제이콥슨은 이런 상호작용을 Use Case라고 했다.
* 애플리케이션 개발은 Delivery와 독립적인 Use Case에 의해 주도되어야 한다.
* Use Case가 시스템에서 가장 중요한 것!

### 사용자가 특정 목적을 이루기 위해 시스템과 어떻게 상호작용하는지에 대한 형식적 기술

### 목적

* 주문처리시스템에서 새로운 주문을 생성하는 것

### screen, button. field 등과 같은 웹(delivery 메커니즘)과 같은 것들은 언급하지 않는다.

### 시스템으로 들어가는 데이터, 커맨드와 시스템이 응답하는 것만 언급

### Delivery 메커니즘과 무관한 아키텍처를 가지려면 delivery 메커니즘과 무관한 use case로 시작해야 한다.

### Use case의 응답도 주목해야 한다.

* order-id는 완전하게 delivery 메커니즘과 무관하다.
* human clerk은 order-id를 볼 필요가 없다.
* 반면 delivery 메커니즘은 팝업을 띄워서 사용자에게 항목을 주문에 추가하라고 요청할 수 있다.

### **Use Case는 입력 데이터를 해석하여 출력 데이터를 생성하는 필수 알고리즘**

### Use Case를 구현하는 객체를 생성할 수 있다는 것을 의미한다.



## Use Case Driven Architecture

### Use Case Driven 시스템의 아키텍처를 보면 delivery 메커니즘이 아닌 use case를 보게 된다.

* 독자가 보게되는 것은 **시스템의 의도**이다.



## Use Case Algorithm

### 다른 비즈니스 객체들을 언급

### 알고리즘

* use case 정의
* 비즈니스 규칙을 내포

### 하지만 이런 비즈니스 규칙은 객체에 속하지 않는다.

### 그럼 어디에 비즈니스 규칙을 내포시킬 것인가?

### 어떤 객체에 위치시킬 것이며 Use Case 객체를 아키텍처의 어디에 위치시킬 것인가?

### 어떻게 우리 시스템을 partition해서 use case가 central organizing principle이 되게 할 것인가?



## Partitioning

### 야콥슨이 말하길 아키텍처는 3개의 fundamental kinds of object들을 갖는다.

* Business Objects
  * Entities라고 불린다.
  * Application 독립적인 비즈니스 로직
  * 다른 application에서도 entity들은 사용된다.
  * 특정 application에 특화된 메소드를 가지면 안된다.
    * 이런 메소드들은 Interactor로 옮겨야 한다.
* UI Objects
  * Boundaries라고 불린다.
  * DTO
* Use Case Objects
  * Controller라고 야콥슨은 부른다.
  * 하지만 MVC와 혼동을 피하기 위해 Interactors라고 부른다.
  * Application 종속적인 비즈니스 로직
  * 특정 application에 특화된 메소드들은 Interactor 객체에 구현한다.

### Interactor는 application에 특화된 로직을 통해 목적을 달성한다.

* application과 무관한 entity 로직을 호출
* 예
  * CreateOrderInteractor
    * Order 생성자 호출
    * Order의 getId를 호출
    * 두 메소드는 application 로직과 무관
* Use Case의 목적을 달성하기 위해 이러한 메소드들을 어떻게 호출하는지 아는것이 Interactor의 책임이다.

### Use Case의 책임 중 하나는 사용자로부터 입력을 받고, 결과를 다시 사용자에게 반환하는 것

* 이를 위해 또 다른 객체가 존재한다.
  * Boundary Object
    * Use Case를 Delivery 메커니즘으로부터 격리
    * Use Case를 Delivery 메커니즘 간의 통신 수단 제공
    * MVC / Console / Thick Client 등은 Boundary의 반대편에 존재
    * Use Case는 이러한 Delivery 메커니즘에 대해 모른체 Boundary의 또 다른 반대편에 존재
* Flow
  * Delivery 메커니즘
    * 사용자 요청 수집
    * 요청을 표준적인 형식 (RequestModel)으로 표현
    * Boundary를 통해 RequestModel을 interactor에 전달
  * Interactors
    * Applications 특화된 비즈니스 로직 수행
    * Entity를 조작하여 Application 독립적인 비즈니스 로직 수행
    * 결과를 수집
    * 표준적인 형식 (ResultModel)로 생성
    * Boundary를 통해 다시 Delivery 메커니즘으로 전달



## Use Cases and Partitioning

### 우리는 시스템의 행위를 use case로 기술한다.

* use case에서 application 특화된 행위를 interactor 객체로 캡쳐한다.
* application 무관한 행위를 entity 객체로 캡쳐하고 interactor로 제어한다.
* UI 종속적인 행위는 Boundary 객체로 캡쳐하여 interactor와 커뮤니케이션한다.



## Isolation

### 소스코드 의존성은 하나의 방향만 유지해야 한다.

* Delivery mechanism을 Decouple하기 위해



## Database

### 비즈니스 객체가 아니라 Data Structure를 포함

### 데이터가 저장되는 방식은 Interator나 Entity가 원하는 방식이 아님

### DB와 Entity 간의 Boundary Layer를 제공해야 한다.

* Dependency Inversion Principle



## The Stakeholder Meeting

### Hourly Employee

* paid hourly base
* submit time card at the end of everyday

### Sales Employee

* Commission Base

### Regular Employee

### Union Employee

### Requirements

* Web Based, DB, Web 2.0, Ajax, SOA, By Next Month, Agile Method
* Web 2.0, Ajax, SOA, DB, GUI 등은 무시한다.
  * Details
  * 이러한 것들은 안전하게 연기할 수 있어야 한다.
  * 이러한 것들을 무관하게 하는 것이 우리 아키텍쳐의 목표이다.
  * 필요할 때 쉽게 추가할 수 있어야 한다는 것을 의미한다.

### Analysis

* Use Case로 시작
* Notice
  * 3개의 변형
  * Use Case와 관련된 데이터들이 존재
  * Details에 대한 언급 없음
* Use Case 설계
  * Use case를 Trnasaction으로 매핑

### Entities

* Interactor는 Entities들과 커뮤니케이션 한다.
  * Entities들은 비즈니스 규칙을 표현
  * 이 애플리케이션에서 어떤 종류의 비즈니스 객체들을 가져야 할까?



## Conclusion

### "Agile Software Development - Principles, Patterns and Practices"

### Architectures는 툴이나 프레임워크에 기반하지 않는다.

### 좋은 Architecture

* 툴이나 프레임워크에 대한 결정을 아주 오랫동안 미룸
* 이행되지 않는 결정의 갯수를 최적화
* delivery 메커니즘에 의존하지 않고, 노출시키지 않고 숨김

### 시스템의 모양을 보면 Web 시스템인지의 여부를 알 수 없어야 한다.

### 시스템의 use case는 주요한 추상화(primary abstraction)이고 시스템 아키텍처를 구성하는 핵심적인 원칙

### 아키텍처를 보면 UI가 아니라 시스템의 의도를 볼 수 있어야 한다.

### Interactor가 use case를 캡슐화

### entity는 비즈니스 객체를 캡슐화

### boundary는 UI와 격리를 제공

### 격리를 얻기 위해 application을 delivery 측과 분리하는 boundary 인터페이스를 생성



## What is the Architect?

### 많은 회사들이 상위 레벨 기술 역할로 아키텍트를 규명했다.

### 가끔 이 역할은 기술적이라기 보다 정치적이거나 관료적이다.

### Sales나 management의 입장을 대변하거나 FW을 옹호하거나 한다.

### 이런 것들이 필요하긴 하지만 아키텍트랑은 별 상관이 없다.

### 회사들은 시니어 개발자들을 아키텍트로 승진시킨다.

### 아키텍트가 코딩을 하는 것을 원하지 않는다.

* 좀 더 high level의 무언가(디자인, 리뷰 등)를 하기 원한다.

### 이런 정의들은 아키텍트가 코딩을 안한다는 것을 가정한다.

* 코딩은 아키텍트가 하기에는 아주 low level의 일라고 생각한다.

### 코딩하지 않는 아키텍트는 무능해진다.

### 코딩 못하는 아키텍트의 설계는 무용지물이다.

### 당신이 아키텍트이고 효과적으로 그 역할을 수행하길 원한다면

* 코드를 작성해야 한다.
* 프로그래머들과 함께 일해야만 한다.
* 프로그래머들과 페어 프로그래밍 해라.

### 100%의 시간을 코딩에 쓸 필요는 없다.

* 하지만 약간의 시간이라도 코딩을 해야 할 때면
  * **you should code well.**







