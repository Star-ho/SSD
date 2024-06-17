---
date: 2023-10-05T23:26:11
updatedAt: 2024-06-17 23:00:55
tags:
  - Elastic-Search
categories:
  - ElasticSearch
---
- 분산 문서 장소
- 분산 시스템으로 구성되어 대용량 데이터와 빠른 검색 가능
- 역인덱스구조
## Document
- 엘라스틱 서치의 단일 데이터 단위
- JSON구조로 되어있음
- 디폴트로 schema-less구조
	- schema를 지정 하지 않아도 됨
	- schema를 지정할 수 있으며, schema를 지정했다면, 모든 document들은 schema를 따라야함
- metadata
	- _index document가 저장된 index를 나타냄
	- _id doucument의 id를 나타냄
> https://opster.com/guides/elasticsearch/glossary/elasticsearch-document/

## Node
- 하나의 ElasticSearch 인스턴스
- node는 여러 role을 가질 수 있음
	- master, data, data_content, data_hot, data_warm, data_cold, data_frozen, ingest, ml, remote_cluster_client, transform
### Master node
- 인덱스의 생성 또는 삭제, 클러스터의 일부인 노드추적, 어떤 샤드를 어떤 노드를 할당할지 결정하는 등 가벼운 작업을 담당

### Data node
- 인덱싱한 문서가 포함된 샤드를 보관
- CRUD, 검색, 집계와 같은 데이터 관련 작업 처리
	- I/O, 메모리, CPU 집약저긴 작업
> https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html#generic-data-node



logstash filter plugin  <br>[https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)<br><br>logsatsh jvm setting  <br>[https://www.elastic.co/guide/en/logstash/current/jvm-settings.html](https://www.elastic.co/guide/en/logstash/current/jvm-settings.html)<br><br>fileabeat custom index name  <br>[https://medium.com/@ketan.bhadoriya/how-to-create-a-custom-index-name-in-filebeat-68151138e090](https://medium.com/@ketan.bhadoriya/how-to-create-a-custom-index-name-in-filebeat-68151138e090)<br><br>docker mounted file not immidatly update  <br>[https://medium.com/@jonsbun/why-need-to-be-careful-when-mounting-single-files-into-a-docker-container-4f929340834](https://medium.com/@jonsbun/why-need-to-be-careful-when-mounting-single-files-into-a-docker-container-4f929340834)|