---
created: 2023-12-19T22:16:41
updated: 2024-03-03T11:41
---
네트워크 관련 질문이 있습니다. SNI(Server Name Indication) 기능이 없었을 때에는 SSL/TLS 요청 시 서버가 어떤 인증서를 제시해야 할지 결정하는데 사용할 수 있는 유일한 정보가 IP 주소였다고 하는데, 인증서는 서버가 가지고 있는거 아닌가요? 그럼 그냥 보유하고 있는 인증서를 제시하면 될텐데 IP 주소가 왜 필요한건지 잘 모르겠습니다.

https://www.cloudflare.com/ko-kr/learning/ssl/what-is-sni/

요약하자면, HTTP레이어 이전에 있는 TLS 암호화에서는 FQDN 정보가 없다. 때문에 어떤 인증서로 Handshake 해야할 지 모른다. 이 인증서를 선택할 수 있게 FQDN을 알려줄 수 있도록 지원하는 것이 SNI다.