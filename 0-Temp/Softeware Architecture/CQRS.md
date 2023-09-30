https://blog.ploeh.dk/2014/08/11/cqs-versus-server-generated-ids/

Dependency Injection in .NET을 쓴 Mark Seemann
생성자 혹은 정적 팩토리 메소드를 호출하는 건 CQS의 command일까요
성능을 위해서 조회 기능 뒤에 캐시를 넣는 경우 조회 과정에서 캐시의 상태가 변경이 됩니다. 이건 cqs를 잘 지키는 query일까요
마이어의 object oriented software construction에는 CQS라는 소제목도 없습니다. CQS는 side effects in functions의 한 내용으로 나오죠. 
중요한 건 side effect를 어떻게 다룰 것인가이고, cqs는 결국 그걸 목적으로 하는 거라는.
command는 procedure로,  function은 공개 attribute 또는 function으로 만들어진다고.
핵심은 query는 다음 query에 영향을 주는 변경을 만들면 안 된다는 것이고.
command에 리턴 값이 없어야 하는 이유는 그러면 function이 되버리니까, 결국 query가 되는 셈이고, 그러면 referential transparency를 충족하지 못하는 function이기 때문이죠. 
마틴 파울러가 마이어의 stack pop 구현을 query + command의 두 가지 작업으로 분리하라고 했던 것과 달리, 그런 경우엔 자기는 예외를 둔다라고 했던 것처럼
db 생성 id가 만들어지는 command에서 그 값을 리턴 받는 것도 충분히 가능하다고 봅니다. 
그걸 query라고 생각하고 쓸 바보 같은 다른 개발자가 있지 않다면. 
그게 아니면 last inserted id 이런 값을 repository가 가지고 있게 해서 그걸 조회하는 query를 만들어야 하는데, 이게 멀티쓰레드 무상태 서버 사이드 서비스 오브젝트에 가당할 리가 없죠. 
물론 db id를 미리 생성해서 넘길 수 있다면 별 상관없겠지만. 혹은 자연키를 쓴다거나. 
어제 질문하셨던 분 이야기도 생각이 나고 해서 (command내에서 db query를 해도 되는가). 