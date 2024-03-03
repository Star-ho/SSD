---
date: 2024-03-02T22:41:32
---
## entity manager
- entity 인스턴스의 생명주기를 관리
- hibernate에서는 entity manager를 상속한 session인터페이스가 있음
 - transaction이 생성될 때 entityManagerFactory에서 생성됨
 - transaction이 끝날 때 삭제됨
 - persist, find, merge 등의 동작이 있음

## jpa 1차 캐시
- 영속성컨텍스트에 존재하는 엔티티를 가져오는 것
- hiberante에서는 session에서 find를 호출하거나, 연관관계가 있는 엔티티에서 호출할때만 사용,
- JPQL이나 Criteria Query를 사용할떄는 사용 불가

## 2차 캐시
- 어플리케이션의 생명주기동안 유지됨
- 궁금할때 찾아볼것...


<br>[https://thorben-janssen.com/wp-content/uploads/member-access/1stLevelCache_Handout.pdf](https://thorben-janssen.com/wp-content/uploads/member-access/1stLevelCache_Handout.pdf)
[https://dzone.com/articles/how-does-spring-transactional](https://dzone.com/articles/how-does-spring-transactional)  

[https://www.ibm.com/docs/en/wasdtfe?topic=architecture-entity-manager](https://www.ibm.com/docs/en/wasdtfe?topic=architecture-entity-manager)  
[https://www.baeldung.com/jpa-hibernate-persistence-context](https://www.baeldung.com/jpa-hibernate-persistence-context)  
[https://openjpa.apache.org/builds/1.2.3/apache-openjpa/docs/jpa_overview_emfactory_perscontext.html](https://openjpa.apache.org/builds/1.2.3/apache-openjpa/docs/jpa_overview_emfactory_perscontext.html)|