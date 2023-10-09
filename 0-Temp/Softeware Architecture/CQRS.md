- 소프트웨어의 복잡성을 해결하는 방법중 하나
- 메서드를 Query와 Command로 구분하자
- 왜?
- CQRS는 side effect 어떻게 다룰까에 대한 문제임
- query는 순전히 조회만을 하는 메서드이므로 side effect가 없
	- 리턴값이 존재함
	- command에서 사용할 수 있음
- commnd는 특정한 객체를 변경하는 메서드이므로 side effect가 존재
	- 리턴값이 없음
	- query에서 사용할 수 없음
- 하지만 command임에도 리턴값이 필요한 상황이 존재한다
- ex) 최종 변경사항을 리턴해줘야하는 경우
- command라는 네이밍을 가지고 메서드명도 충분히 command라는걸 표현함에도 이걸 쿼리처럼 사용하는 사람이 문제

> Query
> - 하나의 값을 받아서 어떠한 처리를 하는 함수
> - Procedure에서 호출될 수 있음

> Procedure
> - 하나의 값을 받아서 결과를 리턴해주는 함수
> - Query에서 호출할 수 없음
> 	- query에서는 side effect가 생기면 안되기 때문



https://blog.ploeh.dk/2014/08/11/cqs-versus-server-generated-ids/

#Software-design 