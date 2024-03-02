---
date: 2024-01-25T13:19:01
---
## 영속성전이

- cascade
	- 부모 엔티티를 영속성 관리시 자식 엔티티도 같이 영향을 끼치게 하는것
	- ALL, PERSIST, REMOVE, MERGE, REFERESH, DETACH
- orphanRemoval
    - 부모엔티티 삭제시 자식 엔티티를 삭제하는것을 포함
    - 부모엔티티의 자식엔티티 리스트에서 제거하는 것으로도 자식엔티티를 삭제

## 프록시객체
- lazy로딩을 구현하기 위해 사용
- lazy로딩을 사용하면 실제 객체를 사용할때 데이터베이스에서 조회함
- 프록시 객체는 실제로 값을 가지고 있지 않고 데이터를 로딩하기 위한 정보만 가지고 있음
- getReference메서드로 프록시 객체를 가져옴

[https://vladmihalcea.com/how-does-a-jpa-proxy-work-and-how-to-unproxy-it-with-hibernate/](https://vladmihalcea.com/how-does-a-jpa-proxy-work-and-how-to-unproxy-it-with-hibernate/)

#JPA 
#transitive-persistence
#Proxy-Object
#영속성전이
#프록시객체