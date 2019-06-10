# OOP

## Why OOP

데이터와 코드가 캡슐화(Encapsulated) 된다.

데이터와 그 데이터를 조작하는 코드의 변경은 외부에 영향을 미치지 않는다.

결합도(Coupling)을 낮추고 응집도(Cohesion)을 높여야 한다.


객체지향이 이렇게 좋은데 사람들이 절차지향으로 짜는 이유는?

객체지향 사고를 가지기 힘들다. (어렵다.)



## Object / Role / Responsibility

객체/클래스의 이름은 무엇으로 정의해야 한다. (어떻게로 정의하지 말자)

역할은 관련된 책임의 집합

객체는 역할을 가진다.



## 객체지향 설계 과정

1. 기능을 제공할 객체 후보 선별
   1. 내부에 필요한 데이터 선별
   2. 클래스 다이어그램
   3. 정적 설계
2. 객체 간 메시지 흐름 연결
   1. 커뮤니케이션 다이어그램
   2. 시퀀스 다이어그램
   3. 동적 설계

위 과정을 반복



## Encapsulation

객체지향의 기본

내부적으로 어떻게 구현했는지를 감춰 내부의 변경(Data, Code)이 Client가 변경되지 않도록 한다.

- 코드 변경에 따른 비용 최소화

Tell, Don't Ask

- 데이터를 요청해서 변경하고 저장하라고 하지말고 무슨 기능을 실행하라.
- 데이터를 잘 알고 있는 객체에게 기능을 수행하라고 하라.
- Encapsulation이 유지되어 변경에 영향을 안받게 된다.

Law of Demeter

- Object should only call
  - it self
  - any parameters that were passed into the method
  - any objects it created
  - any directly held component objects
- Tell, Don't Ask를 지키는지 확인하는 방법

Command Query Separation

- Command (Tell)
  - 객체의 내부 상태를 변경
  - 편이를 위해 어떤 결과를 반환할 수 있다.
- Query (Ask)
  - 객체의 상태에 대한 정보를 제공
  - 객체의 상태를 변경하지 않는다.
  - free of side effects
- 해당 객체의 외부에서 의사결정에 사용하지 않는다면 객체의 상태를 얻을 수 있다.
- 해당 개체의 상태에 기반한 결정은 반드시 객체 내에서 이뤄져야 한다.
- Tell, Don't Ask를 잘 지키게 해준다.



## Polymorphism

한 객체가 여러가지(poly) 모습/타입(morph)을 가질 수 있다.

상속을 통해 다형성을 구현

- 구현 상속
  - 수퍼 타입의 구현을 재사용
- 인터페이스 상속
  - 타입 정의만 상속
  - 상속은 객체에게 다형성을 제공



## Abstraction

타입 추상화

- 공통된 데이터나 프로세스를 제공하는 객체들을 하나의 타입(인터페이스)으로 추상화하는 것
- 객체 지향의 핵심은 의존성 관리를 통해 High Level Logic을 Low Level Detail로 부터 보호하는 것
- Low Level Detail의 변경이 발생해도 High Level Logic는 보호된다.
  - 변경에 영향을 받지 않는다.
  - 재사용된다.


추상화와 개발자의 습성

- 개발자들은 습성상 상세한 구현에 빠지다보면 상위 수준의 설계를 놓치기 쉽다.
- 추상화를 통해서 상위 수준에서의 설계를 하는데 도움을 얻을 수 있다.



## Composition over Inheritance

상속을 통한 재사용 및 추가 기능을 통한 확장

- 서브 클래스는 수퍼 클래스의 기능을 재사용
- 추가적인 기능을 제공하기 쉽다.
- 변경이 유연함 측면의 치명적 단점
  - 수퍼 클래스의 변경이 다수의 서브 클래스에 영향을 미친다.
  - 유사한 기능의 확장에서 클래스의 개수가 불필요하게 증가할 수 있다.
  - 상속 자체를 잘못 사용할 수 있다.

- Composition (Delegation)
  - 유연성 (변경 용이성) 증대
  - Unit Test (Mock) 용이
  - TDD에 용이
  - Interface의 중요성

    
