### 조회할때 mybatis, querydsl, 생성, 수정, 삭제시 jpa이용?
- jpa보다는 생성, 수정, 삭제는 하나의 어그리게이트에서 이용되어야 하며, 불변식은 하나의 aggregate에서 이루어져야 하므로 하나의 객체가 되어야한다.
- 하나의 객체로만 매핑이 된다면 반드시 jpa일필요가 없다.
- 단, 조회할때 도메인로직이 필요할땐 어떻게할 것인가?
	- 도메인로직을 중복으로 가져간다 - 조회가 많고 성능이 중요할때
		- vo를 이용하는건 어떨까?
	- 협력을 이용
	- 조회할때 도메인 entity도 가져와서 사용 - 성능이 중요하지 않을때