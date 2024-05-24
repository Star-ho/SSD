---
date: 2024-05-24 16:30:40
updatedAt: 2024-05-24 16:30:51
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

- 
