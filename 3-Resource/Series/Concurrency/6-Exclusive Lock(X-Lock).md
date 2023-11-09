- X-Lock이 걸린 객체에 대해 다른 트랜잭션에서 읽기, 쓰기 불가능
- X-Lock이 걸린 객체에 대해 다른 객체에서 S-Lock, X-Lock 걸수 없음

- 변경 또는 삭제를 위해 락을 걸떄 활용
 [`SELECT ... FOR UPDATE`](https://dev.mysql.com/doc/refman/8.0/en/select.html "13.2.13 SELECT Statement")문으로 X-lock을 걸 수 있음