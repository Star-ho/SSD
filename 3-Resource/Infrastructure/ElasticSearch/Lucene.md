---
date: 2024-06-17 23:16:44
updatedAt: 2024-06-22 23:37:24
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
- document의 텍스트를 분석하고 term을 추출하여 구축됨
- Inverted Index로 term 또는 term집합이 포함된 document를 찾는 방법을 제공하여 빠르고 효율적인 검색이 가능함
- 특정 document와 일치하는 검색어가 얼마나 많은지 파악하여 검색결과의 관련성 순위를 매기는 방법을 제공함

- term dictionary와 postings list의 2개의 substructure로 구성되어있음
	- term dictionary
		- document 안에 포함된 모든 term의  정렬된 list로 그룹화함
	- postings list
		- 각 term의 목록을 생성하여, 해당 term이 나타나는 문서를 표시함
![|center|600](Pasted%20image%2020240622233603.png)
- Lucene의 Inverted ind










https://j.blaszyk.me/tech-blog/exploring-apache-lucene-index/
