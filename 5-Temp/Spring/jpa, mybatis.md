---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:23:53+8630
---
1 저장 (jpa)
2 flush
3 조회 (mybatis)
4 삭제 (jpa)
5 flush
6 조회 (mybatis)

이렇게 했을 때, 마지막 6번에서 삭제되었어야 할 데이터가 여전히 조회되는 현상이 있어서 하루 종일 고생했는데, 결론은 제가 mybatis에 대한 이해가 부족해서 였습니다.
jpa가 영속성 컨텍스트를 관리하는 것처럼 mybatis도 sqlsession으로 세션을 관리하는데, 거기 캐시가 남아서 계속 조회가 됐던 거였어요.

1 저장 (jpa)
2 flush
3 조회 (mybatis)
4 삭제 (jpa)
5 flush
6 chacheClear★
7 조회 (mybatis)

이렇게 하니까 정상적으로 테스트 케이스 통과했습니다.

JPA만 쓰면 좋은데, 수행사에서 JPA를 사용하는 게 미숙하다보니 조회를 다 mybatis로 구현해놔서,,,ㅜㅜ 