# RIBs_Example
RIBs without RxSwift

RIBs
RIBs는 Uber에서 만든 cross-platform 모바일 아키텍쳐 프레임워크이다.

cross-platform이라는 말답게, AOS, iOS 둘 다 지원을 한다.

RIBs는 Router, Interactor, Builder의 약자이다.

많은 엔지니어(개발자) + nested states(중첩된 상태)의 모바일 앱을 위해 설계되었다고 한다.

RIBs를 통해 다음과 같은 일을 할 수 있다.

- Encourage Cross-Platform Collaboration: 
앱의 복잡한 부분은 iOS, Android에서 비슷비슷하다. RIBs는 iOS, Android에 대해 유사한 개발 패턴을 제공하기 때문에, 공동으로 디자인된 단일 아키텍쳐를 iOS, Android간에 공유할 수 있다. 그러면 iOS <-> Android 팀이 비즈니스 로직 코드를 교차 검토 할 수 있는 장점이 생길 수 있다.
 
- Minimize Global States and Decisions:
Global state변경은 예측할 수 없는 동작을 유발하며, 이걸 변경했다고 해서 이 변경이 미칠 영향들을 엔지니어가 전부 알 수 없다.
RIBs는 잘 격리된(well-isolated) 개별 RIBs의 deep hierarchy내에서 상태를 캡슐화하여, Global state 문제를 방지하도록 권장한다.
 
- Testability and Isolation: 
Class는 Unit Test가 쉬워야합니다. 개별 RIB클래스에는 별도의 "책임"이 있다. 이 책임에는 Routing, Business Logic, View Logic, 다른 RIB 클래스 생성 등이 있어요. 부모 RIB 논리는 자식 RIB 논리와 분리되어(decoupled) 있습니다. 따라서 RIB 클래스를 쉽게 테스트하고 독립적으로 추론할 수 있다. 
 
- Tooling for Developer Productivity: 
non-trivial(사소한?) 아키텍쳐 패턴을 채택한다고 해서 강력한 툴링(tooling) 없이는 소규모 어플리케이션을 넘어서 확장되지 않는다. RIBs에는 코드 생성, 정적 분석 및 runtime integrations에 대한 IDE 툴링이 함께 제공되며, 이 툴은 크고 작은 팀의 개발자 생산성을 향상시킨다.

- Open-Closed Principle: 개발자는 가능하면 기존 코드를 수정하지 않고 새로운 기능을 추가 할 수 있어야 한다. 예를들어 부모 RIB을 거의 변경하지 않고 부모의 종속성이 필요한 복잡한 자식 RIB을 attach하거나 build할 수 있다.

- Structured around Business Logic: 
앱의 비즈니스 로직 구조는 UI의 구조를 엄격하게(또는 절대적으로) 반영할 필요는 없다. 예를들어 애니메이션 및 view 성능을 용이하게하기 위해서 View 계층 구조는 RIB 계층 구조보다 더 얕을 수(shallower) 있습니다. 
또는 단일 기능 RIB이 UI의 다른 위치에 나타나는 세가지..View의 모양을 제어할 수 있다.
 
- Explicit Contracts:
Requirements(요구사항)은 compile-time safe contracts(컴파일 타임 안전 계약.....???)으로 선언해야 한다.
클래스 종속성과 순서(ordering) 종속성이 충족되지 않으면 클래스는 컴파일되지 않아야 합니다. 우리는 ReactiveX를 사용하여 순서 의존성을 나타내며, 클래스 의존성을 나타내기 위해 type safe dependency injection (DI) 시스템과 data invariants의 생성을 장려하기 위해 많은 DI scopes를 나타냅니다. 

