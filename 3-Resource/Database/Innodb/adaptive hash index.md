---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 17:27:35+4200
tags:
  - InnoDB-Architecture
  - "#Database"
  - "#hugo_blog"
categories: InnoDB
---
- 트랜잭션이나 안정성의 희생 없이, InnoDB를 memorydb처럼 활용할 수 있게함
- 검색 관찰자 패턴(observe pattern of search)를 기반으로 인덱스 키의 접두사를 사용하여 인덱스를 구축
- mysql에서 InnoDB테이블의 인덱스 검색을 모니터링 하여 자주 사용하는 인덱스페이지에 대해 hash index를 만듬
- 메모리에 hash index를 구성하여 =, in연산자의 속도를 높일 수 있음(<,>, like 연산에는 사용 불가)
- 만들어진 hash index는 메모리db에 가까움
- 사용 방법에 따라 유용할수도, 유용하지 않을 수 있으므로 도입 후 벤치마크를 통해 확인해야함

https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_adaptive_hash_index

#InnoDB 