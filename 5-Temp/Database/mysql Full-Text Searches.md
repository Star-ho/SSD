---
date: 2024-04-21T15:02:55
updatedAt: 2024-04-21T15:07
tags: 
---
- FULLTEXT type의 인덱스
- ngram파서와 MeCab파서가 있는데 ngram파서가 한국어를 지원
- 데이터셋이 많을경우 테이블 생성시 인덱스를 넣는것보다 데이터를 넣고 인덱스를 넣는게 성능이 더 좋음
- MATCH 함수에 검색할 컬럼을 넣고, AGAINST함수에 검색어를 입력