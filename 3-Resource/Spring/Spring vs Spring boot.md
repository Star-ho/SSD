---
date: 2024-06-28 23:31:36
updatedAt: 2024-06-28 23:31:54
---
Spring boot와 Spring의 차이점을 알아보자.

## 1. Embedded Tomcat
- Spring에는 Tomcat이 없음
- 서버를 띄우기 위해 tomcat을 띄우고, was내의 설정으로 dispatcher서블릿을 지정하고 배포해야함
- spring boot에서는 embedded tomcat이 있어 따로 설정 하지 않아도됨

## 2. AutoConfiguration
- Spring boot는 클래스 패스를 스캔하여, 어떤 라이브러리들이 포함되어 있는지 확인 후 자동으로 설정해줌
- 기본 설정으로 사용할경우, 라이브러리를 추가하고 property를 주입만 하면 해당 라이브러리를 사용할 수 있음

## 3. 코드로 설정 관리
- 기존에는 설정을 xml을 사용하여 관리해야했음
	- 빈, 트랜잭션 매니저, aop관련
- spring boot에서는 코드로 해당 설정들을 설정할 수 있음







https://www.slideshare.net/slideshow/spring-boot-42817314/42817314
https://www.slideshare.net/slideshow/2016-deep-dive-into-spring-boot-autoconfiguration-61584342/61584342