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
<center>[그림1] API 설정화면 이동</center>

2.[New Domain] 버튼을 클릭하여 Domain 생성화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_02.png)
<center>[그림2] Domain 생성화면 이동</center>

3.플러그인 없이 간단히 Domain Name, Domain Key, Target URL만 입력하고 [Save] 버튼을 클릭하여 도메인을 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_03.png)
<center>[그림3] Domain 생성</center>

### Endpoint 생성하기

**Domain 생성**에서 만든 Domain을 이용해서 Endpoint를 생성해보겠습니다.

1.생성한 Domain 우측 끝에 있는 [Setting] > [Endpoint]를 클릭하여 Endpoint 설정화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_04.png)
<center>[그림4] Endpoint 설정화면 이동</center>

2.[New Endpoint] 버튼을 클릭하여 새 Endpoint를 만들고 Method는 GET, Path는 /hello로 설정하고 [Save] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/img_05.png)
<center>[그림4] Endpoint 생성</center>

### Domain 복제하기 
기존에 등록한 Domain과 하위 Endpoint 설정을 그대로 복제할 수 있습니다. 

1. Doamin 리스트 페이지에서 복제할 Domain의 [Setting] > [Clone from domain]을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/img_gettingstarted_5.png)
<center>[그림5] 복제할 Doamin 선택</center>

2. 복제할 Domain의 설정 정보를 입력한 후 저장합니다. 

