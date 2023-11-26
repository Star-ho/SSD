![[Pasted image 20231126172744.png|center|600]]

### Filter
- 모든 request에 적용되는 필터
- 설정을 통해 특정 path로 갈때, 우선순위 등 여러 설정 가능

### DispatcherServlet
- request를 분석하여 처리를 위해 적절한 컨트롤러로 보냄
- 스프링은 FrontController패턴을 사용하여 하나의 Servlet(DispatcherServlet)만 사용
	- 여러 Servlet을 사용할경우 중복코드가 생성되기에 하나의 Servlet에서 요청을 처리함







https://justforchangesake.wordpress.com/2014/05/07/spring-mvc-request-life-cycle/

#argent