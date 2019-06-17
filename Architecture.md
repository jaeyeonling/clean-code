# Architecture

## What is Architecture

### 전체적인 시스템 개발에 기반을 제공하는 변경 불가능한 초기 결정사항의 집합

* Set of irrevocable early decisions that raised the foundation for the entire system development
  * Java: Language
  * IntelliJ: Development Environment
  * Spring: Framework
  * MySQL, MVC

### 건축의 아키텍처가 해머, 못 등이 아니듯

### 툴, Building Material 등이 아니라 사용법(Usage)에 대한 것



## What is Use Case

### a list of steps, typically defining interactions between a role(actor) and a system, to achieve a goal

### 게시글 작성하기

* 사용자
  * 제목을 입력한다.
  * 본문을 입력한다.
  * 글 작성하기를 요청한다.
* 시스템
  * 제목의 유효성을 조사한다.
  * 본문의 유효성을 조사한다.
  * 글을 저장한다.



## Architecture Exposes Usage

### 아키텍처는 사용법에 대해서 설명

### MVC 구조만 있는 웹시스템

* Use case를 숨기고 Delivering 메커니즘만 노출
* 중요한 것은 Delivering 메커니즘이 아니라 Use case
* Use case는 Delivering 메커니즘에 decoupled 돼야 한다.
* UI, DB, F/W, Tools 등에 대한 결정들이 Use case와는 완전히 decouple 되어야 한다.

### Use case should stand alone



## Deferring Decisions

### 좋은 아키텍처는 FW, WAS, UI 등과 같은 stuff들에 대한 결정을 연기하는 것을 허용

* stuff에 대한 결정은 연기될 수 있어야 한다.
* 연기되어야만 한다.
* 이게 좋은 아키텍처의 주요한 목적 중 하나

### 시간이 지날수록 결정을 위한 정보가 풍부해진다.

* TDD의 3가지 법칙을 잘 따르면 설계 문서를 얻게된다.
* test는 low level design document이다.

### EX) Fitness

* 위키 저장을 위해 MySQL을 생각
* 무언가를 하기 전에 DB를 먼저 기동하고 스키마를 개발해야 한다고 생각
* 하지만, 사실 이게 바로 필요하진 않다.
* 위키 텍스트를 html로 변환하는 것에 초점을 둬야한다.
  * 파싱, 번역하는 코드는 DB 없이도 개발할 수 있다.
* WikiPage라는 중요한 추상화
  * wiki text를 가진다.
  * toHtml: wiki text를 html로 parse
  * save: wiki text를 DB에 저장
* 하나 이상의 페이지를 사용해야 하는 경우 발생
  * DB가 실제로 필요한 상황
* InMemoryPage Test Double 
  * 당분간은 DB 사용을 피할 수 있다는 것을 알았다.
  * WikiPage abstraction에 대한 새로운 서브 클래스를 생성함으로써, 메모리의 해쉬 테이블에 위키 페이지를 관리하는 클래스를 만들 수 있다.
  * 이러한 서브 클래스들을 Test Double이라고 한다.
  * Test Double을 이용해서 시스템에서 필요한 모든 기능을 구현할 수 있다. (페이지를 디스크에 저장하는 것을 제외)
* 결국에는 Persistence 없이는 구현할 수 없어졌다.
  * 생각해 낼 수 있는 새로운 테스트는 항상 DB가 필요하다.
  * DB를 기동하고, 스키마를 만들고, DB에 위키 페이지를 저장하고 읽는 기능을 구현
* FileSystemPage Test Double
  * 복잡하지 않게 DB가 있는 것과 같은 환상을 일으키는 테스트를 만들 수 있다.
  * 이 테스트 대역은 DB 구현 없이 DB가 필요한 기능도 만족시켰다.
  * 이 테스트 대역이 위키 페이지를 flat file에 저장한다.
* 주요한 아키텍처 결정을 연기했다.
  * 실제 DB를 사용 안했다.
  * 더 간단하고 충분히 좋은 해결책이 있기 떄문에.
* 최종적으로는 고객사에서 모든 데이터는 실제 DB에 넣아야 한다는 정책이 있어서 그렇게 구현한다.
  * DatabasePage 추가



## Central Abstraction

### 많은 아키텍트는 DB를 core abstraction이라고 생각한다.

* DB가 동작하고 스키마가 준비되기 전에는 어떠한 생각도, 작업도 하지 않는다.

### Fitness 프로젝트의 Central Abstraction - WikiPage

* DB를 연기할 수 있는 Detail로 간주한다.
* 좋은 아키텍처는 Tool, FW로 구성되는 것이 아니다.
* 좋은 아키텍처는 UI, WAS, DI FW 등과 같은 Detail에 대한 결정을 연기할 수 있도록 해준다.

