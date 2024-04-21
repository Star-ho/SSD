---
date: 2024-04-21T15:02:55
updatedAt: 2024-04-21T15:07
tags: 
---
 여쭤본 @DataJpaTest는 데이터소스+JPA쪽만 컨텍스트에 올려줘서 @Service, @Repository가 붙은 클래스를 같이 주입해주기가 번거로웠고 편하게 하려면 @SpringBootTest를 올려야 하거나 구성파일을 주입해줬어야했는데요
그래서 짱구를 굴려보다가 찾은 방법이
E2E API 테스트 하지 않는 이상은 webEnvironment 속성은 사용하지 않았던걸로 기억해서요.
그래서 지금처럼 서비스, repository 등 테스트할때는 해당 속성 없이 작성했던걸로 기억해서요. (버전 올라가서 달라졌나? 싶기도하고요 ㅋㅋ)
아 아마 해당 속성 빼고 돌리셔도 정상작동하실거에요 ㅋㅋ 

---

webEnvironment가 NONE이면
WebMvcAutoConfiguration 이게 임포트가 안되서
웹과 관련된 인프라스트럭처빈을 안올려주는걸로 .. 알고있는데
제가 잘못알고있는건가요 ㅠㅠ?

--- 

음 기억이 가물하긴한데요.
뭘 테스트하냐에 따라 다른것같긴한데요.

NONE 옵션을 사용하면 Servlet 옵션들이 적용 안되는걸로 알고 있긴합니다.
(웹과 관련된 인프라스트럭처빈이 서블릿을 의미하신거면 같은것같구요!)

보통 webEnv는 E2E 에서 톰캣과 같은 웹서버를 테스트 환경에서 수행할때 랜덤포트로 실행할것인가 고정된 포트로 실행할것인가 등으 설정할때 많이 사용하곤했었어요.

다만, 저는 위 테스트 코드 보면서 느끼는건데 
ApplicationContext가 필요한 상태에서도 왜 @DataJpaTest 가 필요한것일까? 하는 생각은 들엇습니다 ㅋㅋ

저같은경우엔

@SpringBootTest (webEnv) - E2E 테스트 작성할때
@SpringBootTest - @Service, @Component 등 비즈니스나 컴포넌트, 비즈니스 테스트할때 
@DataJpaTest - Repository / Entity 테스트 할때 
쓰긴했는데, 사실 @DataJpaTest는 거의 안썼습니다.
@DataJpaTest 는 내부적으로 @Tranasactional을 갖고 있어서 제가 선언하지 않은 트랜잭션을 테스트에 걸어줘서
Lazy Exception이 터졌어야할 상황에서도 안터지게 만들어서 

스프링 컨텍스트가 필요없는 단위 테스트의 비중을 늘리고
나머지 스프링 컨텍스트가 필요한 테스트는 모두 @SpringBootTest로 대부분 구성하긴했었어요 ㅋㅋ

그리고 제가 가능한 @MockBean 이나 다른 @xxxTest를 선호하지 않았던게,
전체 테스트 수행하면 @SpringBootTest (속성이 없는 상태)로 테스트들간에는 테스트 컨텍스트를 유지해줘서 스프링 컨텍스트가 재실행되지 않고 그대로 진행되는데,

조금이라도 다른 속성이 포함된 테스트가 잇으면 해당 테스트는 스프링 컨텍스트가 다시 실행이 되더라구요 ㅠ 
가능한 스프링 컨텍스트 재실행되는 횟수를 줄일려고 @SpringBootTest 를 좀 많이 썼던것같아요 ㅋㅋ

그래서 MockBean을 안쓰는 테스트 클래스가 있더라도 같은 레이어의 테스트는 다 상속 구조로 묶어서 동일한 빈 구성으로 가져가도록 해서 컨텍스트 캐싱하도록 많이 하는 것 같습니다.

https://stackoverflow.com/questions/22939226/how-can-i-initialize-a-spring-applicationcontext-just-once-for-all-tests
SO에 좋은 답변이있네용 ㅋㅋ 

---

네 맞습니다 ㅋㅋㅋ
관련해서 velo에도 MockBean 이 있을때는 최대한 하나으 ㅣ컨텍스트에 묶는 방법을 소개글이있네요!
https://velog.io/@bruni_23yong/%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%97%90%EC%84%9C-Spring-Application-Context%EB%A5%BC-%ED%95%9C-%EB%B2%88%EB%A7%8C-%EB%9D%84%EC%9B%8C%EB%B3%B4%EC%9E%90

오늘도 저장해두겠습니다..ㅎ 감사합니다
ApplicationContext가 필요한 상태에서도 왜 @DataJpaTest 가 필요한것일까? 라는 건 생각도 못해봤습니다
내가 필요한 컨텍스트만 올려서 핏하게 테스트해야지..에 꽂혀있었던것같아요..ㅋㅋ

@MockBean