---
created: 2023-10-04T23:03
date: 2024-03-18T00:17
updated: 2024-03-31T22:43
---
컴파일러의 도움 없이 Java 애플리케이션의 런타임 동안 Java 클래스를 생성 및 수정하기 위한 코드 생성 및 조작 라이브러리

```
Class<?> dynamicType = new ByteBuddy()
  .subclass(Object.class)
  .method(ElementMatchers.named("toString"))
  .intercept(FixedValue.value("Hello World!"))
  .make()
  .load(getClass().getClassLoader())
  .getLoaded();
 
assertThat(dynamicType.newInstance().toString(), is("Hello World!"));
```

위 방법으로 toString함수를 변경가능하다

> jpa에 ByteBuddy관련한 내용이 나와서 찾아봤는데 추후 더 찾아봐야겠다.  
> [https://stackoverflow.com/questions/30769816/how-do-i-use-byte-buddy-to-create-a-lazy-loading-class](https://stackoverflow.com/questions/30769816/how-do-i-use-byte-buddy-to-create-a-lazy-loading-class)

[https://bytebuddy.net/#/](https://bytebuddy.net/#/)

#Byte-Buddy
#Java 
#Tool 