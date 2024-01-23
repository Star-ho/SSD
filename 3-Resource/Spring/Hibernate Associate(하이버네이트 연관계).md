하이버네이트에는 연관관계가 존재함

mant-to-one
one-to-many
one-to-one
mappedBy, joinColumn

mappedBy는 @OneToMany에서 설정할 수 있는 옵션으로 many테이블에서 어떤 필드와 매핑될지 선택하는 옵션, string으로 필드명을 주거나 


fetch=EAGER가 의미가 있는 유일한 시나리오는 연관된 객체가 두 번째 수준 캐시에서 발견될 확률이 항상 매우 높다고 생각하는 경우입니다. 
