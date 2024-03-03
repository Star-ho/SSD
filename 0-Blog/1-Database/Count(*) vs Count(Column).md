---
date: 2024-03-02T22:41:32
---
- 테이블의 전체 갯수를 얻기 위해 Count()과 Count(Column)를 사용할때는 Count(_)가 성능적으로 더 좋음  
- Count를 할때는 null값을 확인한 후 null이 아닌 갯수만 리턴하는데, Count(Column)을 하게되면 Column의 null체크를 하기때문에 성능 저하가 발생함,  
- 전체갯수를 파악하기 위해서는 Count(*)을 사용하자

[https://m.blog.naver.com/pjt3591oo/221030483713](https://m.blog.naver.com/pjt3591oo/221030483713)

#Database 
#Query-turning 