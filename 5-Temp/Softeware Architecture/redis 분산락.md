분산락을 쓰는 이유
한가지 작업을 하나의 프로세스에 맡기기 위해
같은 작업을 동시에 하는걸 방지하기 위해=

1. 레디스 분산락을 실수로 걸지 않거나 잘못거는 휴먼에러 가능성 높음
2. 레디스 분산락은 동일 키(단일키)에 대한 락만 걸 수 있음.

동일 리소스에 대해 a,b,c 행위로 변경이 가능하가면 레디스 분산락으론 저 모든 행위를 동일한 키로 락 잡아야하는데 그게 잘 관리되기 어려움

비관적 락은 트랜잭션이 복잡해지고 잠금 거는 레코드에 대해 여러 곳에서 동시다발적으로 접근하면 같은 api 잠금 뿐만 아니라 데드락 위험이 발생


https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html