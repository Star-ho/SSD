괜히 unix 소켓 까지 애기해서 조금 헷갈려 하실수도 있을거 같아서 rephrase 해드리면..

TCP 소켓은 새로운 클라이언트가 서버에 붙으면 프로세스가 해당 TCP 커넥션 처리를 위해 소켓을 열거든요. 이때 소켓의 ID 혹은 이름은 client(혹은 target)ip, protocal 이라서 당연히 포트 65535개 제한 이상 소켓이 열릴 수 있어요.

실제로 서버의 프로세스가 시작되면 커넥션을 받도록 listening 소켓을 포트(80, 443 같은)에 바인딩 시켜서 열어 높습니다(그래서 실제로 netstat 찍어보면 listening 이라고 프린트됨) 그리고 클라/서버간의 커넥션이 established 되면 기존에 리스닝 하고 있는 소켓을 클론해 ip+ 포트 이름 으로 "서비스 소켓"을 만들고 그 소켓을 통해서 서버/클라가 통신 합니다. 간혹 connection이 진짜 빡세게 한번에 몰리는 경우(예를 들면 게임 점검 후에 사용자가 한번에 spike 되는 상황)엔 TCP 핸쉑 로직 안에서도 backlog queue(기본 1024)가 있어서에서 드랍되는 경우가 있는데 tcp_max_syn_backlog 사이즈도 커널 파라미터로 수정 가능해요

https://www.oreilly.com/library/view/the-sockets-networking/0131411551/
기본적인 Linux/Unix 네턱 통신 관련해서 바이블이긴 한데