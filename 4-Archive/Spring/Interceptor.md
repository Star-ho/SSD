handlerMapping의 구현으로 특정요청에 대해 특정 기능을 적용할때 사용합니다
아래 3가지 메소드가 존재합니다
 
### preHandle 
- 핸들러가 실행되기 전 실행됩니다
- boolean을 리턴하는데, true를 리턴하면 이후 실행이 계속되지만, false나 예외를 리턴하면 이후의 interceptor 및 핸들러를 실행하지 않습니다
### postHandle 
- 핸들러가 실행된 후 실행됩니다
### afterCompletion 
- 모든 완료된 후 실행됩니다

## vs Filter
- Filter와의 차이점으로 Filter는 Dispatcher Servlet이 실행되기전 적용됩니다
- Interceptor는 Dispatcher Servlet이 실행된 후 호출이 됩니다
- Filter는 전체 수명주기 대상하는 작업에 적합함


> webflux에서는 webfilter가 동일한 기능을 제공함

https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/handlermapping-interceptor.html
https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/interceptors.html
https://gngsn.tistory.com/153
https://docs.spring.io/spring-framework/reference/web/webflux/reactive-spring.html#webflux-filters

#Spring 
#Interceptor