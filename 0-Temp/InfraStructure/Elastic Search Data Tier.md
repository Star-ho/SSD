- 시계열 인덱스일때 매우 유용
- 많은 경우, 시계열로 인덱스를 잡았다면 최근 데이터를 자주보고, 옛날 데이터를 덜 보게 될것이다.
- Data Tier는 Content, Hot, Warm, Cold, Frozen 4개의 티어로 나누고 Fronzen에서 계속 보관하거나 삭제를 하는 방법도 있다.
- Content Tier는 실제로 사용하고 있는 데이터 이고 이후 데이터들은 Content Tier에서 
- Hot으로 갈수록 더 최근, 자주 접근하는 데이터이고 Frozen으로 갈수로 옛날, 잘 접근하지 않는 데이터이다.
- 

  
https://www.elastic.co/guide/en/elasticsearch/reference/current/data-tiers.html
https://www.elastic.co/kr/blog/implementing-hot-warm-cold-in-elasticsearch-with-index-lifecycle-management


#wait-to-update