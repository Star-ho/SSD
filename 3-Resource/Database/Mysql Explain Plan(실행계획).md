---
date: 2024-04-30 22:35:11+3940
updatedAt: 2024-04-30 22:43:29+6360
---
## 개요
- Explain 문은 Mysql이 어떻게 statements를 실행할것인가에 대한 정보를 제공
	- select, delete, insert, replace, update문에 적용 가능
- 출력에 테이블이 나열되는 순서는, Mysql이 statements를 처리하는 동안 테이블을 읽는 순서임
	- 첫번째 테이블에서 행을 읽고, 두번째테이블에서 일치하는 행을 찾고, 세번째에서 또 찾는 방식임
- 모든 테이블이 처리되면 Mysql은 선택한 열을 출력하고, 더 많은 행을 찾기 찾을 때 까지 테이블 목록을 역추적함





Real Mysql 8.0
https://dev.mysql.com/doc/refman/8.0/en/explain-output.html
https://zzang9ha.tistory.com/436