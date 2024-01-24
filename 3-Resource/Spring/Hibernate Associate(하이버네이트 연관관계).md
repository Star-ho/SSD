## 연관관계의 소유
- 단방향에서는 소유하는 쪽만 존재
- 양방향에서는 소유하는쪽과 그 반대쪽 둘다 존재
	- manyToOne에서는 many쪽이 소유측을 가지고 있음
	- oneToOne에서는 외래키가 있는쪽이 소유측임
	- ManyToMnay에서는 둘 다 소유측이 될 수 있음
- mappedBy로 관계의 소유자인 엔티티의 속성 또는 필드를 지정함

## Cascade
- ALL, DETACH, MERGE, PERSIST, REFRESH, REMOVE 가 있으며 ALL은 다른 모든 속성을 포괄하는 개념
- 부모엔티티의 변경이 발생할때 자식까지 전파할건지에 대한 여부
> ex) CascadeType.Merge가 지정된경우 부모가 merge되면 자식도 merge됨

one쪽
mappedBy는 @OneToMany에서 설정할 수 있는 옵션으로 many테이블에서 어떤 필드와 매핑될지 선택하는 옵션, string으로 필드명을 주거나 enum으로 줄 수 있음
mappedBy대신 joinColumn으로 many테이블의 어떤 컬럼과 매핑할지 선택할 수 있음

many쪽
joinColumn

연관관계의 주인
관계 설정을 하는 엔티티를 말함
many쪽이 주인일때 list.add()로 연관관계 설정가능
- team=team으로 연관관계 설정 불가
one쪽이 주인일때 team=team으로 연관관계 설정가능
- list.add()로 연관관계 설정불가

양방향일때
child쪽에서만 연결하면 insert한번
paren쪽에서만 연결하면 insert한번 update한번

깔끔하게하려면 부모자식쪽에서 둘다 연결하는게 합리적임
flush해도 부모쪽 캐시는 남아있음

cascade는 부모쪽에서 하는게 합리적이다

꺠알팁
oneToMany, manyToOne설정된 필드에는 Column어노테이션 불가, joinColumn사용해야함


fetch=EAGER가 의미가 있는 유일한 시나리오는 연관된 객체가 두 번째 수준 캐시에서 발견될 확률이 항상 매우 높다고 생각하는 경우입니다. 


https://docs.jboss.org/hibernate/orm/6.4/introduction/html_single/Hibernate_Introduction.html#associations
https://docs.jboss.org/hibernate/orm/6.4/userguide/html_single/Hibernate_User_Guide.html#associations-many-to-one
https://docs.oracle.com/javaee/7/tutorial/persistence-intro001.htm#JEETT01154