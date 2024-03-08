---
created: 2023-11-13T22:37:00
updated: 2024-03-08T23:19
---
- buffer pool 내부에 존재하며, secondary index의 변경을 캐싱하기 위한 공간
- DML(INSERT, UPDATE, DELETE)로 인한 변경되는 페이지가 buffer pool에 없을떄, secondary index의 변경을 캐시하는 buffer
- secondary index는 clustered index와는 다르게 고유하지 않고, 무작위로 데이터가 삽입됨
	- 데이터를 변경하려면 추가 I/O작업이 필요함
- buffer pool에 변경되는 페이지의 데이터를 읽을때, idle상태일때, slow shutdown시 변경내용을 반영함
- 물리적으로 change buffer는 system table space에 위치함
	- db restart발생시에도 변경사항이 보관됨
- 디폴트로 buffer pool의 25%를 사용하며 최대 50%까지 늘릴 수 있음

- 인덱스에 내림차순 인덱스열이 포함되어 있거나, 기본키에 내림차순 인덱스열이 포함되어있는경우 change buffer는 사용되지 않음

#change-buffer
#Innodb-In-Memory-Structure 


https://dev.mysql.com/doc/refman/8.0/en/innodb-change-buffer.html