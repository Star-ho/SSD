---
created: 2023-11-11T23:12:11
date: 2024-03-03T11:41
updated: 2024-03-31T22:43
---
- 트랜잭션이나 안정성의 희생 없이, innodb를 memorydb처럼 활용할 수 있게함
- 검색 관찰자 패턴(observe pattern of search)를 기반으로 인덱스 키의 접두사를 사용하여 인덱스를 구축
- mysql에서 innodb테이블의 인덱스 검색을 모니터링 하여 자주 사용하는 인덱스페이지에 대해 hash index를 만듬
- 메모리에 hash index를 구성하여 =, in연산자의 속도를 높일 수 있음(<,>, like 연산에는 사용 불가)
- 만들어진 hash index는 메모리db에 가까움
- 사용 방법에 따라 유용할수도, 유용하지 않을 수 있으므로 도입 후 벤치마크를 통해 확인해야함

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_adaptive_hash_index

#Innodb 
#adaptive-hash-index
#Innodb-In-Memory-Structure