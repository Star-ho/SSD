---
created: 2024-03-31T22:41:00
date: 2024-04-13T22:56
---
netflix의 msa전환기
https://open.substack.com/pub/bytebytego/p/a-brief-history-of-scaling-netflix?r=3ebbmm&utm_medium=ios

에어비앤비의 soa 
https://blog.bytebytego.com/p/a-brief-history-of-airbnbs-architecture?utm_campaign=post&utm_medium=web

MSA와 SOA의 가장 중요한 차이점은 무엇일까요?
헷갈리시면 롤백시나리오로 생각하시면 더 빠르게 이해되세요 ㅎ
상품 오더를 취소하는 로직이 어떻게 될지
제 정답은 데이터베이스 격리여부 였습니다 
좀더 정확히는
롤백을 디비트렌젝션으로 처리 한다 모든걸 롤백 트렌젝션을 각각 컴포넌트의 api베이스로 한다 입니다
당연히 디비가 분리되어 있으면 트렌젝션 하나로 안되지만 그 이유를 아시면 좋죠 


#argent 