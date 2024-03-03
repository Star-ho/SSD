---
created: 2024-03-02T22:41:32
updated: 2024-03-03T11:41
---
- 주어진 요청의 컨텍스트 내에서 메서드 매개 변수를 인수 값으로 해석하는 전략을 제공하는 Spring의 인터페이스
- 아래의 두 메서드가 있음

### supportsParameter
- 해당 파라미터가 다른 변경이 일어나야 하는지 여부를 판단하는 파라미터입니다
	- 해당 파라미터를 변경여부를 판단
### resolveArgument
- 메서드의 주어진 파라미터를 resolve함
	- handler의 파라미터를 변경함

https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/method/support/HandlerMethodArgumentResolver.html

#Spring
#HandlerMethodArgumentResolver