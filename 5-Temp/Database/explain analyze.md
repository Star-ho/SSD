explain analyze 구문을 이용해 actual time을 획득했습니다.
실제 쿼리 수행시간과 차이가 너무 큰데, 왜 이런걸까요..?ㅠ

쿼리를 실행하기 '전'에 만든 실행계획이기 때문이지 않을까요? 어디까지나 옵티마이저가 통계 데이터를 바탕으로 이정도 걸릴꺼라는걸 예측을 해주는것이지, 실제로 쿼리가 실행될때에는 쿼리에 영향을 줄 많은 요소들이 개입될 소지도 있을거구요. 

explain analyze 구문은 실제 실행시간을 보여주는거 아니었나요??

https://dev.mysql.com/blog-archive/mysql-explain-analyze/#:~:text=Actual%20time%20to,number%20of%20loops

https://hackmysql.com/post/book-2/