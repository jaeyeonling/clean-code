# Function Structure

## Arguments

### 인자가 많아지면 복잡도가 증가한다.

### 3개의 인자를 넘지 말자.

* 외우기 어렵다.

### 생성자의 많은 수의 인자를 넘겨야한다면?

* Java Bean Pattern
  * inconsistent state
* Builder Pattern

### Boolean 인자 사용 금지

* 2가지 이상의 일을 하는 것
  * true의 경우를 위한 일
  * false의 경우 위한 일
  * 2개의 함수로 분리

### Innies not outies

* Output 인자를 사용하지 말라.
* Argument는 함수로 전달되는 것이지, 함수로부터 변경되어 나오는 것이라고는 생각하지 않음.
* Output Argument 대신 return value로 처리

### The null defense

* null을 전달/기대하는 함수는?
  * boolean을 전달하는 만큼 잘못된 것
  * null인 경우의 행위 + null이 아닌 경우의 행위
  * 2개의 함수를 만드는 것이 낫다.
* null을 pseudo boolean로 쓰지 마라.
* defensive programming을 지양
  * 코드를 null, 에러 체크로 더럽히지 말라.
  * 잘못되었다는 단서 (smell)
  * 팀원이나 단위 테스트를 못 믿는다는 말
  * null 여부를 지속적으로 조사할 것이 아니라 단위 테스트에서 검증해야 한다.
* 외부 API의 경우는 defensive하게 programming한다.



## The Stepdown Rule

### 모든 public은 위에, 모든 private는 아래에 둔다.

### public part만 사용자들에게 전달하면 된다.

### 중요한 부분은 위로, 상세한 부분은 밑으로 간다.

### Backward reference 없이 top에서 bottom으로 읽을 수 있게 한다.



## Switchs and cases

### OOP의 가장 큰 이점 중 하나는 의존성 관리 능력이다.

* 모듈 A가 모듈 B의 함수를 사용하는 경우
  * 절차지향
    * 독립적으로 배포/컴파일/개발 불가능하다.
  * 객체지향
    * Runtime 의존성은 그대로 둔채로 Source code 의존성을 역전시킨다. (Dependency Inversion Principle)
    * 절차
      * 본래의 의존성을 제거
      * Polymorphic interface를 삽입
      * 모듈 A는 인터페이스에 의존하고, 모듈 B는 인터페이스로부터 derive한다.
      * B의 Source code 의존성은 Runtime 의존성과 반대가 된다.
      * Independent Deployability

### Switch 문장은 독립적 배포에 방해가 된다.

* 각 Case 문장은 외부 모듈에 의존성을 갖는다.
* 다수의 다른 모듈에 의존성을 가질 수 있다.
* Fan-out Problem이라고 한다.
* Switch 문장에서 Source code 의존성은 Flow of Control과 방향이 같다.
  * 모든 외부 모듈에 영향을 받는다.
  * 외부 모듈 중 하나라도 변경이 일어나면 Switch 문장이 영향을 받는다.
    * Switch에 의존하는 다른 모든 것들도 영향을 받는다.
  * 독립적 배포를 불가능하게 하는 많은 의존성을 만든다.
    * 독립적 컴파일/개발도 불가능하다.

### Switch 문장 제거 절차

* Swich 문장을 Polymorphic Interface 호출로 변환
* Case에 있는 문장들을 별도의 클래스로 추출하여 변경 영향이 발생하지 않도록 한다.
* 신경 쓸 일은 언제/어떻게 인스턴스들을 생성하는가이다.
* 팩토리에서 이런 작업들을 수행한다.



## Temporal Coupling

### 함수들이 순서를 지키며 호출되어야 한다.

### Passing a Block



## CQS

### Side Effect를 관리하는 좋은 방법이다.

### Command

* 시스템의 상태 변경 가능
* Side Effect를 갖는다.
* 아무것도 반환하지 않는다.

### Query

* Side Effect가 없다.
* 계산값이나 시스템의 상태를 반환한다.

