---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 17:28:32+9460
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
- buffer pool에 있는 변경점(Dirty Page)를 실제로 디스크에 쓰기 전 Double write buffer에 기록
- 변경점을 실제 테이블로 적용 후 Double write buffer를 삭제함
- 데이터를 쓰는 도중에 오류로 종료되었을때 데이터의 무결성 보장을 위한 버퍼
- 실제 데이터를 2번쓰는작업이라 속도가 느리긴 하지만, fsync()를 한번만 호출하기 때문에 속도가 2배로 느려지진 않음
- mysql서버는 서버를 시작할, Double write buffer와 데이터를 확인하여 데이터가 다르다면 Double write buffer내용을 데이터파일에 덮어씌움

https://dev.mysql.com/doc/refman/8.0/en/InnoDB-doublewrite-buffer.html
https://hoing.io/archives/1114

#Database 
#InnoDB 