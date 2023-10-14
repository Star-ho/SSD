- table 생성이나, table 데이터의 변경과 같은 데이터베이스의 변경 이벤트를 기록하는 로그
- 변경을 야기할 수 있는 구문도 기록
	- 0개의 row를 삭제하는 구문
- 데이터의 업데이트가 얼마나 걸렸는지도 포함하고 있음
- Select나 Show같은 변경하지 않는 로그는 포함하고 있지 않음
	- 위와같은 로그를 보고싶다면 [The General Query Log](https://dev.mysql.com/doc/refman/8.0/en/query-log.html "5.4.3 The General Query Log")참고
- binlog의 목적
	- replication
		- 소스 서버가 레플리케이션 서버에 binlog를 보내고, bin log를 재생하므로써 같은 데이터가 유지됨
	- recover
		- [Point-in-Time (Incremental) Recovery](https://dev.mysql.com/doc/refman/8.0/en/point-in-time-recovery.html "7.5 Point-in-Time (Incremental) Recovery")에서는 bin log로 recovery진행
- bin log를 사용하는것은 server의 performance가 줄어들지만 replication이나 recover로 인한 이점이 더 많다고 판단함
	- default로 켜짐
- 완료된 이벤트나 트랜잭션만 로깅되므로 예상치못한 중단에도 저항성을 가짐
	- redo log나 undo로그가 있는데도 필요할까? 라는 생각
- 로그형태
	- Statement-based logging 
```
원래 쿼리
update PRODUCT  
set PRODUCT.LABEL = '1'  
where id = 8;
```

```
log에 남은 내용

# at 6100
#231014 22:34:23 server id 1  end_log_pos 6289 CRC32 0x36af659b Query thread_id=25 exec_time=0 error_code=0
SET TIMESTAMP=1697290463/*!*/;
/* ApplicationName=DataGrip 2023.1.2 */ update PRODUCT
set PRODUCT.LABEL = '1'
where id = 8
```

- Row-based logging
```
원래 쿼리
update PRODUCT  
set PRODUCT.LABEL = RAND()  
where id = 1 or id = 2;
```
![[Pasted image 20231014225322.png]]

|특징|Statement-based log|Row-based log|
|-------|---------|-----|
|변경 사항 추적|쿼리 수준|행 수준|
|성능|많은 변경 사항의 경우 더 좋음|적은 변경 사항의 경우 더 좋음|
|log 파일 크기|작음|클 수 있음|
|복구|어려움|



#wait-to-update