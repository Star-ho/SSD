---
date: 2024-04-30 22:35:11+3940
updatedAt: 2024-04-30 23:08:10+5120
---
## 개요
- Explain 문은 Mysql이 어떻게 statements를 실행할것인가에 대한 정보를 제공
	- select, delete, insert, replace, update문에 적용 가능
- 출력에 테이블이 나열되는 순서는, Mysql이 statements를 처리하는 동안 테이블을 읽는 순서임
	- 첫번째 테이블에서 행을 읽고, 두번째테이블에서 일치하는 행을 찾고, 세번째에서 또 찾는 방식임
- 모든 테이블이 처리되면 Mysql은 선택한 열을 출력하고, 더 많은 행을 찾기 찾을 때 까지 테이블 목록을 역추적함

## Explain Output Columns
| Column        | JSON Name     | Meaning               |
| ------------- | ------------- | --------------------- |
| id            | select_id     | Select 식별자            |
| select_type   | None          | Select Type           |
| table         | table_name    | 결과 행을 가져오는 테이블        |
| partitions    | partitions    | 매칭되는 파티션              |
| type          | access_type   | join 유형               |
| possible_keys | possible_keys | 선택될 수 있는 인덱스          |
| key           | key           | 실제로 선택된 인덱스           |
| key_len       | key_length    | 선택된 키의 길이             |
| ref           | ref           | 인덱스와 비교한 열            |
| rows          | rows          | 예상되는 행의 추정치           |
| filtered      | filtered      | 테이블 조건에 따라 필터링된 행의 비율 |
| Extra         | None          | 추가정보                  |
## id 
- Select의 식별자로, 쿼리 내 Select의 일련 번호
- 다른행 의 유니온 결과를 참조하는 경우 Null일수 있음
	- 이 경우 table Column은 <union M,N> 으로 나타남

## select_type
- Select의 유형으로 다음 표에 나타나는 것중 하나가 들어감

| select_type          | JSON Name                  | Meaning                                                                                                   |
| -------------------- | -------------------------- | --------------------------------------------------------------------------------------------------------- |
| SIMPLE               | None                       | 서브쿼리나 Union을 사용하지 않은 간단한 Select                                                                           |
| PRIMARY              | None                       | 가장 바깥쪽의 SELECT                                                                                            |
| UNION                | None                       | UNION으로 결합하는 첫번째를 제외한 두번째 이후의 쿼리                                                                          |
| DEPENDENT UNION      | dependent (true)           | UNION으로 결합하는 첫번째를 제외한 두번째 이후의 쿼리이지만 외부 쿼리의 영향을 받는 Select                                                  |
| UNION RESULT         | union_result               | UNION의 결과를 담아두는 테이블                                                                                       |
| SUBQUERY             | None                       | Subquery의 첫번째 결과                                                                                          |
| DEPENDENT SUBQUERY   | dependent (true)           | 외부 쿼리에 의존하는 Subquery의 첫번째 결과                                                                              |
| DERIVED              | None                       | Derived table                                                                                             |
| DEPENDENT DERIVED    | dependent (true)           | Derived table dependent on another table                                                                  |
| MATERIALIZED         | materialized_from_subquery | Materialized subquery                                                                                     |
| UNCACHEABLE SUBQUERY | cacheable (false)          | A subquery for which the result cannot be cached and must be re-evaluated for each row of the outer query |
| UNCACHEABLE UNION    | cacheable (false)          | The second or later select in a UNION that belongs to an uncacheable subquery (see UNCACHEABLE SUBQUERY)  |

Real Mysql 8.0
https://dev.mysql.com/doc/refman/8.0/en/explain-output.html
https://zzang9ha.tistory.com/436