---
date: 2024-06-17 23:16:44
updatedAt: 2024-06-22 23:11:59
---
## 용어정리
- document
	- 검색과 인덱스의 단위인 레코드, 필드집합
	- document는 Lucene 인덱스에 추가되며, 검색 쿼리로 검색가능
- field
	- document에 입력된 slot
	- terms의 sequence
	- document에는 여러개의 field가 있을 수 있음
- term
	- 검색의 단위인 source doucment의 값
	- inverted index를 만드는데 사용됨
- index
	- 일반적으로 동일한 스키마를 가진 document모음
- inverted index
	- term을 ID별로 document에 매핑하는 내부 테이터 구조로, 텍스트 검색 쿼리에 효율적임
- stored field
	- 애쳐드ㅜㅅ













https://j.blaszyk.me/tech-blog/exploring-apache-lucene-index/