### 어떻게 하면 이렇게 연기할 수 있나?

* 연기하고 싶은 것에서 구조를 decouple, irrelevant하게 설계한다.

### 어떻게 하면 Tool, FWs, DB에서 decouple 할 수 있을까?

* 아키텍처 측면에서 SW 환경이 아닌 Use case에 집중하라.



## Conclusion

### 아키텍처를 Use case에 집중

* UI, FWs, WAS, DB 등과 같은 다른 시스템 컴포넌트에 대한 결정을 미룰 수 있다.
* 이러한 연기는 우리의 선택을 최대한 오래 열어 둘 수 있다.
* 이말은 필요에 따라 결정을 변경할 수 있다는 것이다.
* 프로젝트 진행 중에 충분한 정보가 생김에 따라 undo에 대한 비용 없이 여러번 변경할 수도 있다.







### Decoupling

* 테스트를 먼저 작성하면 Production 코드가 테스트 가능하다.
* 모든 코드 라인을 테스트하는 유일한 방법은 테스트 코드에서 그 코드들에 접근하는 것이다.
* 그러나 테스트 코드에서 코드 라인을 접근하기 위한 유일한 방법은 테스트 하려는 코드를 다른 코드들과 decouple 시키는 것이다.
* TDD로 구현하면 보다 decouple된 시스템을 갖게된다.
* 테스트를 먼저 작성하기만 하면 더 나은 설계를 얻는다.

### Courage to Change

* 개발자가 코드를 깨끗하게 리팩토링하는 것을 두려워하면 코드는 썩는다.
* test가 있어서 시스템이 정상적으로 동작하는지 확인할 수 있다면 변경이 두렵지 않다.
  * regression test
* 테스트는 코드를 깨끗하게 하고, 썩는 것을 방지한다.
* 완벽한 설계에 기반해 개발을 했더라도 테스트가 없다면 코드를 clean하는데 두려움이 생길 것이다.
  * 개선하기 두려울 것이다.
  * 그래서 시간이 지남에 따라 점진적으로 degrade, rot될 것이다.
* 반면 terrible하게 설계를 했더라도 comprehensive suite of tests가 있다면  개선하는 것을 두려워하지 않을 것이다.
  * 그래서 시간이 지남에 따라 점진적으로 점점 더 좋아질 것이다.

### Trust

* 3가지 규칙을 준수했을 때 낙하산에 대한 것과 같은 믿음을 테스트에 가질 수 있게 된다.
* TAD (Test After Development)
  * 테스트를 신뢰할 수 없다.
  * 항상 구멍이 있을 것이라 생각할 것이다.
  * 왜냐면 TAD는 지루하기 때문이다.
  * 이미 수작업으로 테스트를 했기 때문에, 이미 코드가 동작한다는 것을 안다.
  * 낭비적으로 느껴진다.
  * short cut을 취하게 된다.
  * 낙하산을 만드는데 그럴것인가?



## Test Case 추가 순서

### 바로 본질에 접근하지 말고 next most simple and degenerate 케이스를 지속적으로 추가

### TDD의 비밀

* As the tests get more specific, the code gets more generic

### TDD를 잘하는 사람

* 항상 outer에서 시작
* 알고리즘을 구현하기 전에 degenerate case(error, boundary, simple stuff) 등에서 시작

### 테스트코드를 올바른 순서로 추가하면? 

* 지속적으로 production 코드를 generalize 할 수 있고 저절로 알고리즘이 나온다.

### 바로 본질에 접근하면?

* Getting Stucking이 된다.
  * 옴짝달싹 할 수 없는 상태에 빠짐
  * 현재 실패하는 테스트를 성공시키기 위해 점진적으로 할 수 있는 것이 없는 상태
  * 테스트를 성공시키기 위해서는 많은 양의 production 코드를 작성해야만 하는 상황
  * 알고리즘 전체를 다시 작성해야 하는 상황
* 증상
  * 어떤 failing 테스트를 추가 후 어떻게 해야 할지 바로 떠오르지 않는다.
* 원인
  * 잘못된 테스트 코드 작성
  * production 코드를 너무 구체적으로 작성
  * 특정 테스트 케이스만을 위한 production 코드 작성



## Production 코드 추가 시

### 추가해야만 하는 상황을 테스트에서 만들어야 한다.



## 테스트 클래스에서 구현으로 시작

### 그래야 테스트되지 않은 코드가 존재하지 않는다.



## 리팩토링

### 화장실 다녀올 때 마다 손을 씻는다.

### 따로 시간을 잡아서 하는 것이 아니다.

### 늘 깨끗하고 간단하여 읽기 좋기 유지해야 한다.

### 안하면 설계도 없이 마구잡이로 구현하는 꼴이 된다.



