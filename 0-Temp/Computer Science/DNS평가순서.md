최근 example.com
검색 사이트에서 도메인이 이상하게 올라왔다.
test-v2.example.com

결과로 example.com에 대해 리다이렉트를 시켰는데
요구사항이 설정되지 않은 서브도메인 ex) abcd.example.com, ffff.example.com에 대해서도 리다이렉트 시키는 것이었다.

\*.example.com이게 CNAME 레코드로 설정되어있고
이외에 현재 사용하고 있는 서브도메인으로 api.example.com, shop.example.com이 있었다

우선 해당 로드밸런서에서 마지막 평가기준(아무것도 해당되지 않을때) example.com으로 리다이렉트를 시키는 평가기준을 넣었다.

생각을 해보자 api.example.com, shop.example.com들은 언제 빠지는가?
위 api.example.com, shop.example.com은 A레코드로 다른 로드밸런서로 빠지긴 한다

현재 가정은 A레코드가 먼저 평가되고 그다음 CNAME레코드가 평가된다.

A recode는 fixed한 ip를 domain과 연결
cname은 domain과 domain을 연결

++
A recode,  
cname  
nx domain