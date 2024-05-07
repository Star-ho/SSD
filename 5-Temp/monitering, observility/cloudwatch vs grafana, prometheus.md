---
date: 2024-05-07 22:41:47
updatedAt: 2024-05-07 22:42:04
---
aws쓰면 그냥 cloudwatch가 좋지 않나요? 로그수집도 쉽게 볼 수 있고 한데 왜 grafana랑 Prometheus 쓰는지 궁금합니다.
아 근데 cloudwatch가 메트릭이 10개 넘어가면 비용이 상당한거같긴합니다 비용적 측면인가요?

비용도 비용인데 클와는 몇시간 지나면 1분 단위로 어그리케이션 해서 데이터가 뭉게짐
그리고 메트릭중 default 로 수집 안되는 녀석들은 결국 에이전트 설치 해줘야하는데 예를 들면 시스템 메모리 같은. 그럼 결국 에이전트 달아야 하는데 그럼 내가 세세하게 컨트롤 할수 있는 


https://blog.cloudacode.com/monitoring%EC%9D%98-%ED%98%84%EC%9E%AC%EC%99%80-%EB%AF%B8%EB%9E%98-%EA%B7%B8%EB%A6%AC%EA%B3%A0-observability-ab7babbc6d28