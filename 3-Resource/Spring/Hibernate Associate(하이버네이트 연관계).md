하이버네이트에는 연관관계가 존재함

mant-to-one
one-to-many
one-to-one
mappedBy, joinColumn

one쪽
mappedBy는 @OneToMany에서 설정할 수 있는 옵션으로 many테이블에서 어떤 필드와 매핑될지 선택하는 옵션, string으로 필드명을 주거나 enum으로 줄 수 있음
mappedBy대신 joinColumn으로 many테이블의 어떤 컬럼과 매핑할지 선택할 수 있음

many쪽
joinColumn

연관관계의 주인
주인이 되면 뭐가좋냐?
주인쪽에서만 관계 설정이 가능하다
many쪽이 주인일때 list.add()로 연관관계 설정가능
- team=team으로 연관관계 설정 불가
one쪽이 주인일때 team=team으로 연관관계 설정가능
- list.add()로 연관관계 설정불가

모든 양방향연관관계에서는 자식측이 주인이되며, 

꺠알팁
oneToMany, manyToOne설정된 필드에는 Column어노테이션 불가, joinColumn사용해야함


fetch=EAGER가 의미가 있는 유일한 시나리오는 연관된 객체가 두 번째 수준 캐시에서 발견될 확률이 항상 매우 높다고 생각하는 경우입니다. 


https://docs.jboss.org/hibernate/orm/6.4/introduction/html_single/Hibernate_Introduction.html#associations
https://docs.jboss.org/hibernate/orm/6.4/userguide/html_single/Hibernate_User_Guide.html#associations-many-to-one