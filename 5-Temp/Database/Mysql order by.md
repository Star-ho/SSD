---
created: 2023-12-03T23:10:30
updated: 2024-03-03T11:41
---
Mysql order by 동작관련해서 질문이 있는데요~!

Mysql에서 order by를 수행 할 때 sort_buffer_size는 정렬을 할때 사용되는 버퍼사이즈고, 정렬된 데이터들을 sort_buffer_size 만큼 read_rnd_buffer에 저장 한후 
read_rnd_buffer_size 만큼 정렬된 데이터를 반복해서 사용자에게 보여주는 식으로 동작하는게 맞을까요? 

sort_buffer는 정렬해야 할 튜플들이 저장되는 버퍼인데, MySQL 서버의 정렬은 크게 2가지 방식이 있어요. 
1) 정렬 대상 키와 레코드 주소(innodb의 경우 PK)만 sort_buffer에 담아서 정렬하는 방식
2) 쿼리에서 필요한 모든 컬럼으로 구성된 튜플을 sort_buffer에 담아서 정렬하는 방식

2번의 경우는 read_rnd_buffer와는 무관하지만, 1번의 경우 정렬된 결과를 이용해서 (쿼리에서 필요한 컬럼들을 가져오기 위해서) 다시 레코드를 가져와야 하는데, 이때 read_rnd_buffer는 읽어야 할 레코드의 주소(innodb의 경우 PK)를 모아서 정렬한 다음 최대한 빠르게 레코드를 읽도록 해줍니다. 둘 모두 sort에 사용되지만, read_rnd_buffer는 필요한 경우에만 사용되고 용도도 조금 다르다고 볼 수 있어요

답변 감사합니다! 그러면 만약 sort_buffer_size 가 부족해서 디스크에 임시적으로 정렬되는 방식이라면 디스크에서 메모리로 적재할때 innodb buffer pool 이 아니라 read_rnd_buffer에 sequencial하게 적재 후 읽는다고 이해하면 될까요?

그리고 왠만한 문제는 auto increment로 풀립니다

데이터 1600경 정도 까지 감당 가능해요 bigint 타입 기준 