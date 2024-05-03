---
date: 2024-04-30 22:35:11+3940
updatedAt: 2024-05-03 23:30:23+2080
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

| select_type          | JSON Name                  | Meaning                                                      |
| -------------------- | -------------------------- | ------------------------------------------------------------ |
| SIMPLE               | None                       | 서브쿼리나 Union을 사용하지 않은 간단한 Select                              |
| PRIMARY              | None                       | 가장 바깥쪽의 SELECT                                               |
| UNION                | None                       | UNION으로 결합하는 첫번째를 제외한 두번째 이후의 쿼리                             |
| DEPENDENT UNION      | dependent (true)           | UNION으로 결합하는 첫번째를 제외한 두번째 이후의 쿼리이지만 외부 쿼리의 영향을 받는 Select     |
| UNION RESULT         | union_result               | UNION의 결과일때                                                  |
| SUBQUERY             | None                       | Subquery의 첫번째 결과, From절 이외에서 사용되는 서브쿼리                       |
| DEPENDENT SUBQUERY   | dependent (true)           | 외부 쿼리에 의존하는 Subquery의 첫번째 결과,<br>From절 이외에서 사용되는 서브쿼리        |
| DERIVED              | None                       | Select쿼리의 실행결과로 메모리나 디스크에 임시 저장되는 정보                         |
| DEPENDENT DERIVED    | dependent (true)           | 다른 테이블에 의존하고 있는 DERIVED 테이블                                  |
| MATERIALIZED         | materialized_from_subquery | 서브쿼리의 내용을 임시테이블로 구체화 할때 사용                                   |
| UNCACHEABLE SUBQUERY | cacheable (false)          | 결과를 캐시할 수 없고, 외부 쿼리의 각 row에 대해 재평가가 필요한 데이터에 일때 표시됨          |
| UNCACHEABLE UNION    | cacheable (false)          | 캐시를 할 수 없는 서브쿼리를 포함하는, 첫번째를 제외한 두번째 이후의 UNION select일 경우 표시됨 |
- select쿼리가 아닌 CUD쿼리는 해당 statements의 종류가 표시됨
	- DELETE일 경우, select_type에는 DELETE를 표시

### 서브쿼리의 종류가 뭘까?
### DERIVED되는 테이블은 어떤테이블일까?
### MATERIALIZED이 나타나는 쿼리는 어떤쿼리일까?
## table
- 각 행의 결과를 가져오는 테이블의 이름
- \<union`M`,`N`>
	- id(Explain의 id 컬럼)가 M과 N인 행의 UNION결과를 나타냄
- \<derived`N`>
	- id(Explain의 id 컬럼)가 N인 쿼리의 결과로 파생된  행
	- derived테이블은 FROM에 있는 서브쿼리의 결과임
- \<subquery`N`>
	- id(Explain의 id 컬럼)가 N인 행에 대한 구체화된 subquery의 결과를 나타냄

### subquery mareirialzied 최적화 [링크](https://dev.mysql.com/doc/refman/8.0/en/subquery-materialization.html)
## partitions
- 쿼리에 의해 매치된 파티션을 나타냄
- 파티션이 없는 테이블은 NULL로 표시됨

## type(join 유형)
- join type을 나타냄
- 앞에 나올수록 성능이 좋음
- system
	- 테이블이 하나의 row만 가지고 있을때 표시됨
	- const join타입의 특별한 케이스임

- const
	- 쿼리시작시 결과가 오직 하나일때 표시됨
	- 결과가 하나의 row일 경우, 컬럼의 값은 옵티마이저에 의해 상수로 처리됨
	- const 테이블은 오직 한번만 읽기에 매우 빠름
	- 기본키 또는 UNIQUE 인덱스의 모든 부분을 상수값과 비교될때 표시됨
	- 예제 쿼리
```sql
SELECT * FROM _tbl_name_ WHERE _primary_key_=1; 
SELECT * FROM _tbl_name_ WHERE _primary_key_part1_=1 AND _primary_key_part2_=2;
```

- eq_ref
	- const와 system을 제외하고는 가장 최상의 join
	- 이전 테이블에서 가져온 행 조합마다 해당 테이블에서 정확히 한 행을 읽음
	- 인덱스의 모든 부분이 join에 사용되며, 인덱스가 기본키 또는 유니크키+not null조합이면서 `=`를 사용하여 비교될때 사용됨
	- 비교하는 값은 상수이거나, 이전에 읽은 테이블의 컬럼 사용
	- 예제쿼리
```SQL
SELECT * FROM _ref_table_,_other_table_ WHERE _ref_table_._key_column_=_other_table_._column_; 
SELECT * FROM _ref_table_,_other_table_ 
	WHERE _ref_table_._key_column_part1_=_other_table_._column_ AND _ref_table_._key_column_part2_=1;
```

