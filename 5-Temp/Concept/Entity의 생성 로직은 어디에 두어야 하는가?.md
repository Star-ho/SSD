---
date: 2024-04-07T23:04:11
updatedAt: 2024-04-21 18:32:05+2560
tags: 
---
* Entity 생성로직을 Entity에 두는 것(XxxEntity.of(~)) vs. RequestDTO에 두는 것(requestDto.toEntity())

- Entity에 두는 것(XxxEntity.of(~))
-- 장점
--- Entity를 생성하는 방법은 Entity가 정한다. 내가 제일 잘 알고있으니 내가 정하고 그 방법으로만 사용하게 하겠다. (객체지향적, 높은 응집도, 생성방법 오용 불가능)
--- DTO와는 달리 Entity의 필드와 메서드(RequestBody 필드의 암/복호화, 포맷팅 등의 변환)를 사용하는 것도 가능하다.

-- 단점
--- 코드상으로 엔티티가 API 스펙에 의존성이 생긴다.중요한 것(Entity)이 덜 중요한 것(DTO)에 의존한다. 하지만 API 스펙 변경이 엔티티에 영향을 주는 것이라면 이 편이 자연스러울 수도 있다.
--- 동일 생성자를 사용하는 여러 API가 있을 때 서로 영향받을 수 있는데 이를 분리하는게 어렵다? => 생성자를 공유하던 API 중에 일부 API의 스펙이 바뀐다면 해당 API는 원래 새로운 스펙의 DTO가 필요한 것이므로 무관하다.

- RequestDTO에 두는 것(requestDto.toEntity())
-- 단점
--- 생성자를 외부에 노출하지 않을 수 있다. (이건 DTO를 Entity와 같은 패키지에 넣는다면 해결은 가능하지만, 그런 패키지 구조가 썩 좋은 거 같지는 않다. 그리고 이렇게 하더라도 패키지 내에서의 최소한의 생성자 노출은 막을 수 없다.)
--- DTO에 toEntity를 넣으면 Entity 변경시 DTO 변경을 대응하는 것을 잊기 쉽다. (API 스펙이 변경되는 것이 아니라면 굳이 대응이 되지 않아도 될지도)

- Entity에 정적생성자(개별 필드를 받는)를 만들고, RequestDTO에 toEntity를 만들고 toEntity에서 정적생성자를 사용하면 Entity가 DTO에 갖던 의존성은 없어지고, 생성자도 노출하지 않을 수 있다.
다만 toEntity에서 모든 유형의 Entitization을 처리해야하므로, Entity의 정적생성자를 오버로딩하면 사용하기가 까다롭다. (필드 값에 따라 다른 생성자 호출이 필요하므로 분기가 필요)
따라서 모든 필드를 아우르는 하나의 정적생성자를 사용하고 그 안에서 필드 값에 따른(대부분의 경우, 필드값 유무에 따른) 분기처리를 해야한다.

---

정적팩터리메서드의 네이밍과 사용자 정의 오브젝트가 아닌 래퍼클래스들로 구성하고 
파라미터 오브젝트로 서빙하면서 통해 엔티티의 정적팩터리메서드의 파라미터 리스트에 구조분해시켜 생성한다가 저의 그라운드 룰입니당

파라미터 리스트가 너무많다면 값 객체로 랩핑해서 타입안정성을 챙기려고하고잇어요

아 비즈니스 수준의 유효성 검사는 저는 또.. ***Validator라고 만들어서씁니다 -ㅅ-..ㅋㅋ;

--- 

API 스펙이 변경 될 때 프레젠테이션 DTO 의존성이 깊게 잡혀있으면 경험상 불편했던 적이 많았던 적이 있었어서 요건 어떠신지 여쭤보고 싶었습니다. 

말씀하시는 중복되는 보일러플레이트 코드에 관해서는. 우형 기술블로그에서 "클린 아키텍처" 내용에 있는 진짜 중복과 우발적 중복에 대해서 설명한게 있는데 제 생각에는 해당 아티클이 자낳퇴님에게 도움이 될수도 있을 것 같습니다. 

의견 감사합니다!! 