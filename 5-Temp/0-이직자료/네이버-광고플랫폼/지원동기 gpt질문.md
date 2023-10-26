https://foil-beach-f58.notion.site/BE-Flyer-Backend-d1bea6d0467842769d109563032c3fe7 
https://recruit.navercorp.com/rcrt/view.do?annoId=30001581&lang=ko
위의 광고플랫폼 공고를 보고 "지원자의 경력을 중심으로 지원 동기를 소개해 주세요." 라는 자소서 항목을 작성해줘

아래는 해당조직과 관련된 설명이야

네이버 광고 플랫폼 (Naver Dynamic Ads)
- 네이버의 다양한 광고 소재를 통합 관리하고, 사용자에게 최적화된 소재를 구성하여 전달하는 역할을 하고 있습니다
- 이를 위해 다양한 유저 이벤트와 쇼핑정보를 활용하여 개인화된 맞춤 광고를 생성합니다
- 다양한 추천 모델과 여러 알고리즘을 통해 광고 소재를 최적화 하고 있습니다
[https://displayad.naver.com/](https://displayad.naver.com/)
[https://tv.naver.com/v/23860615/list/743144](https://tv.naver.com/v/23860615/list/743144)

라인 Flyer 서비스(일본)
- 라인을 통해서 일본 사용자를 대상으로하는 서비스로 지금까지 오프라인 중심이었던 전단지 시장의 패러다임을 바꾸기 위해서 만들어진 서비스입니다. 사용자의 관심과 생활 영역에 맞게 디지털라이즈된 전단지나 상품정보를 제공합니다.
- [https://www.linebiz.com/jp/service/line-flyer/](https://www.linebiz.com/jp/service/line-flyer/)
- [https://chirashi.line.me/home](https://chirashi.line.me/home)

해당 조직에서 하는 일이야
광고 소재를 서빙하고, 데이터를 실시간으로 연동하여 소재를 업데이트하고,
유저 데이터와 쇼핑 상품 정보와 같은 도메인데이터를 수집, 가공하여 광고를 위해 저장합니다.
앞으로 신규로 진행할 프로젝트가 이미 많이 준비되어 있고, 글로벌한 경험도 쌓을 수 있는 기회가 있습니다.
아래와 같은 기술 스택기반으로 다양한 경험을 할 수 있습니다
- Backend: Kotlin(coroutine), Spring Mvc/Webflux, Redis, Kafka, MongoDB
- Data Engineering : Hadoop, Hive, Spark, Kafka, Redis, Airflow, Trino, MongoDB
- 사용자 행동 분석, A/B Test, MAB(Multi Armed Bandi) Test, 광고 성과 분석

이 이후로는 나의 경력과 관련된것들이야
## 더파이러츠 (2021.10 ~ 현재)

### [통합계정]

- 프로젝트 구조 설계 및 구현
- Spring WebFlux를 도입
- 콘솔 로그인, 회원가입, 판매자 로그인, 회원가입 구현
- Email 인증, 본인 인증, OAuth, 핸드폰 인증 구현
- Redis를 이용한 블랙리스트 토큰 관리
- 레거시 프로젝트 개선
    - 코드 정리
    - 로그인시 요청 개선
        - 기존
            - 브라우저 -> 프론트 서버 -> 외부 Oauth 서버 -> 프론트서버 -> 내부 계정 서버  -> 프론트 서버 -> 서비스별 백엔드서버 -> 브라우저
        - 개선
            - 브라우저 -> 백엔드 서버 -> 외부 Oauth 서버 -> 백엔드서버 -> 브라우저
    - 오류개선
        - 서비스별 access token에 담는 정보의 형식이 달라 a서비스에서 로그인시 b서비스에서 재 로그인 해야 하는 문제 해결
        - 권한 확인 로직 개선
            - 기존
                - 인증이 필요한 요청시 session을 호출하여 인증 여부 확인 후 해당 요청 전송
            - 개선
                - 인증이 필요한 요청 바로 전송
- account-lib수정
    - 커스텀 어노테이션을 선언 및 구현하여 토큰 검증 및 토큰에서 데이터를 파싱
    - 파싱할 수 있는 데이터를 Enum으로 정의
    - 인증이 필요한 요청이 들어오면 쿠키에서 토큰을 가져와서 토큰을 검증하고, redis에서 해당 토큰을 조회하여 로그아웃된 토큰인지 검증
    - 기존에는 각 서비스에서 intercetor를 구현하였으나 account-lib내에서 구현하여 bean으로 등록하면 되도록 구현
- 웹 시스템 아키텍처 설계 및 구현
    - 프로젝트 구조 설계 및 AWS ECS, RDS 등 인프라 구축
    - CodePipeline, CodeBuild를 이용한 CI/CD 환경 구성
- 사용 기술
    - spring webflux(2.7), kotlin(1.7), r2dbc
    - mysql, redis
    - codePipeline, codeBuild, ecs
    

### [도매 서비스]

- API 개발
    - 주문 프로세스(주문접수, 중량/수량/사입 관리, 출고지시), 배송기사 페이지, 휴면회원, 등급관리, 영업담당자 관리, 단가관리, 예약관리, 재고관리 구현
    - 웹 시스템 아키텍처 설계 및 구현
- 멀티 모듈 설계로 같은 로직은 공통모듈, 사용자 모듈, 관리자 모듈로 분리
- 성능 개선을 위한 자바(11 to 17), 코틀린(1.4 to 1.7), 스프링 버전 업(2.3 to 2.7)
- CodePipeline, CodeBuild를 이용한 CI/CD 환경 구성
- 사용기술
    - Spring Boot, Kotlin, JPA, Hibernate, MySQL, ElasticSearch,
    - CodeBuild, CodePipeline, ECS, Elastic LoadBalancer 사용

### [수조 환경정보]

- 수조 환경정보 앱(안드로이드) 개선
- 수조 환경정보 API 개선

### [수산시장]

- 장바구니 조회 속도 개선
- 가게 목록 조회 개선
- 오류수정
    - 예약배송
    - 마이페이지 오류 수정
    - 가게의 주문 가능 검증 로직

### [인프라]

- 데이터베이스 분리
    - 기존에는 1개의 aws rds 클러스터를 사용하여 5개의 서비스를 운영하였음
    - 1개의 서비스에서 갑작스러운 트래픽 증가, 혹은 DeadLock으로 인한 데이터베이스 장애로 전체 서비스 중단이 발생하는 상황이 있었음
    - 데이터베이스 장애로 전체 서비스 중단을 방지하기 위해 각각의 서비스별로 데이터베이스 클러스터를 사용하도록 변경하였음
    - 데이터베이스 업그레이드(5.6 → 5.7)
    - AWS Lambda를 이용한 스크립트 작성을 수행하였습니다.
    - CI/CD (AWS CodePipeline, CodeBuild, ECS, ECR) 및 Routing(Route53, Elastic Load Balancer) 설정을 수행하였습니다. 또한, 팀원 교육을 담당하였습니다.
- Sentry 도입
    - 6개의 서비스 도입
    - 오류 수집 기능
        - 생각보다 많은 오류가 발생하고 있었음
        - 오류 발생, 빈도에 대해 정리할 수 있었고, 생각치 못한 버그를 찾을 수 있었음
    - 알림기능
        - 중요한 에러, 덜 중요한 에러에 대해 구분하였고 중요한 에러는 즉각적으로, 덜 중요한에러는 5분에 10개 이상 발생시 알림하도록 설정하였음
        - 갑자기 큰 트래픽 혹은 장애로 성능이 저하되었을때 알림을 받을 수 있도록 설정함