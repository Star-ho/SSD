---
date: 2024-05-03 23:35:47+8830
updatedAt: 2024-05-04 22:02:09
---
- Extra 열에는 Mysql에서 쿼리를 resolve하기 위한 추가적인 정보가 들어감
- 여기서는 추가적인 정보 중 유용하다고 생각되는 정보를 정리할 예정
- 전체 정보는 다음 [링크]를 참고할것

## Using index
- 커버링 인덱스가 사용되었음을 의미함
- 실제 테이블데이터를 읽지 않고, 인덱스만 조회함
- 쿼리가 하나의 인덱스에서 조회에 필요한 모든 데이터를 가지고 있을경우 사용됨
## Using index condition
- 인덱스를 먼저 읽은 후 필요할 경우 테이블 데이터를 읽음
- 테이블 데이터를 필요할때 까지 읽는것을 미룸
- [링크](https://dev.mysql.com/doc/refman/8.0/en/index-condition-pushdown-optimization.html)참고

## Using index for group-by
- Using index와 유사하게, 테이블을 
#### **Using temporary**
#### **Using index for skip scan**
#### **12.5 Using join buffer(Block Nested Loop, hash join)**

#### **Using where**