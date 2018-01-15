## Application Service > API Gateway > 개요

> ※ 본 문서는 alpha 개발 단계의 문서입니다.
> 사용에 관심이 있으신 분은 **support@cloud.toast.com**으로 문의해 주시기 바랍니다.



## API Gateway 개요 

API Gateway는 사용자의 API 생성과 배포 관리를  손쉽게 할 수 있는 서비스를 제공합니다. 
접근 제한, 트래픽 제어, 메시지 변조 방지 등의 유용한 플러그인을 제공합니다. 


## 주요 기능 

- API 생성, 배포, 관리 

  API Gateway는 사용자의 API의 리소스와 메서드를 손쉽게 관리하고 배포할 수 있습니다.
  API Gateway에서 제공하는 프런트 엔드 포인트를 통해 사용자의 API를 노출시킬 수 있습니다. 
  사용자 API 서버마다 API Gateway를 만들지 않아도 되므로 비용이 절감됩니다.

- 다양한 플러그인 제공 
  접근 제한(IP ACL), 메시지 변조 방지(HMAC, JWT), 트래픽 관리(Throttling) 등의 다양한 플러그인 기능을 제공합니다.
  API Gateway 플러그인에서 제공하는 기능을 이용하면 개발자는 주 비즈니스 로직 개발에만 집중할 수 있습니다. 

- 다양한 통계 정보 제공 
  API Call Count, HTTP Response Code별 통계, 평균 응답속도, 네트워크 트래픽 사용량에 대한 정보를 제공합니다.

- 모니터링 
  모니터링 플러그인을 통해 사용자의 API 서버의 장애를  API Gateway가 탐지하고 알림을 전송합니다. 

## API Gateway 서비스 흐름 

![[그림1] 서비스 구조](http://static.toastoven.net/prod_apigateway/overview/service_flow.png)

Client는 API Gateway에서 제공하는 Domain url을 통해 사용자의 Target API Server의 Target Url을 호출 할 수있습니다.
API Gateway Console에서 부가적인 Plugin 설정을 하는 것만으로 Access Control, Authentification 등의 기능을 추가 할 수 있습니다. 

## 용어 정리 

| 용어        | 설명                                       |
| --------- | ---------------------------------------- |
| DomainKey | API 제공자가 가지는 고유키 ex) exampleDomain       |
| TargetUrl | 사용자 API Server의 api url  ex) http://api-myservice.cloud.toast.com |
| DomainUrl | API Gateway를 통해 노출되는 대상 서버에 대한 URL ex) https://api-gw.cloud.toast.com/example |
| Endpoint  | API Gateway를 통해 노출시킬 API                 |
| Plugin    | Domain 혹은 Endpoint에 연결되어 API에 적용되는 플러그인 ex) ACL, Authentification |