![](http://static.toastoven.net/prod_apigateway/img_gettingstarted_6.png)
<center>[그림6] 복제 Domain 설정</center>


### Swagger Import & Export
swagger 파일을 import하여 domain을 등록하거나 등록된 domain을 swagger 파일로 export 할 수 있습니다.

#### Swagger Export
1. Export할 도메인의 [Setting] > [Export swagger]를 클릭하면 swagger 파일이 다운로드 됩니다. (기본 파일명: export.json)
![](http://static.toastoven.net/prod_apigateway/img_gettingstarted_7.png)
<center>[그림7] Domain Export</center>


#### Swagger Import
1. swagger spec을 참고하여 swagger 파일을 작성합니다.
	- [Swagger Specification](http://swagger.io/docs/specification/what-is-swagger/)
2. TOAST Cloud API Gateway 에서 제공하는 플러그인 설정을 추가하려면 x-toastcloud-apigw 확장 설정 정보를 추가합니다.
  - 예시)
```json
{
	"swagger": "2.0",
	"info": {
		"version": "2017-05-12T18:34:14.000+09:00",
		"title": "apigw example"
	},
	"host": "alpha-api-gw.cloud.toast.com",
	"basePath": "/example_apigw",
	"schemes": [
		"http"
	],
	"paths": {
		"/v1.0/apigw/**": {
			"get": {
				"parameters": [],
				"x-toastcloud-apigw": {
					"plugins": {
						"MOCK": {
							"statusCode": 200,
							"headers": {
								"x-cloudtoast-apigw": "mock_value"
							},
							"body": "mock response"
						},
						"ENDPOINT_USAGE_QUOTA": {
							"usageQuotaBeans": [
								{
									"maxUsageQuota": 1,
									"resetTimeSeconds": 10
								}
							]
						},
						"PRE_API": {
							"method": "GET",
							"url": "http://cloud.toast.com"
						},
						"HEADER": {
							"requestHeaders": {
								"x-cloudtoast-apigw-request": "add_request_header"
							},
							"responseHeaders": {
								"x-cloudtoast-apigw-response": "add_response_header"
							}
						},
						"CACHE": {
							"timeToLiveSeconds": 100
						}
					}
				}
			}
		}
	},
	"x-toastcloud-apigw": {
		"plugins": {
			"MAINTENANCE": {
				"isUse": true,
				"statusCode": 200,
				"headers": {
					"x-toastcloud-apigw": "value"
				},
				"body": "maintenance"
			},
			"IPACL": {
				"isPermit": true,
				"ipList": [
					{
						"ip": "192.168.0.1"
					}
				]
			},
			"HMAC": {
				"secretKey": "hmac_scret_key",
				"clockSkew": 100
			},
			"HTTP_PROXY": {
				"url": "http://cloud.toast.com"
			},
			"USAGE_QUOTA": {
				"usageQuotaBeans": [
					{
						"maxUsageQuota": 1,
						"resetTimeSeconds": 10
					}
				]
			},
			"URI_REWRITE": {
							"uriPattern": "/{version}/{path}",
							"rewriteUri": "/{path}/{version}"
			}
		}
	}
}
```
3. Domain 기본 정보 설정
	* swagger : swagger 버전 정보를 입력합니다. (swagger 2.0 버전 기본 지원)
	* info: 기본 정보를 입력합니다.
		* version: 버전 정보를 입력합니다.
		* title: domain name 정보를 입력합니다.
	* host: api gateway domain 정보를 입력합니다.
	* basePath: domain key 정보를 입력합니다.
	* schemes: scheme 정보를 입력합니다. (http/https 중 하나만 입력)
	* paths: endpoint path 정보를 입력합니다.

4. Domain Plugin 설정
	* Domain plugin은 최상위 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
	* HTTP_PROXY : Domain의 Targer server url을 입력합니다. (* 입력 필수)
	* IPACL : Domain의 Access Control > IP ACL 플러그인 설정 정보를 입력합니다. (Access Control 그룹 중 하나만 입력 가능)
	* HMAC : Domain의 Authentication > HAMC 플러그인 설정 정보를 입력합니다. (Authentication 그룹 중 하나만 입력 가능)
	* JWT : Domain의 Authentication > JSON Web Token (JWT) 플러그인 설정 정보를 입력합니다. (Authentication 그룹 중 하나만 입력 가능)
	* USAGE_QUOTA : Domain의 Quota Limit > Usage Quota 플러그인 설정 정보를 입력합니다. (Quota Limit 그룹 중 하나만 입력 가능)
	* MAINTENANCE : Domain의 Maintenance > Maintenance Response 플러그인 설정 정보를 입력합니다.  (Maintenance 그룹 중 하나만 입력 가능)

5. Endpoint Plugin 설정
	* Endpoint plugin은 각 paths 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
	* MOCK : Mock Response 플러그인 설정 정보를 입력합니다.
	* ENDPOINT_USAGE_QUOTA: Usage Quota 플러그인 설정 정보를 입력합니다.
	* PRE_API: Pre API 플러그인 설정 정보를 입력합니다.
	* HEADER: Modify  플러그인 설정 정보를 입력합니다.
	* CACHE: Cache 플러그인 설정 정보를 입력합니다.
	* URI_REWRITE: URL Rewrite 플러그인 설정 정보를 입력합니다.

6. Import domain 버튼을 클릭하고 import할 swagger file을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_gettingstarted_8.png)
<center>[그림8] Domain Import</center>

7. Import 버튼을 클릭하면 swagger file의 설정 정보대로 Domain이 등록됩니다.
![](http://static.toastoven.net/prod_apigateway/img_gettingstarted_9.png)
<center>[그림9] Domain Import</center>

### API 배포하기

Domain 목록 우측에 있는 [Deploy] 버튼을 눌러 API를 배포합니다.

![](http://static.toastoven.net/prod_apigateway/img_06.png)
<center>[그림7] API 배포</center>

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
<center>[그림8] 통계 대시보드 화면 이동</center>

2.왼쪽 상단에 있는 달력 아이콘으로 API 사용 기간을 조작해서 API 사용 결과가 기간에 따라 달라지는 것을 확인해봅니다.

![](http://static.toastoven.net/prod_apigateway/img_08.png)
<center>[그림9] 기간별 통계</center>

3.Domain 목록을 클릭하여 Domain에 대한 상세한 통계를 확인합니다.

![](http://static.toastoven.net/prod_apigateway/img_09.png)
<center>[그림10] Domain별 통계</center>

![](http://static.toastoven.net/prod_apigateway/img_10.png)
<center>[그림11] 상세 통계 정보</center>
