## Upcoming Products > API Gateway > Overview
> ※ 본 문서는 alpha 개발 단계의 문서입니다.
> 사용에 관심이 있으신 분은 **support@cloud.toast.com**으로 문의해 주시기 바랍니다.

API를 생성, 관리, 배포, 통계, 모니터링 할 수 있으며, 플러그인을 사용하여 API에 부가기능을 더할 수 있는 서비스입니다.

## 특/장점

- 대상 API 서버마다 API Gateway를 만들지 않아도 되므로 비용이 절감됩니다.
- 클릭 몇 번 만으로 API에 접근제어와 같은 부가기능을 더할 수 있습니다.
- 통계를 통해 API 사용량과 응답시간 등을 모니터링 할 수 있습니다.

## 주요 기능

- API 생성, 관리, 배포
- API를 대상 서버로 프록시
- 다양한 플러그인 기능 제공
- API 사용량과 실패율 및 응답시간 통계 제공

## 서비스 용어

|용어|	설명|
|---|---|
|Domain|	API 제공자|
|DomainKey|	API 제공자가 가지는 고유키 ex) exampleDomain|
|TargetUrl|	API 제공자의 대상 서버 ex) http://api.target.server.com|
|DomainUrl|	API Gateway를 통해 노출되는 대상 서버에 대한 URL ex) https://api-gw.cloud.toast.com/example|
|Endpoint|	API Gateway를 통해 노출시킬 API|
|Plugin|	Domain 혹은 Endpoint에 연결되어 API에 적용되는 플러그인 ex) ACL, Authentification|
