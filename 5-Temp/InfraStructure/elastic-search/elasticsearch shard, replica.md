---
date: 2023-10-05T23:32:36
updatedAt: 2024-05-28 23:27:39
tags: 
---
## node 
- elastic search 인스턴스

## index 
- 데이터가 저장되는 공간
- 하나의 인덱스가 여러 shard를 가질 수 있음

## shard 
- 인덱스의 모든 데이터중 일부만 보관
	- shard에 모든 데이터가 들어가지만, 하나의 shard에 다 들어가는게 아닌, 여러 shard에 나누어져 들어감
- 개수를 수정하려면 reindex해야함
- shard는 Lucene의 싱글 인스턴스이며 그 자체로 완벽한 검색엔진임
- 디폴트로 ??
- primary shard와 replica shard가 존재함
	- primary shard
		- 각각의 document는 하나의 primary shard에 속함
		- 최대 Integer.MAX_VALUE - 128 만큼의 document를 저장할 수 있음
		- update시 즉시 업데이트
	- replica shard
		- primary shard의 복제본
		- update시 즉시 업데이트 되지 않음



https://www.elastic.co/kr/blog/how-many-shards-should-i-have-in-my-elasticsearch-cluster
https://www.elastic.co/guide/en/elasticsearch/guide/2.x/_add_an_index.html
https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro.html
#wait-to-update 