---
date: 2023-10-05T23:26:11
updatedAt: 2024-06-17 22:43:08
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
	- '_index' document가 저장된 index를 나타냄
	- _id doucument의 id

logstash filter plugin  <br>[https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)<br><br>logsatsh jvm setting  <br>[https://www.elastic.co/guide/en/logstash/current/jvm-settings.html](https://www.elastic.co/guide/en/logstash/current/jvm-settings.html)<br><br>fileabeat custom index name  <br>[https://medium.com/@ketan.bhadoriya/how-to-create-a-custom-index-name-in-filebeat-68151138e090](https://medium.com/@ketan.bhadoriya/how-to-create-a-custom-index-name-in-filebeat-68151138e090)<br><br>docker mounted file not immidatly update  <br>[https://medium.com/@jonsbun/why-need-to-be-careful-when-mounting-single-files-into-a-docker-container-4f929340834](https://medium.com/@jonsbun/why-need-to-be-careful-when-mounting-single-files-into-a-docker-container-4f929340834)|