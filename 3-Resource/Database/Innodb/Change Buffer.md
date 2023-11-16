- DML(INSERT, UPDATE, DELETE)로 인한 변경되는 페이지가 buffer pool에 없을떄, secondary index의 변경을 캐시하는 buffer
- buffer pool 내부에 존재함
- 데이터 엑세스시, 변경된 내용을 디스크에서 읽는 것 보다 change buffer에서 변경사항을 병합하는게 I/O가 덜 사용되어 
- buffer pool에 변경되는 페이지의 데이터를 읽을때, idle상태일때, slow shutdown시 업데이트된 인덱스페이지를 디스크에 작성
- secondary index는 clustered index와는 다르게 고유하지 않고, 무작위로 데이터가 삽입됨
- 
	- 
해당 페이지를 읽거나, 

- 인덱스에 내림차순 인덱스열이 포함되어 있거나, 기본키에 내림차순 인덱스열이 포함되어있는경우 change buffer는 사용되지 않음


#Innodb-In-Memory-Structure 