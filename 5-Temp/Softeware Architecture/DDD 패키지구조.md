---
date: 2024-05-07 18:06:48
updatedAt: 2024-05-07 18:07:04
---
질문있습니다!

도메인별로 패키지가 분리되어있다고 가정했을 때,
a도메인의 서비스에서 b도메인의 필드가 필요한 경우 도메인별로 의존성이 분리된 수준을 유지하면서 어떻게 처리해야할까요? 

a서비스에서 b도메인 리포지토리 인터페이스를 인스턴스변수로 선언하여 사용하거나, a컨트롤러에서 b서비스를 쓰는건 다른 패키지와 의존성이 걸리는 것 같아서 안될 것 같고.. 

이벤트로 처리하려니까 반환값이 필요한 경우는 처리 할 수가 없다해서 어떻게 해야할지 고민입니다

Facade 혹은 Usecase 를 두고, 이 계층은 Service 에 대한 규합을 제공한다라는 룰을 가져갑니다.
이에 각 도메인 서비스 끼리는 서로 의존할 수 없고 Facade/UC 에서만 서로 다른 도메인의 서비스에 의존해 특정 비즈니스 유즈케이스를 달성한다. 라는 룰을 가져가면 됩니다.

즉, 프로젝트 구조에서 말씀해주신
a 도메인 - a controller, service, repository 이런 형태가 아니라

api/
  controller/
  usecase/
domain/
  도메인별/


api/
  controller/
    UserController
  usecase/
    GetMeUseCase
    UserCommand
domain/
  user/
    UserService
    UserRepository
        infrastructure/
            UserRepositoryImpl
            UserJpaRepository

이런 형태로 패키지 구조를 가져가면
api ( presentation ) 레벨의 패키지 하위인 usecase 에서 각 domain 의 서비스를 가져다 쓰는게 자연스러워집니다.
위상을 분리해놓았으니까요

#argent 