## Play a little golf

### 최소한의 코딩으로 테스트를 성공시킨다.

### 너무 많이 Production에서 개발하면 다시 테스트로 돌아가지 못하는 상황이 발생한다.



## Comment Out

### 지우려는 코드를 comment out

### 테스트 실행 후 성공 확인하여 코드의 불필요성 확인 후 삭제



## TDD in Growing Object Oriented Software, Guided by Tests

### TDD

* 테스트는 regression 테스트로서 의미를 지닌다.
  * 새로운 기능을 마음대로 추가할 수 있기 때문
* 테스트를 작성하는 것은 수행할 작업에 대한 acceptance criteria를 작성하는 것
* loosely coupled component 작성을 가능하게 한다.
* 코드가 무엇을 하는지에 대한 실행 가능한 기술 (executable description)
* 리팩토링은 코드를 늘 깨끗하고 간단하게 유지시켜 준다.
* 테스트와 리팩토링을 위해 TDD가 중요하다.

### Levels of Testing

* Acceptance
  * Does the whole system work?
  * same as: "functional tests", "customer tests", "system tests"
  * 진척도 측정을 위한 테스트
* Integration
  * Does our code work against code we can't change?
* Unit
  * Do our objects do the right thing, are they convenient to work with?
  * 회귀 테스트

### Unit Test

* 객체에 대한 unit test는 객체를 생성하고, 의존성을 제공하고, 객체와 상호작용을 하고, 예상한대로 동작하는지 검사할 필요가 있다.
* 그래서 unit test하기 위운 클래스는
  * 명시적인 의존성을 가져야만 하고
  * 이 의존성은 쉽게 대체 가능해야 하고
  * 쉽게 호출되고 검증할 수 있는 명확한 책임을 가져야 한다.
* losely coupled & highly cohesive 해야 한다는 뜻
  * 설계를 잘 해야 한다.
* 테스트를 먼저 작성한 것은 우리의 설계에 대한 직각적이고 값진 피드백을 제공한다.



## ETC

### Leayering 기법(DIP)

* High Level Module should not depend on Low Level Detail
* Separate Complexity

### DB 테스트는 어떻게 하나?

* 대개의 경우 테스트를 안한다.
  * 블랙박스
* 테스트 하고 싶은 것
  * 스키마
  * 쿼리가 원하는 플랜대로 동작하는가?
  * 수작업으로 한번만 진행
* Layering 기법을 이용
  * Application과 DB를 분리
  * DB를 Mock이나 Stub으로 교체할 수 있다.
  * Application을 실제 DB 없이 테스트

### GUI 테스트는 어떻게 하나?

* 대개의 경우 테스트를 안한다.
* the content of the screen can be tested, event if the final format can not.
  * Gray로 표현할지 말지를 결정하는 로직 - O
  * Gray로 표현하는 것 자체 - X
* GUI를 2개의 컴포넌트로 분리한다.
  * Presenter - O
    * integrate the business objects and then constructs the data structure
  * View - X
    * renders that data structure

### Private method는 어떻게 하나?

* protected로 scope을 변경하여 
* reflection을 이용하여
* public으로 변경하여
* 테스트를 안한다.

### Naming

* 이름은 매우 중요하다.
* 구현되지 않은 것에 대해서 이름이 잘 안 떠오를 수 있다.
* foo, bar 등으로 시작해도 된다.
  * 의미가 정확해 질 때 이름도 정확하게 변경하면 된다.

### Mock Library

* 가급적 안쓰는 것이 가장 좋다.
* 신규 코드 작성
  * subclassing & override
  * Mockito
* 레거시 테스트 코드 작성

### TDD & BDUF

* BDUF (Big Design Up Front)
* 허공에 설계 vs 동작하는 코드로 설계
* 오늘 결정할 수 없는 일: unknown unknowns
  * 7% always
  * 13% often
  * 45% Never
* 2주 단위의 Interation에서 2주 후에 보여줄 Executable (Unit Test, Scenario Test)

### Grand Refactoring Project

* Grand Refactoring Project or Make a New System
  * always fails
  * Pareto's Rule
  * Needs Based Refactoring
* 장애 / 버그
  * 재현하는 테스트 추가
  * Make It Pass

### Legacy Project

* Sprout / Wrap Method / Class
* Extract Till Drop - fitness
* Extract Method Object
* Characterization Test - using replacing stdout

### TAD ????

* TAD (Test After Development)
* 프로젝트 완료 후 작성하는 문서
* 되는 것만 해본다.
* 개발하기 위해 협의한 문서는 가치가 없다.
* 완료한 후 인수인계를 위해 작성한 문서는 무의미하다.
  * 형식적이고
  * 도움이 안됨
* Scenario Test 개념으로는 의미가 있다.



