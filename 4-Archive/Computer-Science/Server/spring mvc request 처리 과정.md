![[Pasted image 20231125233607.png|center|600]]

### Filter
- Dispatcher Servlet으로 가기전 적용되는 필터
- 모든 request에 적용되는 필터
- 설정을 통해 특정 path로 갈때, 우선순위 등 여러 설정 가능

### DispatcherServlet
- request를 분석하여 처리를 위해 적절한 컨트롤러로 보냄
- 스프링은 FrontController패턴을 사용하여 하나의 Servlet(DispatcherServlet)만 사용
	- 여러 Servlet을 사용할경우 중복코드가 생성되기에 하나의 Servlet에서 요청을 처리함
	- 스프링은 하나의 Dispatcher Servle만 생성 [참고링크](https://stackoverflow.com/questions/23049736/working-with-multiple-dispatcher-servlets-in-a-spring-application)
### Hander Mapping
- request와 handler

### View Reslover
- 전달받은 view





https://justforchangesake.wordpress.com/2014/05/07/spring-mvc-request-life-cycle/

#argent