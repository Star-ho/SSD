---
created: 2023-09-30T14:43:28
updated: 2024-03-08T23:21
---
```
@AutoConfiguration(after = { ReactiveWebServerFactoryAutoConfiguration.class, CodecsAutoConfiguration.class,
		ReactiveMultipartAutoConfiguration.class, ValidationAutoConfiguration.class,
		WebSessionIdResolverAutoConfiguration.class })
@ConditionalOnWebApplication(type = ConditionalOnWebApplication.Type.REACTIVE)
@ConditionalOnClass(WebFluxConfigurer.class)
@ConditionalOnMissingBean({ WebFluxConfigurationSupport.class })
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE + 10)
public class WebFluxAutoConfiguration {

    ... 생략

}
```

WebFluxAutoConfiguration에서 결정

둘다 dependency가 걸려있다면  
@EnableWebFlux를 통해 설정가능

EnableWebMvc도 존재함!  
but 둘다 의존한다면 mvc가 우선됨  
좀 더 명확하게 해주려는 의도가 있는거 같다

---

[https://mangkyu.tistory.com/257](https://mangkyu.tistory.com/257)  
[https://stackoverflow.com/questions/54069614/springwebflux-error-with-enablewebflux-annotation](https://stackoverflow.com/questions/54069614/springwebflux-error-with-enablewebflux-annotation)

#Spring 
#Reactive
#Tip