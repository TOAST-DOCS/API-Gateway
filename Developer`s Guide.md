## Upcoming Products > API Gateway > Developer's Guide

> ※ 본 문서는 alpha 개발 단계의 문서입니다.
> 사용에 관심이 있으신 분은 **support@cloud.toast.com**으로 문의해 주시기 바랍니다.

이 문서는 API Gateway의 구조와 기능 및 사용법을 서술합니다.

## 서비스 구조

![](http://static.toastoven.net/prod_apigateway/img_11.png)

## 플러그인 동작 구조

![](http://static.toastoven.net/prod_apigateway/img_12.png)

Domain에 추가한 플러그인은 Domain에 속한 모든 API에 대해서 동작합니다. 마찬가지로 Endpoint에 추가한 플러그인은 Endpoint에 대해 API call이 수행될 때 동작합니다.

## 기능

#### Domain 관리

하나의 Domain은 대상 서버를 가르키는 Domain URL 하나에 대응됩니다. Domain은 생성, 편집, 삭제가 가능합니다. 그리고 Domain에 대해 플러그인을 설정할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_13.png)

웹콘솔의 [API Gateway] > [API Setting] 을 클릭하여 Domain 관리 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_14.png)

#### Endpoint 관리

Endpoint는 API에 접근 가능한 Endpoint를 의미합니다. 그러므로 하나의 Endpoint는 API 한 개에 대응됩니다. Endpoint는 생성, 편집, 삭제가 가능합니다. 그리고 Endpoint에 대해 플러그인을 추가, 편집, 삭제가 가능합니다.

![](http://static.toastoven.net/prod_apigateway/img_15.png)

Domain 목록에서 관리할 Domain의 가장 우측에 있는 [Setting] > [Endpoint]를 클릭하여 Endpoint 관리 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_16.png)

```
URI가 같더라도 HTTP Method가 다르면 다른 Endpoint입니다.
```

#### API 통계

API 통계는 사용자가 등록한 Domain들에서 발생한 API call의 사용량과 평균응답시간을 나타냅니다. Domain 목록 중 하나를 클릭하여 특정 Domain에 대한 통계를 차트와 Endpoint별 통계로 좀 더 자세히 확인할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_17.png)

![](http://static.toastoven.net/prod_apigateway/img_18.png)

웹콘솔에서 [API Gateway] > [Dashboard]를 클릭하여 통계 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_19.png)

### 사용법

#### Domain 생성

1.[New Domain] 버튼을 클릭하여 Domain 생성화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_20.png)

2.Domain 설정 폼을 채우고 [Save] 버튼을 클릭하여 Domain을 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_21.png)

#### Domain 편집

1.Domain 목록에서 편집할 Domain 우측에 있는 [Setting] > [Domain] 버튼을 클릭하여 Domain 편집 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_22.png)

2.Domain 설정을 변경하고 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_23.png)

#### Domain 삭제

1.Domain 목록에서 삭제할 Domain 우측에 있는 [Setting] > [Delete] 버튼을 클릭하면 Domain 삭제 팝업이 나타납니다.

![](http://static.toastoven.net/prod_apigateway/img_24.png)

2.삭제할 Domain을 다시 한번 확인하고 Domain 이름을 입력해서 삭제를 합니다.

![](http://static.toastoven.net/prod_apigateway/img_25.png)

> 주의 : 삭제한 Domain은 복구할 수없습니다. 삭제 시도시 사용자로부터 Domain 이름을 입력 받아서 확인을 합니다.

#### Endpoint 생성

1.Endpoint 목록에서 [New Endpoint] 버튼을 클릭하여 새 Endpoint를 추가합니다.

![](http://static.toastoven.net/prod_apigateway/img_26.png)

2.빈 칸을 채우고 우측에 있는 [Save] 버튼을 클릭하여 Endpoint를 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_27.png)

#### Endpoint 편집

1.Endpoint 목록에서 편집할 Endpoint 우측에 있는 [Edit] 버튼을 클릭하여 편집을 시작합니다.

![](http://static.toastoven.net/prod_apigateway/img_28.png)

2.설정을 수정하고 우측에 있는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_29.png)

#### Endpoint 삭제

1.Endpoint 목록에서 삭제할 Endpoint 우측에 있는 [Delete] 버튼을 클릭하여 삭제합니다.

![](http://static.toastoven.net/prod_apigateway/img_30.png)

#### Endpoint Plugin 추가

1.Plugin을 추가할 Endpoint 우측에 있는 [+] 버튼을 클릭하면 나타나는 Plugin 목록에서 원하는 Plugin을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/img_31.png)

2.Plugin 설정 폼을 채우고 우측에 있는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_32.png)

#### Endpoint Plugin 편집

1.편집할 Plugin을 클릭하여 편집 화면을 보이게 합니다.

![](http://static.toastoven.net/prod_apigateway/img_33.png)

2.설정을 수정하고 우측에 보이는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_34.png)

#### Endpoint Plugin 삭제

1.삭제할 Plugin을 클릭하여 편집 화면을 보이게 합니다.

![](http://static.toastoven.net/prod_apigateway/img_35.png)

2.우측에 보이는 [Delete] 버튼을 클릭하여 삭제합니다.

![](http://static.toastoven.net/prod_apigateway/img_36.png)

### Domain Plugin

#### Access Control

- IP ACL : IP 기반 Access Control

#### Authentification

- HMAC
- JWT (JSON Web Token)

#### Qouta Limit

- Usage Quota : 시간당 API 사용량 제한

### Endpoint Plugin

- Mock : Response Mock
- Cache : API 결과 Cache
