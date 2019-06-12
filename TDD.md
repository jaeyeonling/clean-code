# TDD



## The Three Laws of TDD

### Write NO production code except to pass a failing test

### Write only ENOUGH of a test to demonstrate a failure

### Write only ENOUGH production code to pass the test



## TDD 절차

### start

### write a failing test (red)

### write code to make it pass (green)

### refactor (blue)

* mandatory 
* not optional

### stop

* can't think of any more tests



## 원칙 & 팁

### most simple / degeneraate test case first

### little golf game

### As the tests get more specific, the code gets more generic



## TDD의 잇점

### Debugging Time

* Champion Debugger가 되고 싶은가?
* 이건 요구되는 스킬이 아니다.
  * 디버깅에 시간을 보내길 원치 않는다.
  * 코드가 동작하도록 하는데 시간을 사용하길 바란다.
* TDD가 디버깅 시간을 1/10로 줄여 줄 것이다.
* 그런데 1/10이 아니라 1/2만 줄여도 의미가 있다.

### Design Documents

* TDD의 3가지 법칙을 잘 따르면 설계 문서를 얻게된다.
* test는 low level design document이다.

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
* 그래서 unit test하기 쉬운 클래스는
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



