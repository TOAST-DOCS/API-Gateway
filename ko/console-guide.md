## Application Service > API Gateway > 콘솔 사용 가이드

## API Gateway 활성화 

API Gateway 상품을 활성화하려면 콘솔에서 상품을 추가할 프로젝트를 선택한 후, 서비스 선택에서 [Application Service] > [API Gateway]를 클릭하여 활성화합니다. 

## 도메인

### 도메인 생성 

1.콘솔에서 [API Gateway] > [API Setting] 버튼을 클릭합니다.

2.[New Domain] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/console/new_domain.png)
<center>[그림1] Domain 생성 화면 이동</center>

3.Domain Setting을 설정합니다. 

![](http://static.toastoven.net/prod_apigateway/console/add_domain_setting.png)
<center>[그림2] 도메인 설정</center>

- Domain Name: 도메인의 별칭입니다. 도메인 이름을 등록하여 각 도메인을 구분하는 용도로 사용할 수 있습니다.
- Domain Key: 도메인의 고유한 키입니다. 키 값은 API Gateway의 Endpoint URL에 사용이 됩니다.(api-gw.cloud.toast.com/{domainKey})
  - Domain Key값은 path 형식의 값은 사용할 수 없습니다. (ex: /apis/gateway 사용 불가)
- Target URL: API Gateway가 요청을 포워딩할 사용자 API 서버의 URL을 입력합니다. 
- Scheme: API Gateway가 제공하는 Domain url의 scheme 을 선택합니다.

4.Plugin Setting에서 플러그인을 추가합니다. 

도메인 단위에 적용한 플러그인은 도메인 하위의 엔드 포인트에 공통적으로 적용됩니다.

![](http://static.toastoven.net/prod_apigateway/console/add_domain_plugins.png)

<center>[그림3] 도메인 플러그인 설정</center>

5.[Save] 버튼을 클릭합니다.

### 도메인 편집

1.[Setting] > [Domain] 버튼을 클릭하여 Domain 편집 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/console/domain_edit.png)
<center>[그림4] Domain 편집 </center>

2.Domain 설정을 변경하고 [Save] 버튼을 클릭하여 저장합니다.

### 도메인 삭제

1.[Setting] > [Delete] 버튼을 클릭하면 Domain 삭제 다이얼로그가 화면에 표시됩니다.

![](http://static.toastoven.net/prod_apigateway/console/domain_delete.png)
<center>[그림5] Domain 삭제</center>

2.삭제할 Domain을 다시 한번 확인하고 도메인 키를 입력하면 삭제가 됩니다.

![](http://static.toastoven.net/prod_apigateway/console/domain_delete_popup.png)
<center>[그림6] Domain 삭제 확인</center>

> 주의 : 삭제한 Domain은 복구할 수없습니다. 삭제 시도시 사용자로부터 Domain 이름을 입력 받아서 확인을 합니다.



### 도메인 복제

기존에 생성한 Domain의 설정을 복제하여 새로운 Domain을 생성할 수 있습니다. 

1.복제할 Domain의 [Setting] > [Clone from domain]을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/getting_started/getting_started_import_domain.png)
<center>[그림7] 복제할 Doamin 선택</center>

2.복제하여 새로 생성할 도메인에서 변경이 필요한 설정 정보를 수정 후 [Save] 버튼을 클릭합니다. 

![](http://static.toastoven.net/prod_apigateway/console/domain_clone.png)
<center>[그림8] 복제 Domain 설정</center>





### Swagger Import & Export

swagger 파일을 import하여 domain을 등록하거나 등록된 domain을 swagger 파일로 export 할 수 있습니다.

#### Swagger Export

1.Export할 도메인의 [Setting] > [Export swagger]를 클릭하면 swagger 파일이 다운로드 됩니다. (기본 파일명: export.json)
![](http://static.toastoven.net/prod_apigateway/console/domain_swagger.png)
<center>[그림9] Domain Export</center>

#### Swagger Import

1.swagger spec을 참고하여 swagger 파일을 작성합니다.

- [Swagger Specification](http://swagger.io/docs/specification/what-is-swagger/)

2.TOAST Cloud API Gateway 에서 제공하는 플러그인 설정을 추가하려면 x-toastcloud-apigw 확장 설정 정보를 추가합니다.

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

#### Domain 기본 정보 설정

- swagger : swagger 버전 정보를 입력합니다. (swagger 2.0 버전 기본 지원)
- info: 기본 정보를 입력합니다.
  - version: 버전 정보를 입력합니다.
  - title: domain name 정보를 입력합니다.
- host: api gateway domain 정보를 입력합니다.
- basePath: domain key 정보를 입력합니다.
- schemes: scheme 정보를 입력합니다. (http/https 중 하나만 입력)
- paths: endpoint path 정보를 입력합니다.

#### Domain Plugin 설정

- Domain plugin은 최상위 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
- HTTP_PROXY : Domain의 Targer server url을 입력합니다. (* 입력 필수)
- IPACL : Domain의 Access Control > IP ACL 플러그인 설정 정보를 입력합니다. (Access Control 그룹 중 하나만 입력 가능)
- HMAC : Domain의 Authentication > HAMC 플러그인 설정 정보를 입력합니다. (Authentication 그룹 중 하나만 입력 가능)
- JWT : Domain의 Authentication > JSON Web Token (JWT) 플러그인 설정 정보를 입력합니다. (Authentication 그룹 중 하나만 입력 가능)
- USAGE_QUOTA : Domain의 Quota Limit > Usage Quota 플러그인 설정 정보를 입력합니다. (Quota Limit 그룹 중 하나만 입력 가능)
- MAINTENANCE : Domain의 Maintenance > Maintenance Response 플러그인 설정 정보를 입력합니다.  (Maintenance 그룹 중 하나만 입력 가능)

#### Endpoint Plugin 설정

- Endpoint plugin은 각 paths 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
- MOCK : Mock Response 플러그인 설정 정보를 입력합니다.
- ENDPOINT_USAGE_QUOTA: Usage Quota 플러그인 설정 정보를 입력합니다.
- PRE_API: Pre API 플러그인 설정 정보를 입력합니다.
- HEADER: Modify  플러그인 설정 정보를 입력합니다.
- URI_REWRITE: URL Rewrite 플러그인 설정 정보를 입력합니다.

3.Import domain 버튼을 클릭하고 import할 swagger file을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/domain_import.png)
<center>[그림10] Domain Import</center>

4.Import 버튼을 클릭하면 swagger file의 설정 정보대로 Domain이 등록됩니다.
![](http://static.toastoven.net/prod_apigateway/console/domain_swagger_upload.png)
<center>[그림11] Domain Import</center>







## 엔드 포인트

### 엔드 포인트 생성

엔드 포인트는 사용자의 API 중  API Gateway를 통해 제공할 API를 관리합니다.

1.엔드 포인트를 생성할 도메인의 [Setting] > [Endpoint]를 클릭합니다. 

![](http://static.toastoven.net/prod_apigateway/console/move_endpoint_setting.png)

<center>[그림12] 엔드 포인트 설정 화면 이동</center>

2.[New Endpoint] 버튼을 클릭 후 엔드 포인트의 HTTP Method와 Path를 설정합니다.

![](http://static.toastoven.net/prod_apigateway/console/add_endpoint.png)
<center>[그림13] 엔드포인트 생성</center>

3.플러그인 추가는 [+] 버튼을 클릭한 후, 추가할 플러그인을 선택하고 설정값을 입력합니다

![](http://static.toastoven.net/prod_apigateway/console/add_endpoint.png)
<center>[그림14] 엔드 포인트 플러그인 추가</center>

4.[Save] 버튼을 클릭합니다.

>  [참고] Endpoint URI Pattern
>  Endpoint URI Pattern을 AntPattern 형식으로 입력할 경우, 하나의 Endpoint URI Pattern을 통해 복 수개의 API와 대응시킬 수 있습니다. 
>
>  [AntPattern 예시]
>
>  - ? : 하나의 문자와 대치. e.g. /docs/te?t : /docs/test , /docs/text 
>  - \* : 0개 또는 하나 이상의 문자와 대치   e.g. /docs/*.txt : /docs/example1.txt, /docs/example2.txt
>  - \*\* : 0개 또는 하나 이상의 path와 대치   e.g. /docs/** : /docs/apigw/guide, /docs/image/guide
>  - {[a-z]+} : path variable에 대치   e.g. /v1.0/appKeys/{appKey} : /v1.0/appKeys/myAppKey1, /v1.0/appKeys/myAppKey2 



### 엔드 포인트 편집

1.엔드 포인트 목록에서 편집할 Endpoint 우측에 있는 [Edit] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_edit.png)
<center>[그림15] Endpoint 편집</center>

2.설정을 수정하고 우측에 있는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_delete_save.png)
<center>[그림16] Endpoint 편집 정보 저장</center>



### 엔드 포인트 삭제

1.Endpoint 목록에서 삭제할 Endpoint 우측에 있는 [Delete] 버튼을 클릭하여 삭제합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_delete.png)
<center>[그림17] Endpoint 삭제</center>



### 엔드포인트 플러그인 편집

1.편집할 Plugin을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_edit_plugin.png)
<center>[그림18] Endpoint Plugin 편집</center>

2.설정을 수정하고  [Save] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_plugin_edit_save.png)
<center>[그림19] Endpoint Plugin 편집 저장</center>

### 엔드 포인트 플러그인 삭제

1.삭제할 Plugin을 클릭합니다.

2.[Delete] 버튼을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/console/endpoint_plugin_delete.png)
<center>[그림20] Endpoint Plugin 삭제</center>

## 플러그인 

### 플러그인 동작 구조

API Gateway는 접근제어, 인증, 사용량 제한, 메시지 변조 등의 다양한 플러그인을 제공합니다.

플러그인은 도메인과 엔드포인트에 적용할 수 있습니다. 도메인 계층에 추가한 플러그인은 해당 도메인의 하위 엔드 포인트에 공통적으로 적용됩니다.

엔드 포인트 계층에 추가한 플러그인 해당 엔드 포인트에만 적용됩니다. 

![](http://static.toastoven.net/prod_apigateway/img_12.png)
<center>[그림21] 플러그인 동작 구조</center>

API Gateway가 요청을 전달받으면 설정된 플러그인의 속성 그룹 순서대로 플러그인을 동작시킵니다.

- Access Control filter에서 제한된 사용자의 요청, 사용 제한 초과 시 요청을 거부합니다. 
- Authentification filter에서 인증되지 않은 요청, 변조된 요청에 대해 요청을 거부합니다. 
- Custom filter에서 요청/응답에 대한 메시지 변조, Mock 응답에 대한 처리를 합니다. 
- Proxy filter에서 사용자의 API 서버로 요청을 포워딩하고 응답 값을 전달받아 요청자에게 전달합니다. 





## 도메인 플러그인 

### IP ACL

IP 기반 접근 제한 기능으로 특정 IP를 allow하거나 deny할 수 있습니다.

1.[API Gateway > API Setting] 에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)

<center>[그림22] 도메인 설정 페이지 이동</center>

2.[Plugin Setting] > [Access Control] > [IP ACL]을 클릭합니다. 
![](http://static.toastoven.net/prod_apigateway/console/plugin_ip_acl.png)
<center>[그림23] IP ACL 플러그인 설정</center>   

3.Permit을 통해 설정된 IP 목록에 대해 allow할 것인지 deny할 것인지 설정합니다. 



- true로 설정할 경우 white list로 동작합니다. (설정된 IP에 대해서만 allow, 그 외 모든 IP는 block)
- false로 설정할 경우 black list로 동작합니다. (설정된 IP에 대해서만 deny, 그 외 모든 IP는 allow)

4.ipv4 형식의 IP를 입력 후 add 버튼을 클릭하여 IP 목록에 추가합니다. 

5.[Save] 버튼을 클릭하여 설정 내용을 저장합니다. 





### Quota Limit

단위 시간당 API 사용량을 제한할 수 있습니다.

1.[API Gateway] > [API Setting]에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)
<center>[그림24] 도메인 설정 페이지 이동</center>

2.[Plugin Setting] > [Quota Limit] > [Usage Quota]를 선택합니다. 
![](http://static.toastoven.net/prod_apigateway/console/plugin_usage_quota.png)<center>[그림25] Usage Quota 설정</center>

3.사용량 제한 조건 설정합니다. 



- Max Usage Quota에 최대 API 호출 가능 횟수를 지정합니다. 
- Per(sec)에 초 단위의 시간을 지정합니다. 

4.단위 시간 동안 최대 호출 횟수를 초과할 경우 API 사용이 제한됩니다. 

복 수개의  사용량 제한 조건을 추가할 수 있으며, 설정된 제한 조건 중 하나 이상의 조건이 제한량을 초과할 경우 사용이 제한됩니다. 

> [참고]
> 도메인 설정 페이지에서 설정한 [Usage Quota] 플러그인은 도메인 하위 모든 엔드 포인트의 API 사용량에 대한 제한입니다.  
> 엔드 포인트별로 사용량 제한이 필요한 경우 엔드 포인트의 [EndPoint Usage Quota] 플러그인을 적용해주세요.  





### Maintenance

정기점검 등의 이유로 모든 Endpoint API 호출에 대해서 사용자가 정의한 Response를 반환하도록 설정이 필요한 경우 [Maintenance] 플러그인 사용할 수 있습니다.

1.[API Gateway] > [API Setting] 에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)
<center>[그림26] 도메인 설정 페이지 이동</center>

2.[Plugin Setting > Maintenance] 에서 Maintenance Response 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_maintenance.png)
<center>[그림27] Maintenance Response 플러그인 설정</center>

3.응답 설정값 입력 후 [Save] 버튼을 클릭하여 저장합니다. 

4.Deploy 후 Endpoint API 호출에 대해서 Maintenance 플러그인에 설정된 응답이 반환됩니다.





### HMAC

요청 URL과 시간을 메시지로 사용하여 HMAC 인증을 합니다.

1.[API Gateway] > [API Setting] 에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)
<center>[그림28] 도메인 설정 페이지 이동</center>

2.[Plugin Setting] > [Authentication]에서 HMAC 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_hmac.png)
<center>[그림29] HMAC 플러그인 설정</center>

> [주의] Clock skew 설정  
> APIGW 서버의 시간과 Client에서 보낸 X-TC-Timestamp 사이의 차가 Clock Skew보다 크면 HMAC 인증에 실패하게 됩니다.  
> Clock Skew 값으로 설정 가능한 범위는 0~86400(sec)이며, 만약 0이라면 Clock Skew를 무시합니다.

#### Authentification > HMAC > 인증 API 호출

HMAC 인증을 사용하기 위해서 다음 값을 Request Header에 포함하여 요청해야 합니다.

- Authorization : [Method + "\n "+ URL + "\n "+ Timestamp]를 조합하여 HmacSHA1 알고리즘으로 암호화한 후 Base64로 인코딩 한 값

- X-TC-Timestamp : ISO datetime format (yyyy-MM-dd'T'HH:mm:ssZZ)

| 요청                                       | StringToSign                             |
| ---------------------------------------- | ---------------------------------------- |
| GET /test/1?query1=1&query2=2<br><br>X-TC-Timestamp: 2016-07-23T12:20:02+09:00<br><span style="color:red">Authorization: IqY8u/RZY8IMESwa/TPW9P9Z39Y=</span> | GET\n<br>/test/1?query1=1&query2=2\n<br>2016-07-23T12:20:02+09:00 |

> [참고] 요청 시간은 ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)을 따릅니다.

#### Authorization 생성 코드 (JAVA)
```java
String secretKey = "Console에서 설정한 Secret Key";
SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes(), "HmacSHA1");
Mac mac = Mac.getInstance("HmacSHA1");
mac.init(signingKey);

String message = "StringToSign";
byte[] rawHmac;
rawHmac = mac.doFinal(message.getBytes());
String authorization = new String(Base64.encodeBase64(rawHmac));
```





### JWT (JSON Web Token)

JWT(Json Web Token) 인증을 합니다.

1.[API Gateway] > [API Setting]에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)
<center>[그림30] 도메인 설정 페이지 이동</center>

2.[Plugin Setting] > [Authentication]에서 JWT 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_jwt.png)
<center>[그림31] JWT 플러그인 설정</center>

> [참고]
> APIGW 서버의 시간과 Client에서 보낸 ExpirationTime 사이의 차가 Clock Skew보다 크면 JWT인증에 실패하게 됩니다.  
> Clock Skew 값은 0~86400 사이의 값을 입력할 수 있습니다.  

#### Authorization > JWT (JSON Web Token) > JWT 인증 API 호출

JWT 인증을 사용하기 위해서 다음 값을 Request Header에 포함하여 요청해야 합니다.

- Authorization : Json Web Token

Request: GET /test/1?query1=1&query2=2<br>
 <span style="color:red">Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJpbnZhbGl...</span>

#### Authorization 생성 코드 (JAVA)

```
<dependency>
    <groupId>org.bitbucket.b_c</groupId>
    <artifactId>jose4j</artifactId>
	<version>0.5.0</version>
</dependency>
```

```
String secretKey = "Console에서 설정한 Secret Key";
int expireTimeMinutes = "토큰만료시간 = 현재시간 + expireTimeMinutes";
String issuer = "Console에서 설정한 issuer";

JwtClaims claims = new JwtClaims();
claims.setIssuer(issuer);
claims.setExpirationTimeMinutesInTheFuture(expireTimeMinutes);

JsonWebSignature jws = new JsonWebSignature();
jws.setPayload(claims.toJson());
jws.setKey(new HmacKey(secretKey.getBytes()));
jws.setDoKeyValidation(false);
jws.setAlgorithmHeaderValue(AlgorithmIdentifiers.HMAC_SHA256);

String authorization = jws.getCompactSerialization();
```

#### 



### CORS(Cross-Origin Resource Sharing)

Cross-Site의 방식 내에서의 XMLHttpRequest API 호출이 가능하도록 합니다.

1.[API Gateway > API Setting] 에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)
<center>[그림32] 도메인 설정 페이지 이동</center>

2.[Plugin Setting > CORS] 에서 CORS 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_cors.png)
<center>[그림33] CORS 플러그인 설정</center>

- Allowed credentials: Request with Credential 방식을 사용할 수 있는지를 지정합니다.
- Max credentials Age: Preflight Request의 결과가 캐시에 얼마나 오래 남아 있는지를 지정합니다. 초 단위이며 0~86400 사이의 값을 입력할 수 있습니다.
- Allowed origins: 지정된 도메인만 서버의 리소스에 접근할 수 있도록 지정할 수 있습니다. 
    - *로 입력할 경우 모든 도메인에 대해서 허용합니다. (단, \*로 지정할 경우 credentials를 지원하지 않으므로 allowed origin에 구체적인 도메인을 지정하셔야 합니다.) 
    - 지정된 도메인에서만 허용하도록 할 경우 ,(comma)로 분리하여 입력합니다. 
    - 도메인은 URI(scheme, domain, port) 포맷으로 입력해야 합니다.(ex: http://api-gw.toast.com:8080)
- Allowed methods: 지정된 HTTP Method만 서버 리소스의 접근을 허용합니다.
- Allowed headers: 클라이언트가 리소스 요청시 사용할 수 있는 HTTP Header를 지정합니다. 여러 헤더를 입력할 경우 ,(comma)로 분리하여 입력합니다.
- Exposed headers: 클라이언트에게 노출 할 헤더를 지정합니다. 여러 헤더를 입력할 경우 ,(comma)로 분리하여 입력합니다.
- 자세한 CORS 규약은 https://www.w3.org/TR/cors/ 를 참고 해주세요.





### Monitor

API Gateway의 Proxy에서 사용자의 API 서버의 응답 값이 오류 상태 코드를 전달받았을 때  Email과 SMS을 통해 알림을 받을 수 있는 기능입니다. 

1.[API Gateway > API Setting] 에서 도메인 설정 페이지로 이동합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_domain.png)

<center>[그림34] 도메인 설정 페이지 이동</center>

1.[Plugin Setting] > [Monitor] 을 클릭합니다.

2.모니터링 기본 설정 정보를 입력합니다. 
![](http://static.toastoven.net/prod_apigateway/console/plugin_monitor_default.png)
 <center>[그림35] 모니터링 기본 설정</center>

#### Monitor Type

- Domain: 도메인에서 발생한 전체 에러 발생량에 대해 모니터링을 수행합니다.
  - 하위 모든 Endpoint의 에러 발생량의 합계가 Threshold를 초과 하였을 경우 모니터링 알림이 발송됩니다. 
- Endpoint: 각 Endpoint 에러 발생량에 대해 모니터링을 수행합니다. 
  - 각 Endpoint 별로 Threshold을 초과 하였을 경우 모니터링 알림이 발송됩니다.

#### Monitor Period (모니터 주기 시간, 단위/분) 

- 모니터링 주기 시간(단위/분)을 지정합니다. 

#### Threshold(단위/분)

- 모니터링 주기 시간동안 에러 발생 수가 Threshold를 초과하여 발생하였을 경우 모니터링 알림을 발송합니다. 

#### Snooze(단위/분)

- 모니터링 알림 발생 후 Snooze(분) 시간 동안은 알림을 발송하지 않도록 설정합니다. 
  Threshold 초과 후 에러가 지속적으로 발생할 경우 알림 발송이 과도하게 발생할 수 있으므로, 이 경우 Snooze을 입력해주세요.

3.Notification 설정 

모니터링 알림 발송 수단과 수신 대상자를 설정합니다.

> [참고]  
> 모니터링 플러그인을 이용하려면 Toast Cloud의 Email 또는 SMS 상품을 활성화 후 앱키를 등록하여 사용할 수 있습니다.  
> Email/SMS 상품 이용방법은 해당 상품의 설명서를 참고해주세요.  
> 모니터링 알림 발송으로 인한 발송 요금은 Email과 SMS 상품 이용 요금으로 과금됩니다.   
> 모니터링 알림 발송 내역은 Email 상품 또는 SMS의 발송 내역 조회에서 확인할 수 있습니다.   

![](http://static.toastoven.net/prod_apigateway/console/plugin_monitor_email.png)
 <center>[그림36] 모니터링 Email 알림 설정</center>

Toast Cloud Email AppKey: TOAST Cloud의 Email 상품의 앱 키를 입력합니다. 

Email: 모니터링 알림을 수신 받을 Email 주소를 입력합니다. 


![](http://static.toastoven.net/prod_apigateway/console/plugin_monitor_sms.png)
 <center>[그림37] 모니터링 SMS 알림 설정</center>

Toast Cloud SMS AppKey: TOAT Cloud의 SMS 상품 앱 키를 입력합니다.

Toast Cloud SMS Send number: SMS 발송시 사용 할 발송번호를 입력합니다. 발송번호는 하이픈(-)을 제외한 숫자만 입력해주세요.

Phone Number: 모니터링 알림을 수신 받을 단말기 번호를 입력합니다.  단말기번호는 하이픈(-)을 제외한 숫자만 입력해주세요.

> [참고] 
> 발송 번호는 SMS상품에 등록된 발송 번호만 사용이 가능 합니다. 등록되지 않은 발송 번호는 사용할 수 없습니다.   
> 발송 번호는 등록에 대한 가이드는 SMS 상품의 가이드를 참고해주세요.  

4.Notification 필터

![](http://static.toastoven.net/prod_apigateway/console/plugin_monitor_filter.png)
 <center>[그림38] 모니터링 필터링 설정</center>

API Gateway Monitor 플러그인은 Response의 HTTP Status Code가 400 이상일 경우 에러가 발생한 것으로 판단합니다. 

특정 에러에 대해 알림을 받고 싶지 않은 경우 Response의 HTTP Status 코드와 Response Body 내용으로 필터를 할 수 있습니다. 

> [참고]  
> Filter는 Status Code 또는 Filter String 둘 중 하나는 필수 입력입니다.  
> Status Code 만 입력 할 경우, Response의 HTTP Status Code가 설정한 Status Code에 대해서 필터합니다.  
> Filter String 만 입력한 경우, Response 의 Body 내용에 filter String이 포함된 경우 필터합니다. 대소문자를 구분하지 않습니다. 
> Status Code과 Filter String을 둘 다 입력할 경우 조건(AND/OR)을 설정해야합니다.  
> OR 조건으로 등록한 경우 설정한 Status Code 또는 Response Body에 filter String이 포함될 경우 필터됩니다.   
> AND 조건으로 등록한 경우 설정한 Status Code와 Response Body에 filter String이 포함될 경우 필터됩니다.  

#### 알림 발송 내용 

![](http://static.toastoven.net/prod_apigateway/console/plugin_monitor_notification_info.png)
 <center>[그림39] 모니터링 알림 예시</center>

모니터링 플러그인에 설정한 모니터링 설정에 따라 모니터링 알림 대상자에게 알림이 발송됩니다. 

- 알림 일시: 에러 발생 수가 Threshold를 초과하여 모니터링 알림이 발생한 시간 입니다. 
- Domain Key: 알림이 발생된 API Gateway의 Domain Key 입니다.
- 오류 건 수 : 오류 발생 건 수 입니다.
- [Request/Response] : 마지막으로 오류가 발생한 Request와 Response의 정보입니다. Request와 Response의 데이터 크기가 클 경우 일부만 전송될 수 있습니다. 

> [참고]  
> Error 발생 기준은 Response의 HTTP Status Code가 400 이상의 코드가 반환된 경우 입니다.  
> SMS의 경우 알림 확인 URL이 문자로 발송됩니다.   
> 모니터링 플러그인에서 설정한 발신번호로 https://api-gw.cloud.toast.com/m/XXXX/YY 형식의 URL이 전송됩니다. URL을 반드시 확인 후 열어주세요.   





## 엔드 포인트 플러그인 

### Mock Response

사용자가 미리 설정한 Response Mock 을 반환합니다.

Endpoint Uri pattern에 해당하는 request uri가 요청된 경우, 지정된 Target Server로의 HTTP Proxy를 하지 않고 사용자가 설정한 Mock Response가 response로 반환됩니다. 

![](http://static.toastoven.net/prod_apigateway/console/plugin_mock_response.png)

<center>[그림40] Mock Response 설정</center>

- HTTP Status: response의 status code를 설정합니다.
- Headers: response header에 추가할 헤더와 헤더 값을 설정합니다.
- Body: response body 내용을 설정합니다. 






###  Pre API

Pre API는 Endpoint를 호출하기 전에 호출되며 Pre API의 응답 코드에 따라 Endpoint를 호출 여부를 결정하는 인증 역할을 합니다.

API Gateway를 통해 들어온 요청 헤더를 포함하여 Pre API를 호출하고, Pre API에서는 전달받은 헤더 내용에 따라 응답 코드를 반환하도록 합니다.

Pre API의 응답 코드에 따라 200이면 Endpoint를 호출하고, 응답 코드가 200이 아니면 Pre API의 응답 결과를 리턴합니다.
만약, Pre API 호출에 실패할 경우 에러를 리턴하게 됩니다.

> [참고]  
> API Gateway는 요청의 헤더 정보만 Pre API의 URL로 전달합니다.   
> Request URL 또는 Body 정보는 전달하지 않습니다.  

1.[API Gateway] > [Endpoint] 을 클릭합니다. 
![](http://static.toastoven.net/prod_apigateway/console/move_endpoint.png)
<center>[그림41] Endpoint 설정 화면 이동</center>

2.[Plugins] > [Pre API]를 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_preapi_add.png)
<center>[그림42] Pre API 플러그인 추가</center>

3.Pre API의 Method type과 URL을 입력한 후 [Save]를 클릭합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_preapi.png)
<center>[그림43] Pre API 플러그인 설정</center>

#### 



### Modify Headers

API Gateway가 요청을 Proxy 할 때 요청/응답의 헤더 값을 변조하여 사용자 API 서버에 요청하거나 요청 클라이언트에 응답값을 전달 합니다.

#### Modify Headers 설정

1.[API Gateway > Endpoint] 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/console/move_endpoint.png)
<center>[그림44] Endpoint 설정 화면 이동</center>

2.Plugins > Modify Headers 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_modifyheaders_add.png)
<center>[그림45] Modify Headers 플러그인 추가</center>

3.Plugins > Modify Headers 플러그인 설정 정보를 입력합니다.
![](http://static.toastoven.net/prod_apigateway/console/plugin_modifyheaders.png)
<center>[그림46] Modify Headers 플러그인 설정 정보 입력</center>

Request Headers는 요청 헤더를 수정합니다.

Response Headers는 응답 헤더를 수정합니다.

> [참고]
> 설정한 헤더 키가 이미 존재한다면 덮어쓰게 됩니다.





### Usage Quota

단위 시간동안 Endpoint URI Pattern 별  API 사용량을 제한할 수 있습니다.

#### Usage Quota 설정

1.[API Gateway > Endpoint] 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/console/move_endpoint.png)
<center>[그림47] Endpoint 설정 화면 이동</center>

2.Plugins > Usage Quota 플러그인을 추가한 후 단위 시간(sec) 동안 최대 호출 가능 횟수를 입력합니다.

복 수개의  사용량 제한 조건을 추가 할 수 있으며, 설정된 제한 조건 중 하나 이상의 조건이 제한량을 초과 할 경우 사용이 제한됩니다. 
![](http://static.toastoven.net/prod_apigateway/console/plugin_usagequota.png)
<center>[그림48] Endpoint Usage Quota 플러그인 추가</center>

> [주의]  
> Endpoint Usage Quota는 Endpoint URI 별 사용량 제한이 아닌 URI Pattern별 사용량 제한입니다.    
> Domain 사용량 제한이 필요한 경우 Domain 설정 페이지의 Usage Quota를 설정하세요.    
> Domain 과 Endpoint에 각각 Usage Quota 플러그인을 설정한 경우 각각 사용 제한이 적용됩니다.   
> Domain 사용량 초과시 Endpoint의 사용량이 초과되지 않아도 요청이 거부되며, Endpoint의 사용량 또한 증가됩니다.     

사용량 제한을 초과하였을 경우 아래의 HTTP STATUS 403 response가 반환 됩니다. 

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```





### URL Rewrite

Request URL을 패턴 표현식으로 Rewrite 해주는 플러그인 입니다. 

1.[API Gateway > Endpoint] 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/console/move_endpoint.png)
<center>[그림49] Endpoint 설정 화면 이동</center>

2.URI Pattern에는 어떤 패턴형식의 Request URL에 대해 rewrite 할 것인지 패턴 형식을 입력합니다. 

3.Rewrite URI에는 (2)에서 작성한 URI Pattern 형식에 대해 URL을 Rewrite 할 형식을 입력합니다. 

![](http://static.toastoven.net/prod_apigateway/console/plugin_url_rewrite.png)

#### [예시] /api/v2.0/\*\* -> /api/v1.0/\*\* 로 Rewrite 하는 경우 

- URI Pattern: /api/v2.0/(.\*)


- Rewrite URI: /api/v1.0/%1

위의 규칙을 적용하면 Request URL `/api/v2.0/members` 가` /api/v1.0/members` 로 변경되어 요청됩니다. 

<center>[그림50] Endpoint URL Rewrite 플러그인 추가</center>




## API 배포 

### API 배포

1.배포할 Domain의 [Deploy] 버튼을 클릭합니다. 

![](http://static.toastoven.net/prod_apigateway/getting_started/getting_started_deploy.png)
<center>[그림51] API 배포</center>

2.배포한 API가 정상적으로 호출되는지 테스트를 합니다.
domain url에 등록한 endpoint url을 호출 하였을 때 기대한 Response가 전달되는지 확인합니다. 

```bash
$ curl -s http://api-gw.cloud.toast.com/apigw/hello
hello world
```





## 통계 

### 통계 조회 

API 통계에서는 각 도메인 별 API Call 평균 응답시간, 네트워크 트래픽 사용량을 확인 할 수 있습니다.
통계 데이터는 배포(Deploy)된 Domain에 대해서만 통계 데이터가 출력됩니다.

도메인 목록의 도메인을 클릭하면 해당 도메인에 대한 통계를 차트와 URI 패턴 별 상세 통계 데이터를 확인할 수 있습니다. 
차트는 검색 기간에 따라 10분/1시간/1일 단위의 데이터를 확인할 수 있습니다.

> [참고] 검색기간별 통계 시간 단위  
>
> - 6시간 미만: 10분 단위 
> - 6시간 이상 ~ 7일 미만: 1시간 단위 
> - 7일 이상 ~ 30일: 1일 단위   
>   최대 검색 가능 기간은 한 달(30일) 이며, 10분 단위의 데이터에 대한 통계 데이터는 3개월 동안 보관됩니다. 

통계 데이터는 실시간으로 집계되지 않습니다. 
10분, 1시간 단위의 데이터는 10분마다, 1일 단위는 1시간마다 데이터가 집계됩니다.

1.[API Gateway] > [Dashboard] 를 클릭하여 대시보드 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/console/statistics.png)
<center>[그림52] 통계 대시보드 화면 이동</center>

2.검색 기간 설정하시면 해당 기간 동안의 통계 데이터가 조회됩니다. 
검색 기간은 최대 30일이내의 데이터만 조회 가능합니다. 

![](http://static.toastoven.net/prod_apigateway/console/statistics_search.png)

<center>[그림53] 기간별 통계</center>

Domain Key: API Setting에서 등록한 도메인 고유 키가 표시됩니다.

Success: 성공한 API Call의 Count 합계 
- API Call의 성공 기준은 Response HTTP Status Code가 400미만 일 경우 입니다.

Failures: 실패한 API Call의 Count 합계
- API Call의 실패 기준은 Response HTTP Status Code가 400이상 일 경우 입니다.

Response By APIGW Count: API Gateway 에서 Response가 Client에 전달된 API Call의 Count 합계 입니다. 
- 특정 플러그인은 API Gateway에서 Response를 반환하기도 합니다. 예를들어 IP ACL에서 허용되지 않은 IP 소유자가 요청이 들어온 경우, API Gateway는 403 Forbidden를 반환합니다. 이와 같이 API Gateway의 Response가 Client에게 전달된 API Call의 합계 입니다.  

Total API CAll Count: 전체 API Call Count 합계 
- API Gateway로 인입된 전체 API Call Count 입니다. (Total API Call Count = Success + Failures) 

Avg. response time (ms) : 평균 응답 속도 입니다. 단위는 ms 입니다. 

Sum. network outbound traffic: API Gateway -> Client로 Response 전송량의 합계 입니다. 

3.검색기간을 설정하여 검색기간 내 도메인별 통계 정보를 확인할 수 있습니다.

4.Domain 목록을 클릭하여 Domain의  상세 통계를 확인할 수 있습니다. 

![](http://static.toastoven.net/prod_apigateway/console/statistics_endpoint.png)
<center>[그림54] Domain별 통계</center>



5.상세 통계에서는 성공,실패 API Call count, Average Response Time, Network Outbound Traffic 에 대한 그래프를 확인할 수 있습니다. 

![](http://static.toastoven.net/prod_apigateway/console/statistics_endpoint_success.png)
<center>[그림55] API Call 성공 통계 그래프</center>

![](http://static.toastoven.net/prod_apigateway/console/statistics_endpoint_fail.png)

<center>[그림56] API Call 실패 통계 그래프</center>

![](http://static.toastoven.net/prod_apigateway/console/statistics_endpoint_response_time.png)

<center>[그림57] 평균 응답시간 및 네트워크 트래픽 사용량 통계 그래프</center>

6.Endpoint Path별 상세한 통계 정보를 확인할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/console/statistics_endpoint_detail_table.png)

<center>[그림58] URI Pattern별 통계 정보</center>

>  [참고] CORS 플러그인 이용시 API Call Count 사용량  
> CORS 플러그인을 사용하는 경우 API Call Count가 실제 사용량 보다 크게 나올 수 있습니다.  
> 경우에 따라 CORS 요청은 하나의 요청에 대해 Preflight 요청 (OPTIONS 메서드)과 실제 요청, 총 2건의 요청을 합니다.

