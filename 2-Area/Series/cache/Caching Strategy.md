## 어디에 저장할 것인가?
### In-memory caching
- 데이터를 데이터베이스나 디스크가 아닌 RAM에 저장하는 방식
- 높은 조회 성능을 가짐
- 비 휘발성, 서버가 종료되면 삭제됨
	- 중요한 데이터를 보관하기 힘듦
	- 정말 성능이 중요한 서버라면 RAM에 저장하고 분산 합의 알고리즘(ex. Raft 알고리즘)으로 분산해서 저장
### Distributed caching
- 하나의 네트워크에 있는 서버, 노드들의 데이터를 한곳에 캐싱하는 방식
	- Redis, memcached
- 높은 가용성과 확정성이 필요한 서비스에서 유용함
- 다른 지역에있는 데이터베이스의 정보를 가져오면 시간이 오래 걸리기에 지역마다 caching server를 두어 지역간 지연시간을 줄임

### Client-Side caching
- 데이터를 사용자의 장비(ex. 웹브라우저)에 저장하는 방식
- javaScript, image같은 정적 리소스에 자주 접근해야하는 경우 유용함
- 최신의 데이터가 아닌 옛날 데이터를 가져오지 않을 수 있기에, 정책과 만료시간을 잘 고려해야함

## 캐시 전략
### Cache-Aside
![[Pasted image 20240216132133.png|center|700]]
- 캐시에서 데이터를 확인 후, 캐시에 데이터가 없다면 데이터베이스에 요청하는 방식
- 어플리케이션이 캐시 관리의 책임을 가짐
- 캐시를 최신상태로 관리하도록 노력이 많이 필요함

### Write-Through
![[Pasted image 20240216132203.png|center|700]]
- 쓰기작업시 캣

### Write-Behind
![[Pasted image 20240216132217.png|center|700]]

### Read-Through
![[Pasted image 20240216132233.png|center|700]]



https://medium.com/@mmoshikoo/cache-strategies-996e91c80303