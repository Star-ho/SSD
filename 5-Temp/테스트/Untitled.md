 여쭤본 @DataJpaTest는 데이터소스+JPA쪽만 컨텍스트에 올려줘서 @Service, @Repository가 붙은 클래스를 같이 주입해주기가 번거로웠고 편하게 하려면 @SpringBootTest를 올려야 하거나 구성파일을 주입해줬어야했는데요
그래서 짱구를 굴려보다가 찾은 방법이


E2E API 테스트 하지 않는 이상은 webEnvironment 속성은 사용하지 않았던걸로 기억해서요.
그래서 지금처럼 서비스, repository 등 테스트할때는 해당 속성 없이 작성했던걸로 기억해서요. (버전 올라가서 달라졌나? 싶기도하고요 ㅋㅋ)

아 아마 해당 속성 빼고 돌리셔도 정상작동하실거에요 ㅋㅋ 

webEnvironment가 NONE이면

WebMvcAutoConfiguration 이게 임포트가 안되서