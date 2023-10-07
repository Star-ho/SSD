mysql foreign key, join lock
어떨때 foreign key 제약조건

데이터 변경할때 기본적으로 x락이 걸리는데  
외래키가 걸려잇으면 외래키 친구들에게도 s락이 걸리면서  
[https://stackoverflow.com/questions/83147/whats-wrong-with-foreign-keys](https://stackoverflow.com/questions/83147/whats-wrong-with-foreign-keys)|