### CQS 정의

* 상태를 변경하는 함수는 값을 반환하면 안된다.
* 값을 반환하는 함수는 상태를 변경하면 안된다.

### 당신의 코드의 독자들을 혼란스럽게 하지 말라.

* 값을 반환하는 함수는 상태를 변경하면 안된다.
* 상태를 변경하는 함수는 Exception을 발생시킬 수는 있지만, 값을 반환할 수는 없다.
* 약속이다.



## Tell Don't Ask

### Extreme한 CQS는 C와 Q를 함께 사용하지 말도록 한다.

### Tell Don't Ask

* Tell other object what to do
* But not to ask object what the state is

### 이 규칙을 준수하다보면 Q가 많이 필요가 없어진다.

* 매우 좋은 것이다.
* 왜냐면 Q는 곧 Out of Control 되는 경향이 있다.



## Law of Demeter

### 하나의 함수가 전체 시스템의 객체들 간의 네비게이션을 아는 것은 잘못된 설계다.

### 함수가 시스템 전체를 알게 하면 안된다.

### 개별 함수는 아주 제한된 지식만 가져야 한다.

### 요청을 수신하면 적절한 객체가 수신할 때 까지 전파되어야 한다.

### 일련의 규칙을 통해 Tell, Don't Ask를 형식화(formalize)한다.

* 아래와 같은 객체들의 메소드만 호출할 수 있다.
  * 인자로 전달된 객체
  * Locally 생성한 객체
  * 필드로 선언된 객체
  * 전역 객체
* 이전 메소드 호출의 결과로 얻는 객체의 메소드를 호출하면 안된다.

### Ask 대신 Tell하면 Surrounding과 Decouple된다.



## Ealry Returns

### Ealry Return이나 Guarded Return은 허용한다.

### 루프의 중간에서 리턴하는 것은 문제다.

* break, 루프 중간에서의 return은 loop를 복잡하게 한다.
* 코드가 동작하도록 하는 것보다 이해할 수 있게 하는 것이 더 중요하다.



## Error Handling

### Use Exception

* Checked
  * Reverse Dependency를 유발한다.
    * 하위 클래스에서 어떤 Exception이 유발되면 상위 클래스를 변경해야한다.
    * 사용되는 모든 코드를 변경해야 한다.
  * 잘 모르면 Checked Exception을 사용하지 말자.
* Unchecked

###  Exception들에 어떤 메시지를 담아야 할까?

* Message가 필요 없는 것이 가장 좋다.
* Exception 이름을 정확하게 지어 이름으로 의미가 전달되도록 한다.
  * 가장 좋은 코멘트가 코멘트를 작성하지 않는 것이다.
  * 코드(이름)가 코멘트를 대신하도록 해라.



## Special Cases

###매우 특별한 경우 예외처리

* Special Case Pattern 
* Null Object Pattern



## Null is not an error

### Null을 반환할 수도 있다.

* 사용자가 Null을 반환하는 것을 기대할 것 인가?
* null은 NPE를 발생시킬 때 까지 시스템의 여기저기 조용히 퍼지는 속성이 있다.



## Null is a value

### Null을 반환할 수도 있다.

* 사용자가 Null을 반환하는 것을 기대할 경우
  * 어떤 때는 실패할 것을 기대하기 때문이다.
* Exception이 부적절한 경우
  * Exception은 기대하지 못한 때를 위한 것이다.
* 예외상황 때 반환할 수 있는 값이 필요하다.



## try도 하나의 역할/기능이다.

### 함수 내에서 try 문장이 있다면 try 문장이 변수 선언을 제외하고는 첫번째 문장이어야 한다.

### try 블럭 내에는 한 문장(함수 호출)만 있어야 한다.

### finally가 함수의 마지막 블럭이어야 한다.

* 이후에 어떤 라인도 없어야 한다.

### Error Handling도 하나의 일이다.

* 함수는 하나의 일만 해야한다.

