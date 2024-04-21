---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:52+8140
tags: 
---
  
InnoDB는 조회할 때 해당 row에 lock이 걸려있는지 다음과 같은 방법으로 확인합니다.

- **Read View:** InnoDB는 조회하는 트랜잭션에 대해 Read View를 생성합니다. Read View는 조회 시점의 데이터베이스 상태를 캡처한 것입니다. Read View를 생성할 때 InnoDB는 해당 row에 걸려있는 lock을 확인합니다.
- **Lock Info:** InnoDB는 각 row에 Lock Info를 저장합니다. Lock Info에는 row에 걸려있는 lock의 유형과 트랜잭션 ID가 포함됩니다. 조회할 때 InnoDB는 해당 row의 Lock Info를 확인하여 lock이 걸려있는지 여부를 확인합니다.

InnoDB는 Read View와 Lock Info를 사용하여 조회할 때 해당 row에 lock이 걸려있는지 확인합니다.

**Read View를 통한 lock 확인**

InnoDB는 조회하는 트랜잭션에 대해 Read View를 생성합니다. Read View는 조회 시점의 데이터베이스 상태를 캡처한 것입니다. Read View를 생성할 때 InnoDB는 해당 row에 걸려있는 lock을 확인합니다.

Read View를 생성하는 단계는 다음과 같습니다.

1. InnoDB는 조회하는 트랜잭션의 트랜잭션 ID를 가져옵니다.
2. InnoDB는 해당 트랜잭션 ID보다 이전에 생성된 모든 lock을 확인합니다.
3. InnoDB는 Read View에 해당 lock을 포함합니다.

예를 들어, 트랜잭션 T1이 row A에 X lock을 걸고 있는 상태에서 트랜잭션 T2가 row A를 조회한다고 가정합니다. InnoDB는 트랜잭션 T2의 Read View를 생성할 때 트랜잭션 T1의 X lock을 포함합니다. 따라서 트랜잭션 T2는 row A를 읽을 수 있지만 수정할 수는 없습니다.

**Lock Info를 통한 lock 확인**

InnoDB는 각 row에 Lock Info를 저장합니다. Lock Info에는 row에 걸려있는 lock의 유형과 트랜잭션 ID가 포함됩니다. 조회할 때 InnoDB는 해당 row의 Lock Info를 확인하여 lock이 걸려있는지 여부를 확인합니다.

Lock Info를 확인하는 단계는 다음과 같습니다.

1. InnoDB는 조회하는 row의 Lock Info를 가져옵니다.
2. InnoDB는 Lock Info에 포함된 lock의 유형과 트랜잭션 ID를 확인합니다.
3. InnoDB는 해당 lock이 조회 트랜잭션의 lock과 충돌하는지 여부를 확인합니다.

예를 들어, 트랜잭션 T1이 row A에 X lock을 걸고 있는 상태에서 트랜잭션 T2가 row A를 조회한다고 가정합니다. InnoDB는 row A의 Lock Info를 확인하여 트랜잭션 T1의 X lock을 발견합니다. 이 경우 트랜잭션 T2는 row A를 읽을 수는 있지만 수정할 수는 없습니다.

InnoDB는 Read View와 Lock Info를 사용하여 조회할 때 해당 row에 lock이 걸려있는지 확인합니다.

#wait-to-update 