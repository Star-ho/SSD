---
created: 2023-10-04T22:56:42
date: 2024-04-09T23:39
updated: 2024-03-31T22:43
---
## Fixture
- 소프트웨어를 일관되게 테스트 할 수 있게 해주는 장치
- 테스트를 실행하고, 특정결과를 예상하기 위해 필요한 모든것 [링크](http://xunitpatterns.com/test%20fixture%20-%20xUnit.html)
- 테스트 더블과는 다른 용어임

> SUT(System Under Test)
> 우리가 테스트하고 싶어하는 모든것, 테스트 관점에서 정의됨
> 단위테스트를 작성할 때는 테스트를 하는 클래스(CUT), 객체(OUT), 메서드(OUT), 
> 통합 테스트를 작성할때는 어플리케이션(AUT)

## Test Double
- 테스트 목적으로 실제 객체 대신 올 수 있는 모든 종류의 객체를 의미함
- 테스트를 진행하기 어려운 경우, 이를 대신해 테스트를 진행할 수 있도록 만들어 주는 객체
> 영화 촬영시 위험한 역할을 대신한느 스턴트 더블에서 비롯됨
- Dummy Object, Test Stub, Test Spy, Mock Object, Fake Object 과 같은 구현이 존재함

![center](Pasted%20image%2020240409231740.png)
## Dummy
- SUT의 메소드 시그니처에 필요한 객체들
- 테스트에 영향은 가지 않지만, SUT 메소드 시그니처에 필요한 객체
- null 오브젝트, 하드코딩된 값들
> 실제로 테스트에 영향이 가지않아, Test Double로 보지않는 의견도 있음

## Test Stub
- SUT가 의존하는 실제 컴포넌트를 대체하기 위해 사용
- 실제 컴포넌트를 대체하여 간접적인 입력에 대해 제어할 수 있음

## Spy
- 
## Mock

## Fakes



https://martinfowler.com/articles/mocksArentStubs.html
http://xunitpatterns.com/Test%20Double.html
#Test-Double