- ref
	- 이전 테이블에 가져온 행 조합마다일치하는 모든 인덱스를 읽음
	- 키의 접두사만 읽거나, 키가 기본키나 유니크키가 아닐 경우 사용됨
		- 정확히 하나의 row를 반환하지 않는 경유를 의미
	- 키에 해당하는 행이 적은경우, 충분히 좋은 join 방법임
	- `=`이거나 `<=>`일때 사용됨
	- 예제쿼리
```SQL
SELECT * FROM _ref_table_ WHERE _key_column_=_expr_; 
SELECT * FROM _ref_table_,_other_table_ WHERE _ref_table_._key_column_=_other_table_._column_; 
SELECT * FROM _ref_table_,_other_table_ 
	WHERE _ref_table_._key_column_part1_=_other_table_._column_ AND _ref_table_._key_column_part2_=1;
```

- fulltext
	- FULLTEXT인덱스를 사용할때 사용됨

- ref_or_null
	- ref와 유사하지만, null을 포함하는 행의 질의를 할때 사용됨
	- subquery를 처리할때 자주 표시됨
	- 예제쿼리
```SQL
SELECT * FROM _ref_table_ WHERE _key_column_=_expr_ OR _key_column_ IS NULL;
```

- index_merge
	- 인덱스 병합 최적화일때 사용됨
	- 이 경우 Explain의 key column에는 사용된 인덱스 목록이 포함되며, key_len에는 가장 긴 인덱스의 키 목록이 표함됨
	- [링크](https://dev.mysql.com/doc/refman/8.0/en/index-merge-optimization.html)참고

- unique_subquery
	- IN절 내의 eq_ref 서브쿼리의를 대체함
	- 효율성을 높이기 위해 서브쿼리를 대체하여 인덱스만 조회함
	- 예제쿼리
```sql
value IN (SELECT primary_key FROM single_table WHERE some_expr)
```

- index_subquery
	- unique_subquery와 유사하지만, non-unique 서브쿼리일때 사용됨
	- 예제쿼리
```sql
value IN (SELECT key_column FROM single_table WHERE some_expr)
```

- range
	- 인덱스로 범위질의를 사용시 사용됨
	-  =, <>, >, >=, <, <=, IS NULL, <=>, BETWEEN, LIKE, IN() 연산자를 사용하여 상수 값과 비교할때 나타남
	- key_len에는 사용된 키 중 가장 긴키의 길이를 표시함
	- 예제쿼리
```sql
    SELECT * FROM tbl_name
      WHERE key_column = 10;
    
    SELECT * FROM tbl_name
      WHERE key_column BETWEEN 10 and 20;
    
    SELECT * FROM tbl_name
      WHERE key_column IN (10,20,30);
    
    SELECT * FROM tbl_name
      WHERE key_part1 = 10 AND key_part2 IN (10,20,30);
    ```

- index
	- 인덱스 트리가 스캔되는 것을 제외하면, ALL과 동일함
	- 아래 두가지 경우에 나타남
		- 인덱스 쿼리가 커버링 인덱스이고, 테이블에서 필요한 모든 데이터를 인덱스에서 가져올 수 있는 경우, 인덱스 트리만 스캔함
			- Extra column에 Using Index라고 나타남
			- index Only 스캔은 인덱스만 스캔하므로, 모든 테이블 데이터를 스캔하는 ALL보다 항상 빠름
		- 인덱스를 사용하여 모든 테이블 데이터를 인덱스 순서대로 접근하는 경우
			- Extra column에 Using Index라고 나타나지 않음
	- 쿼리가 단일 인덱스의 일부 열만 사용하는 경우 이 조인 유형이 나타남

- ALL
	- 이전의 모든 테이블 행 조합마다 테이블 전체 테이블을 스캔함
	- 거의 모든 경우 좋지않음
	- index를 추가하여 피할 수 있음

## possible_keys
- MySQL이 해당 테이블에서 데이터를 찾기위해 선택할 수 있는 인덱스를 보여줌
- EXPLAIN문과는 독립적이어서, possible_keys에 나타난 인덱스를 실제로 사용할 수 없을 수 있음
- 해당 행이 NULL일경우 관련 인덱스가 없다는걸 난타냄
	- 이 경우 WHERE절을 참고해 컬럼에 인덱스를 지정하여 쿼리 성능을 개선할 수 있음

## key
- 실제로 사용을 결정한 인덱스를 보여줌

## key_len
- 사용하기로 결정된 key의 길이를 나타냄

## ref
- key에서 선택된 인덱스와 비교되는 컬럼 또는 상수값을 나타냄

## rows
- MySQL이 해당 쿼리를 실행하기 위해 검사해야 한다고 생각되는 행의 수를 나타냄
- innodb의 경우 항상 추정치이며 정확하지 않을 수 있음

## filtered
- 테이블의 조건에 따라 필터링 되는 행의 수를 퍼센트로 나타낸것
- 최대값은 100이며 필터링 되지 않은 것을 의미함
- 

Real Mysql 8.0
https://dev.mysql.com/doc/refman/8.0/en/explain-output.html
https://zzang9ha.tistory.com/436