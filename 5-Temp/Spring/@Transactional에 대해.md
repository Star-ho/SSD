---
date: 2023-10-30T23:26:34
updatedAt: 2024-04-21 18:34:36+2450
tags: 
---
서비스 메서드가 너무 길어서 메서드 추출을 하여 자식 메서드를 만들고 있는데, 이 때 자식 메서드에서도 부모 메서드의 영속성 컨텍스트를 그대로 사용하려면 @Transactional 걸어주면 되나요?
main logic이 tx범위고 추출한 메소드 호출하면 그냥 main tx따라갈껄요
클래스 분리를 해서 별도로 호출하면 그거는 propagation에 따라 가겠지만
클래스 분리해도 무조건 트랜잭션 있는데서만 호출할거면 그것도 안달아도 됩니다