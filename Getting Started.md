## Upcoming Products > API Gateway > Getting Started 

> ※ 본 문서는 alpha 개발 단계의 문서입니다.
> 사용에 관심이 있으신 분은 **support@cloud.toast.com**으로 문의해 주시기 바랍니다.

본 문서에서는 웹콘솔을 이용하여 API Gateway를 구성하고 이용하는 방법을 설명합니다.

### 서비스 활성화

Console의 [Upcoming Products] > [API Gateway]를 선택한 후 [상품이용] 버튼을 클릭하여 서비스를 활성화합니다.

### Domain 생성하기

간단히 플러그인이 없는 Domain을 생성해보도록 하겠습니다.  

1.[API Gateway] > [API Setting] 를 클릭하여 API 설정 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_01.png)

2.[New Domain] 버튼을 클릭하여 Domain 생성화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_02.png)

3.플러그인 없이 간단히 Domain Name, Domain Key, Target URL만 입력하고 [Save] 버튼을 클릭하여 도메인을 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_03.png)

### Endpoint 생성하기

**Domain 생성**에서 만든 Domain을 이용해서 Endpoint를 생성해보겠습니다.

1.생성한 Domain 우측 끝에 있는 [Setting] > [Endpoint]를 클릭하여 Endpoint 설정화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_04.png)

2.[New Endpoint] 버튼을 클릭하여 새 Endpoint를 만들고 Method는 GET, Path는 /hello로 설정하고 [Save] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/img_05.png)

### API 배포하기

Domain 목록 우측에 있는 [Deploy] 버튼을 눌러 API를 배포합니다.

![](http://static.toastoven.net/prod_apigateway/img_06.png)

### 생성한 API 테스트

앞에서 Domain과 Endpoint를 만들어봤습니다. 생성한 API가 의도한대로 잘 동작하는지 테스트를 해보도록 하겠습니다. Endpoint에 요청을 보내고 기대한 응답이 오는지 확인해봅니다.

```bash
$ curl -s http://apis.apigw.com/myDomain/hello
hi!
```

### 통계 확인하기

**! 배치를 통해 통계가 쌓이기 때문에 아직 데이터가 없을 수 없습니다.**

1.[API Gateway] > [Dashboard] 를 클릭하여 대시보드 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_07.png)

2.왼쪽 상단에 있는 달력 아이콘으로 API 사용 기간을 조작해서 API 사용 결과가 기간에 따라 달라지는 것을 확인해봅니다.

![](http://static.toastoven.net/prod_apigateway/img_08.png)

3.Domain 목록을 클릭하여 Domain에 대한 상세한 통계를 확인합니다.

![](http://static.toastoven.net/prod_apigateway/img_09.png)

![](http://static.toastoven.net/prod_apigateway/img_10.png)
