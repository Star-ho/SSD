안녕하세요? varchar type 관련해서 궁금한 것이 있어서 질문을 드립니다.

mysql DB 테이블에서 어떤 컬럼을 varchar(255) 로 설정한 경우와 varchar(16) 으로 설정한 경우에 데이터 저장 공간이나 쿼리 등의 성능상의 차이가 있나요?

공식문서에서 확인해봤을 때는 varchar 는 실제로 저장되는 문자열에 필요한 만큼 저장공간을 할당을 하기에 varchar(255) 를 사용하든 varchar(16) 를 사용하든 "저장공간"의 관점에서는 별 차이가 없을 것 같다는 생각이 드는데, 이렇게 판단해도 될까요?
https://dev.mysql.com/doc/refman/8.0/en/char.html

그리고.. 쿼리 성능 측면에서 차이가 날 수도 있는 부분이 있는지는 전혀 감이 오지 않는데 혹시 설명해주실 수 있으신 분이 있다면 답변 부탁 드립니다

 https://medium.com/daangn/varchar-vs-text-230a718a22a1 이거 추천드립니다!