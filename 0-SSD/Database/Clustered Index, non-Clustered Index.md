## Clustering Index

- 데이터가 물리적으로 저장될떄 정렬 방식을 정의
- 테이블당 하나만 존재 가능
- 기본키 제약조건이 걸린 컬럼에 자동으로 생성됨

## non-Clustering Index

- 데이터를 물리적으로 정렬하지 않음
- 테이블과 다른 물리적 공간에 저장됨
- 테이블에 여러개가 존재 가능
- 유니크 제약조건에 걸린 컬럼에 자동으로 적용됨
- 너무 많이 생성시 생성, 수정, 삭제의 오버헤드가 커짐

[https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)

[https://learn.microsoft.com/ko-kr/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described?view=sql-server-ver16](https://learn.microsoft.com/ko-kr/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described?view=sql-server-ver16)

[https://gwang920.github.io/database/clusterednonclustered/](https://gwang920.github.io/database/clusterednonclustered/)

#Database
#Definition
#Innodb 