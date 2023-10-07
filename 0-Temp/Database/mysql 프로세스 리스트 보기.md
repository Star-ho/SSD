select * from information_schema.PROCESSLIST;

![[Pasted image 20231007162016.png]]

### ID
- connection의 식별자
### USER
- 해당 구문을 실행한 유저
- event_schduler는 예약된 이벤트를 모니터링하는 스레드

### HOST
- 해당 구문을 실행한 호스트명

### DB
- 해당 스레드가 선택한 데이터베이스

### COMMAND
- 실행하는 명령의 유형
- sleep - 클라이언트에게 새로운 구문을 받기위해 대기하는 상태
- query - 쿼리를 실행중인 상태
- [상태 참고 링크](https://dev.mysql.com/doc/refman/8.0/en/thread-commands.html)

## TIME
- 쓰레드가 현재 상태에 있던 시간
- 초단위
### STATE
- 

### INFO


https://dev.mysql.com/doc/refman/8.0/en/information-schema-processlist-table.html

#Database 
#Query 
#Trouble-Shooting 