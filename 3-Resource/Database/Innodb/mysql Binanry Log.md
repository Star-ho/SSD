---
date: 2024-03-31T22:41:00
updatedAt: 2024-04-21 18:32:05+2240
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
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
- 수명은 디폴트 30일
- 완료된 이벤트나 트랜잭션만 로깅되므로 예상치못한 중단에도 저항성을 가짐
- 로그형태
	- Statement-based logging 
```
원래 쿼리
update PRODUCT
set PRODUCT.LABEL = RAND()
where id = 1 or id = 2
```
![Pasted image 20231014225459](real-resource-image/Pasted%20image%2020231014225459.png)

- Row-based logging
```
원래 쿼리
update PRODUCT  
set PRODUCT.LABEL = RAND()  
where id = 1 or id = 2;
```
![Pasted image 20231014225322](real-resource-image/Pasted%20image%2020231014225322.png)
- mixed logging
	- default로 Statement-based logging 이지만, 특정상황에서 Row-based logging함
> mixed logging은 중요하지 않을것 같아 기회가 생기면 추후 작성


|특징|Statement-based log|Row-based log|
|-------|---------|-----|
|변경 사항 추적|쿼리 수준|행 수준|
|성능|많은 변경 사항의 경우 더 좋음|적은 변경 사항의 경우 더 좋음|
|log 파일 크기|작음|클 수 있음|
|복구|어려움|

> 아래 명령어를 사용하여 로그파일 확인함
> mysqlbinlog --base64-output=DECODE-ROWS  -v binlog.000025
## Binary log vs redo log

- 로깅 주체
	- Binary log는 mysql서버에서 로깅
	- redo로그는 InnoDB 엔진에서 로깅
- 로그 레벨
	- Binary log는 sql문에 대한 논리적인 로깅
	- redo로그는 데이터 페이지에 대한 물리적인 로깅
- 목적
	- Binary log는 특점시점 복구 및 복제에 사용
	- redo log는 장애시 트랜잭션 내구성을 보장하기 위해 사용
		> aws aurora에서는 redo log와 storage를 복제에 사용



https://dev.mysql.com/doc/refman/8.0/en/binary-log-setting.html
https://dev.mysql.com/doc/refman/8.0/en/binary-log.html
https://www.alibabacloud.com/blog/what-are-the-differences-and-functions-of-the-redo-log-undo-log-and-binlog-in-mysql_598035

#Database 
#InnoDB 