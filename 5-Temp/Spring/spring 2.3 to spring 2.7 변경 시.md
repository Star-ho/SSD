---
created: 2024-03-31T22:41:00
date: 2024-04-13T22:56
---
spring version up시 httpconverter 문제가 있음

https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-Config-Data-Migration-Guide
마이그레이션 가이드

자바 17은 spring boot 2.5부터 사용가능
![Pasted image 20231204225453](real-resource-image/Pasted%20image%2020231204225453.png)


request를 Map<String,?>로 받는 사람들이 있었는데 spring 버전업하면 serialize변경사항으로 에러가 난다(해당 핸들러가 100개 이상이기에 수정하기 너무 빡셌다..)

진행하고 싶다면 아래 코드를 WebMvcConfigurer를 구현한곳에 넣자
```
@Override  
public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {  
    GsonHttpMessageConverter gsonHttpMessageConverter = new GsonHttpMessageConverter();  
    Gson gson = new GsonBuilder().create();  
    gsonHttpMessageConverter.setGson(gson);  
    converters.add(gsonHttpMessageConverter);  
}
```