---
date: 2024-06-17 23:16:44
updatedAt: 2024-06-23 00:11:10
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
- Lucene의 Inverted index로 색인된 3개의 document임\
- 각 document의 내용은 inverted index에 삽입되는 term으로 tokenized됨
- Terms Dictionary가 정렬되어 있기 때문에, 바이너리 검색처럼 용어를 빠르게 찾을 수 있으며, posting-structure에서 해당 용어의어가 나타난것을 찾을 수 있음
- 특정 document에서 관련된 term을 나열하는 forward index와 반대됨

## DocValues
- 색인 시점에 document와 value를 매핑한 column-oriented field이며, inverted된것이 아님
- DocValues를 사용하면 단일 디스크 검색으로 여러 document의 field를 검색할 수 있으므로 정렬 및 그룹화를 위한 조회 속도가 빨라짐
- 쿼리에서 전체 document를 검색하는 경우가 아니라면, stored field 보다 DocValues를 선호해야함

## Stored Field
- DocValues와 유사하게, document field를 값을 효과적유지한 다음 필요할 때 검색할 수 있도록 저장된 것
- 행 방식으로 구성됨
- field집합이 주어지면, 각 document에 대해 이 field의 값이 행으로 연결됨
- 이후 row는 Lucene Document ID에 따라 디스크에 순처적으로 저장됨
- 각 행은 해당 문서에 정의된 필드수와 데이터 유형에따라 크기가 다름
- 각 행에 대한 포인터는 빠르게 접근할 수 있도록 저장됨
- 검색 쿼리가 일부 field가 아닌, 전체 document를 반환하는 경우에 유리함

# Insertion(삽입)
- Inverted index를 구축할때, 검색속도, 압축, 인덱싱 속도, 새로운 변경사항이 표시되는데 걸리는 시간 등을 우선적으로 고려해야함
- 검색 속도와 index 압축은 서로 관련이 있음
- 작은 index로 검색할때는 처리해야하는 데이터 양이 줄어들고, 메모리에 더 많은 데이터를 저장할 수 있음
- 둘 다, 특히 압축은 색인 속도가 느려지는 문제가 있음

![|center|800](Pasted%20image%2020240622235513.png)
- 새 document가 추가되면, index 변경사항이 먼저 메모리에 버퍼링되고, index파일 전체가 디스크에 flush됨
- 이렇게 작성된 파일은 index 세그먼트를 구성함
- Lucene index segment는 write-once파일로, segment가 저장소에 저장되면 절대 변경되지 않음
- index는 실제로 전체 index의 하위 집합으로, 여러 파일로 구성됨
	- index의 영구적인 조각화를 방지하기 위해, segment는 주기적으로 병합됨
- 위의 예에서는 각각 하나의 문서로 구성된 2개의 세그먼트가 있고, 오른쪽에서 세그먼트 병합의 결과를 볼 수 있음
	- 2개의 세그먼트가 병합되어 새로운 세그먼트가 형성됨
-> 단일 document추가는 세그먼트를 추가해야 하므로 비용이 많이듬, 

# Deletions(삭제)
- 각 segment에 대해 Lucene은 segment별 비트를 유지함
- 비트가 1에서 0으로 바뀌면 document가 삭제되었다는 신호가 Lucene에 전달됨
- 그 이후 모든 검색은 삭제된 문서를 건너뜀
- 병합 후에는 결과 segment가 삭제된 document가 포함되지 않으므로, segment가 병병합될 때 까지는 삭제된 document가 소비한 바이트가 회되지 않음
- 기존 segment document를 제자리에서 삭제하려면 비용이 너무 많이듬

# Update
- 이전에 색인된 document를 수정하는것은 document를 cheap하게 삭제한다음, 다시 삽입하는것
- document를 수정하는 것음 처음에 추가하는 것보다 훨씬 더 많이듬
- 자주 바뀌는 값을  Lucene인덱스에 저장하는 것은 좋지 않음 

https://j.blaszyk.me/tech-blog/exploring-apache-lucene-index/
https://j.blaszyk.me/tech-blog/exploring-apache-lucene-search-and-ranking/
https://j.blaszyk.me/tech-blog/exploring-apache-lucene-scale/