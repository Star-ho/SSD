---
date: 2024-06-18 22:30:18
updatedAt: 2024-06-18 22:30:56
---
- search쿼리는 도착지를 고정할 수 없고, 잠재적으로 매칭되는 index또는 indices안의 모든 샤드를 검색해야하기에 어려움
- 일치하는 문서를 찾는 것 뿐만아니라, 검색 api는 결과를 사용자에게 표시하기 전에 통합되고 정리된 목록으로 결합해야함
- 기본적으로, 엘라스틱서치는 Query Then Fetch라는 검색방법을 사용함

## 단계
1. 클라이언트가 Elasticsearch로 쿼리 전송
2. 쿼리를 각 샤드로 브로드캐스팅
3. 로컬 용어/빈도를 사용해 일치하는 모든 문서 찾기 및 점수계산
4. 결과의 우선 대기열 구축(정렬, 페이지네이션 등)
5. 요청 노드에 결과에 대한 메타데이터를 반환함
	- 실제 문서는 아직 전송되지 않고 점소만 전송됨
6. 모든 샤드의 점수가 요청 노드에서 병합 및 정렬되고, 쿼리 기준에 따라 문서가 선택됨
7. 끝으로, 실제 문서가 있는 개별 샤드에서 실제 문서가 검색됨
8. 결과를 클라이언트에 반환한

- 조정 노드는 1,2,8단계에서 사용됨

## Query Phase(3,4,5,6)
- 검색 쿼리는 모든 샤드에 전성되어 로컬 실행이 시작되고, 일치하는 문서가 포함된 우선순위 대기열이 생성됨

![](Pasted%20image%2020240618223803.png|center)

## Fetch Phase(7)
- query Phase가 연관된 문서를 확인하는 반면에,  Fetch phase에서는 각각의 샤드에서 실제 문서를 가져오는 역할을 담당함
![](Pasted%20image%2020240618223931.png|center)

- 이 분할방식은 분산된 환경에서 효과적이고 확장가능한 검색작업을 보장함
	- Query phase에서는 검색 커리가 각 샤드 복사본을 탐색하여 로컬 검색을 시작하고, 일치하는 문서의 우선순위가 지정된 목록을 컴파일함
		- 이 단계는 검색 결과를 구체화 하는 초기단계임
	- Fetch phase에서는 원하는 검색 결과를 제공함
		- 이 단계는 쿼리 실행과 검색 결과 사이의 가교 역할을 하며 검색 프로세스의 철저함을 보장함

## 추가 정보
- Elasticsearch의 query와 fetch phases에서 slow logs를 enable하면, 검색 성능을 모니터링 및 죄적화가 가능함
```HTTp
PUT *,-.*/_settings  
{  
"index.search.slowlog.threshold.query.warn": "1s",  
"index.search.slowlog.threshold.fetch.warn": "100ms"  
}  
  
#or with curl  
  
curl -XPUT "http://localhost:9200/*,-.*/_settings" -H "Content-Type: application/json" -d'  
{  
"index.search.slowlog.threshold.query.warn": "1s",  
"index.search.slowlog.threshold.fetch.warn": "100ms"  
}'
```



https://medium.com/@musabdogan/elasticsearchs-distributed-search-query-and-fetch-phases-df869d35f4b3