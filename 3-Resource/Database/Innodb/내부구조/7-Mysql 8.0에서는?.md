---
date: 2024-05-24 16:30:40
updatedAt: 2024-05-24 17:05:27
tags:
  - InnoDB
  - InnoDB-File-Structure
  - hugo_blog
categories:
  - Database
---
- Jeremy Cole의 InnoDB정보들은 MySQL 5버전에 관한 내용이며, 10년전의 내용임
- 현재 MySQL 8버전대를 사용하는데, 큰 기본 틀의 큰 차이는 없어 보이지만, 간단하게 알아볼 예정

- Jeremy Cole의 Innodb_ruby는 현재 8버전 대를 지원하고 있지 않음
- 필자는 아래 두가지 도구를 추천한다
	- https://github.com/alibaba/innodb-java-reader
		- 이 포스팅에서 사용할 도구
	- https://github.com/baotiao/inno_space
		- 사용방법을 익히려 해보았지만, record를 파싱하는 부분에서 에러가 나서 결국 포기하였다.
		- 예제 데이터는 ibd2sdi를 이용하여 record정보를 가져오는것 같은데 실패하였다
			- 방법을 알면 댓글로 알려주시길 바랍니다 ㅠㅠ

## 무엇을 알아볼 것인가?
- space page구조
- index page들은 doubly-linked list 구조인지
- index record들은 singly-linked list구조인지

## Space page 구조
```json

{"checksum":3778981766,"pageNumber":0,"prevPage":80037,"nextPage":1,"lastModifiedLsn":403626824,"pageType":"FILE_SPACE_HEADER","flushLsn":0,"spaceId":13}
{"checksum":3416855761,"pageNumber":1,"prevPage":0,"nextPage":0,"lastModifiedLsn":403623384,"pageType":"IBUF_BITMAP","flushLsn":0,"spaceId":13}
{"checksum":4200002457,"pageNumber":2,"prevPage":0,"nextPage":0,"lastModifiedLsn":403626824,"pageType":"INODE","flushLsn":0,"spaceId":13}
{"checksum":2629066168,"pageNumber":3,"prevPage":null,"nextPage":null,"lastModifiedLsn":403655232,"pageType":"SDI","flushLsn":0,"spaceId":13}
{"checksum":3816051266,"pageNumber":4,"prevPage":null,"nextPage":null,"lastModifiedLsn":403629472,"pageType":"INDEX","flushLsn":0,"spaceId":13}
{"checksum":0,"pageNumber":0,"prevPage":0,"nextPage":0,"lastModifiedLsn":0,"pageType":"ALLOCATED","flushLsn":0,"spaceId":0}
{"checksum":0,"pageNumber":0,"prevPage":0,"nextPage":0,"lastModifiedLsn":0,"pageType":"ALLOCATED","flushLsn":0,"spaceId":0}
```
- 매우 작은 테이블의 구조임
- 5버전대와의 차이점은 SDI페이지가 생겼다는 것이고, 이외에는 동일하다
	- 
- 