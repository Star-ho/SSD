handlerMapping의 구현으로 특정요청에 대해 특정 기능을 적용할때 사용합니다
아래 3가지 메소드가 존재합니다
 
### preHandle 
- 핸들러가 실행되기 전 실행됩니다
- 리턴으로 
### postHandle 
- 핸들러가 실행된 후 실행됩니다
### afterCompletion 
- 모든 완료된 후 실행됩니다

## vs Filter
- Filter와의 차이점으로 Filter는 Dispatcher Servlet이 실행되기전 적용됩니다
- Interceptor는 Dispatcher Servlet이 실행된 후 호출이 됩니다
- 이로인해 Filter에서는 Spring의 기능들을 사용할 수 없지만, Interceptor는 Spring

webflux에서는 webfilter가 동일한 기능을 제공함


https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/handlermapping-interceptor.html
https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/interceptors.html
https://gngsn.tistory.com/153
https://docs.spring.io/spring-framework/reference/web/webflux/reactive-spring.html#webflux-filters