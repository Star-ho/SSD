---
date: 2024-06-17 23:16:44
updatedAt: 2024-06-22 23:11:59
---
# Lucene 용어정리
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
	- document 순서대로 저장된 field별 모든 field값의 배열로, inverted되지 않은 방식으로 인덱스에 저장됨
	- 몇개의 문서의 많은 field값을 가져오는데 효율적임
- doc values
	- Lucene의 열 단위 필드값 저장소
	- 많은 document에 대해 적은 field값을 가져오는데 효율적
	- 정렬 및 faceting에 유용함
- Index segment
	- Lucene index는 여러개의 하위 index 또는 segment로 구성될 수 있음
	- 각 segment 완전히 독립적인 인덱스이며, 개별적으로 검색될 수 있음

# Lucene에 저장된 데이터
## Inverted Index
- term과 term을 포함한 document를 매핑하는 데이터 구조
- 












https://j.blaszyk.me/tech-blog/exploring-apache-lucene-index/
