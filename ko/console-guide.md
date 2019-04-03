## Application Service > API Gateway > 콘솔 사용 가이드

## API Gateway 활성화 

API Gateway 서비스를 활성화하려면 콘솔에서 서비스를 추가할 프로젝트를 선택한 후, **서비스 선택**에서 **Application Service > API Gateway**를 클릭합니다. 

## 도메인

API Gateway 기본 화면입니다. 등록된 도메인의 목록이 표시됩니다.

![apigw_01_201812](https://static.toastoven.net/prod_apigateway/apigw_01_201812.png)

### 도메인 생성 

API Gateway의 도메인 주소 생성과 클라이언트의 요청을 포워딩할 엔드포인트 서버 주소를 설정하려면 도메인을 생성해야 합니다.

![apigw_02_201812](https://static.toastoven.net/prod_apigateway/apigw_02_201812.png)

1. **도메인 생성(New Domain)** 목록을 클릭합니다.

2. **도메인 생성(New Domain)** 버튼을 클릭합니다.

3. 도메인을 설정합니다. 
  - 도메인 이름(Domain Name): 도메인의 별칭입니다. 도메인을 구분하는 용도로 사용할 수 있습니다.
  - 도메인 키(Domain Key): 도메인의 고유한 키입니다. 키 값은 API Gateway의 엔드포인트 URL에 사용됩니다.(api-gw.cloud.toast.com/{domainKey})
    - 도메인 키에는 경로(path) 형식의 값은 사용할 수 없습니다(예: /apis/gateway 사용 불가).
  - 엔드포인트 서버 URL: API Gateway가 요청을 전달할 사용자 API 서버의 URL을 입력합니다. 
  - 스킴(Scheme): API Gateway가 제공하는 도메인 URL의 스킴을 선택합니다.
> [참고] 엔드포인트 서버 URL의 URI 구문은 [RFC3986](https://tools.ietf.org/html/rfc3986)을 참고해주세요.

4. **플러그인 설정(Plugin Setting)**에서 플러그인을 추가합니다. 
  - 도메인 단위에 적용한 플러그인은 도메인 하위의 엔드포인트에 공통으로 적용됩니다.

5. **저장(Save)** 버튼을 클릭합니다.

### 도메인 편집

등록된 도메인의 설정을 수정할 수 있습니다. 

![apigw_03_201812](https://static.toastoven.net/prod_apigateway/apigw_03_201812.png)

1. 편집할 도메인의 **설정(Setting)** 버튼을 클릭합니다.

2. **도메인(Domain)** 버튼을 클릭하여 도메인 편집 화면으로 이동합니다.

3. 도메인 설정을 변경하고 **저장(Save)** 버튼을 클릭하여 저장합니다.

### 도메인 삭제

등록된 도메인을 삭제할 수 있습니다.

![apigw_04_201812](https://static.toastoven.net/prod_apigateway/apigw_04_201812.png)

1. **삭제(Delete)** 버튼을 클릭하면 도메인 삭제 대화 상자가 나타납니다.

2. 삭제할 도메인을 다시 한번 확인하고 도메인 키를 입력합니다.

3. **삭제(Delete)** 버튼을 클릭합니다.

> [주의] 도메인 키를 입력해야 삭제할 수 있습니다. 삭제한 도메인은 복구할 수 없습니다.


### 도메인 복제

기존에 생성한 도메인의 설정을 복제하여 새로운 도메인을 만들 수 있습니다. 

![apigw_05_201812](https://static.toastoven.net/prod_apigateway/apigw_05_201812.png)

1. 복제할 도메인의 **설정(Setting)** > **'\_\_\_\_' 으로부터 도메인 복제**(Clone from '\_\_\_\_' domain)을 클릭합니다.

2. 복제하여 새로 생성할 도메인에서 변경이 필요한 정보를 수정합니다.

3. **저장(Save)** 버튼을 클릭합니다.


### Swagger 파일로 가져오기와 내보내기

swagger 파일을 가져와 도메인을 등록하거나 등록된 도메인을 swagger 파일로 내보낼 수 있습니다.

#### Swagger 파일로 가져오기

1. Swagger 명세를 참고하여 swagger 파일을 작성합니다.
  - [Swagger Specification](http://swagger.io/docs/specification/what-is-swagger/)
2. TOAST 클라우드 API Gateway에서 제공하는 플러그인 설정을 추가하려면 x-toastcloud-apigw 확장 설정 정보를 추가합니다.
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

#### Swagger 파일로 내보내기

![apigw_06_201812](https://static.toastoven.net/prod_apigateway/apigw_06_201812.png)

1. 내보낼 도메인의 **설정(Setting) > Swagger 파일로 내보내기(Export swagger)**를 클릭하면 swagger 파일이 다운로드됩니다. 기본 파일 이름은 export.json입니다.
#### 도메인 기본 정보 설정

- swagger: swagger 버전을 입력합니다. 기본 지원 버전은 swagger 2.0입니다.
- info: 기본 정보를 입력합니다.
  - version: 버전을 입력합니다.
  - title: 도메인 이름을 입력합니다.
- host: API Gateway 도메인을 입력합니다.
- basePath: 도메인 키를 입력합니다.
- schemes: 스킴을 입력합니다(http/https 중 하나만 입력).
- paths: 엔드포인트 경로를 입력합니다.

#### 도메인 플러그인 설정

- 도메인 플러그인은 최상위 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
- HTTP_PROXY: 엔드포인트 서버 URL을 입력합니다(* 입력 필수).
- IPACL: 도메인의 접근 제어(Access Control) > IP 접근 제어(IP ACL)플러그인 설정 정보를 입력합니다(액세스 제어 그룹 중 하나만 입력 가능).
- HMAC: 도메인의 인증(Authentication) > HAMC 플러그인 설정 정보를 입력합니다(인증 그룹 중 하나만 입력 가능).
- JWT: 도메인의 인증(Authentication) > JSON Web Token (JWT) 플러그인 설정 정보를 입력합니다(인증 그룹 중 하나만 입력 가능).
- USAGE_QUOTA: 도메인의 사용량 제한(Quota Limit) > 사용량 제한(Usage Quota) 플러그인 설정 정보를 입력합니다(사용량 제한 그룹 중 하나만 입력 가능).
- MAINTENANCE: 도메인의 유지 관리(Maintenance) > 유지 관리 응답(Maintenance Response) 플러그인 설정 정보를 입력합니다(유지 관리 그룹 중 하나만 입력 가능).

#### 엔드포인트 플러그인 설정

- 엔드포인트 플러그인은 각 경로 레벨의 x-cloudtoast-apigw에 설정 정보를 입력합니다.
- MOCK: 사용자 정의 응답(Mock Response) 플러그인 설정 정보를 입력합니다.
- ENDPOINT_USAGE_QUOTA: 사용량 제한(Usage Quota) 플러그인 설정 정보를 입력합니다.
- PRE_API: 사전 호출 API(Pre API) 플러그인 설정 정보를 입력합니다.
- HEADER: 헤더 변조(Modify Header) 플러그인 설정 정보를 입력합니다.
- URI_REWRITE: URL 재작성(URL Rewrite) 플러그인 설정 정보를 입력합니다.

![apigw_07_201812](https://static.toastoven.net/prod_apigateway/apigw_07_201812.png)

1. **Swagger 파일로 도메인 가져오기(Import Domain)** 버튼을 클릭합니다.

2. 가져올 Swagger 파일을 첨부합니다.

3. **가져오기(Import)** 버튼을 클릭하면 Swagger 파일의 설정 정보대로 도메인이 등록됩니다.

## 엔드포인트

### 엔드포인트 생성

엔드포인트는 사용자의 엔드포인트 API 중 API Gateway를 통해 제공할 API를 관리합니다.

![apigw_08_201812](https://static.toastoven.net/prod_apigateway/apigw_08_201812.png)

1. 엔드포인트를 생성할 도메인의 **설정(Setting)** > **엔드포인트(Endpoint)**를 클릭합니다. 

2. **엔드포인트 생성(New Endpoint)** 버튼을 클릭한 후 엔드포인트의 HTTP 메서드와 경로를 설정합니다.

3. 플러그인을 추가하려면 **+** 버튼을 클릭한 후, 추가할 플러그인을 선택하고 값을 입력합니다.

4. **저장(Save)** 버튼을 클릭합니다.

>  [참고] 엔드포인트 경로
>  엔트포인트 경로에 AntPattern 형식으로 입력할 경우, 여러 개의 API와 대응시킬 수 있습니다. 
>
>  [AntPattern 예시]
>
>  - ?: 하나의 문자와 대치	예) /docs/te?t : /docs/test , /docs/text 
>  - \*: 0개 또는 하나 이상의 문자와 대치   예) /docs/*.txt : /docs/example1.txt, /docs/example2.txt
>  - \*\*: 0개 또는 하나 이상의 경로(path)와 대치  예) /docs/** : /docs/apigw/guide, /docs/image/guide
>  - {[a-z]+}: 경로 변수(path variable)에 대치   예) /v1.0/appKeys/{appKey} : /v1.0/appKeys/myAppKey1, /v1.0/appKeys/myAppKey2 


> [참고] 엔드포인트 경로 매핑(endpoint path mapping)
> Request URI는 여러 개의 경로 패턴과 일치할 수 있습니다. 
> API Gateway는 Request URI와 가장 일치하는 경로에 연결합니다.   
>
> [예시]
> 엔드포인트 경로에 아래의 경로가 등록되어 있다고 가정합니다.
>  - 경로1: /docs/apigw/guide
>  - 경로2: /docs/**
>        Request URL이 '/docs/apigw/guide'일 경우, 경로 1,2 모두 일치합니다. 
>        경로1이 경로2에 비해 매칭된 패턴이 많기 때문에 URI 경로1로 연결됩니다.
>        매칭된 패턴이 문자인 경우 AntPattern 표현식보다 우선순위가 높습니다.

### 엔드포인트 편집

등록된 엔드포인트의 설정을 편집할 수 있습니다.

![apigw_09_201812](https://static.toastoven.net/prod_apigateway/apigw_09_201812.png)

1. 엔드포인트 목록에서 편집할 엔드포인트 오른쪽에 있는 **수정(Edit)** 버튼을 클릭합니다.

2. 설정을 수정하고 오른쪽에 있는 **저장(Save)** 버튼을 클릭하여 저장합니다.

### 엔드포인트 삭제

등록된 엔드포인트를 삭제할 수 있습니다.

![apigw_10_201812](https://static.toastoven.net/prod_apigateway/apigw_10_201812.png)

1. 엔드포인트 목록에서 삭제할 엔드포인트 오른쪽에 있는 **삭제(Delete)** 버튼을 클릭합니다.

2. **확인(OK)** 버튼을 클릭합니다.

### 엔드포인트 플러그인 편집

엔드포인트의 플러그인 설정을 편집할 수 있습니다.

![apigw_11_201812](https://static.toastoven.net/prod_apigateway/apigw_11_201812.png)

1. 편집할 플러그인을 클릭합니다.

2. 설정을 수정하고  **저장(Save)** 버튼을 클릭합니다.


### 엔드포인트 플러그인 삭제

등록된 엔드포인트의 플러그인을 삭제할 수 있습니다.

![apigw_12_201812](https://static.toastoven.net/prod_apigateway/apigw_12_201812.png)

1. 삭제할 플러그인을 클릭합니다.

2. **삭제(Delete)** 버튼을 클릭합니다.

3. **확인(OK)** 버튼을 클릭합니다.

## 플러그인 

### 플러그인 동작 구조

API Gateway는 접근 제어, 인증, 사용량 제한, 메시지 변조 등의 다양한 플러그인을 제공합니다.

플러그인은 도메인과 엔드포인트에 적용할 수 있습니다. 도메인 계층에 추가한 플러그인은 해당 도메인의 하위 엔드포인트에 공통으로 적용됩니다.

엔드포인트 계층에 추가한 플러그인 해당 엔드포인트에만 적용됩니다. 

![](http://static.toastoven.net/prod_apigateway/img_12.png)

API Gateway가 요청을 전달받으면 설정된 플러그인의 속성 그룹 순서대로 플러그인이 동작됩니다.

- Access Control filter에서 제한된 사용자의 요청, 사용 제한 초과 시 요청을 거부합니다. 
- Authentification filter에서 인증되지 않은 요청, 변조된 요청에 대해 요청을 거부합니다. 
- Custom filter에서 요청/응답에 대한 메시지 변조, 모의(mock) 응답을 처리합니다. 
- Proxy filter에서 사용자의 API 서버로 요청을 포워딩하고 응답 값을 전달받아 요청자에게 전달합니다. 

## 도메인 플러그인 

### IP 접근 제어(IP ACL)

IP 기반 접근 제한 기능으로 특정 IP를 허용하거나 거부할 수 있습니다.

![apigw_13_201812](https://static.toastoven.net/prod_apigateway/apigw_13_201812.png)

1. **플러그인 설정(Plugin Setting) > 접근 제어(Access Control)** 플러그인을 클릭한 후  **IP 접근 제어(IP ACL)**을 선택합니다. 

2. 허용(Permit)을 통해 설정된 IP 목록에 대해 허용할 것인지 거부할 것인지 설정합니다. 
  * true로 설정하면 화이트리스트로 동작합니다(설정된 IP만 허용, 그 외 모든 IP는 거부).
  * false로 설정하면 블랙리스트로 동작합니다(설정된 IP만 거부, 그 외 모든 IP는 허용).

3. IPv4 형식의 IP를 입력한 후 **추가(Add)** 버튼을 클릭하여 IP 목록에 추가합니다. 

4. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다. 


### 사용량 제한(Quota Limit)

일정 시간 API 사용량을 제한할 수 있습니다.

![apigw_14_201812](https://static.toastoven.net/prod_apigateway/apigw_14_201812.png)

1. **플러그인 설정(Plugin Setting) > 사용량 제한(Quota Limit)** 플러그인을 클릭한 후 **사용량 제한(Usage Quota)**을 선택합니다. 

2. 사용량 제한 조건을 설정합니다. 
  * 최대 사용 한도(Max Usage Quota)에 최대 API 호출 가능 횟수를 지정합니다. 
  * 시간(Per(sec))에 초 단위의 시간을 지정합니다. 
  * 지정한 시간에 최대 호출 횟수를 초과할 경우 API 사용이 제한됩니다. 
  * 사용량 제한 조건을 여러 개 추가할 수 있으며, 설정된 제한 조건 중 하나 이상의 조건이 제한량을 초과하면 사용이 제한됩니다. 

> [참고]
> 도메인 설정 페이지에서 설정한 **사용 한도(Usage Quota)** 플러그인은 도메인 하위 모든 엔드포인트의 API 사용량에 대한 제한입니다.  
> 엔드포인트별로 사용량 제한이 필요하면 엔드포인트의 **엔드포인트 사용 한도(EndPoint Usage Quota)** 플러그인을 적용해주세요.  

3. 설정을 저장하려면 **저장(Save)** 버튼을 클릭합니다. 

### 유지 관리(Maintenance)

정기 점검 등의 이유로 모든 엔드포인트 API 호출에 사용자가 정의한 응답(response)를 반환하도록 설정하려면 **유지 관리(Maintenance)** 플러그인을 사용할 수 있습니다.

![apigw_15_201812](https://static.toastoven.net/prod_apigateway/apigw_15_201812.png)

1. **플러그인 설정(Plugin Setting) > 유지 관리 설정(Maintenance)** 플러그인을 클릭한 후 **유지 관리 설정(Maintenance Response)**을 선택합니다.

2. 유지 관리(Maintenance) 응답 값을 입력합니다.

3. 설정을 저장하려면 **저장(Save)** 버튼을 클릭합니다.

배포 후 엔드포인트 API 호출에 유지 관리(Maintenance) 플러그인에 설정된 응답이 반환됩니다.

### 인증(Authentication)

API Gateway 인증 방식은 HMAC과 JWT(JSON Web Token) 방식이 있습니다.

#### HMAC

요청 URL과 시간을 메시지로 사용해 HMAC 인증을 합니다.

![apigw_16_201812](https://static.toastoven.net/prod_apigateway/apigw_16_201812.png)

1. **플러그인 설정(Plugin Setting) > 인증(Authentication)** 플러그인 클릭 후 **HMAC**을 선택합니다.

2. HMAC 비밀 키(secret key)와 클록 스큐(clock skew) 값을 설정합니다.
> [주의] 클록 스큐(clock skew) 설정  
> API Gateway 서버 시간과 클라이언트에서 보낸 X-TC-Timestamp 사이의 차가 클록 스큐(clock skew)보다 크면 HMAC 인증에 실패합니다.  
> 클록 스큐(clock skew) 값으로 설정 가능한 범위는 0~86400(sec)이며, 만약 0이라면 클록 스큐(clock skew)를 무시합니다.

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.

##### 인증(Authentication) > HMAC > 인증 API 호출

HMAC 인증을 사용하려면 다음 값을 Request Header에 포함하여 요청해야 합니다.

- Authorization : [Method + "\n "+ URL + "\n "+ Timestamp]를 조합하여 HmacSHA1 알고리즘으로 암호화한 후 Base64로 인코딩 한 값

- X-TC-Timestamp : ISO datetime format (yyyy-MM-dd'T'HH:mm:ssZZ)

| 요청                                       | StringToSign                             |
| ---------------------------------------- | ---------------------------------------- |
| GET /test/1?query1=1&query2=2<br>X-TC-Timestamp: 2016-07-23T12:20:02+09:00<br><span style="color:red">Authorization: IqY8u/RZY8IMESwa/TPW9P9Z39Y=</span> | GET\n<br>/test/1?query1=1&query2=2\n<br>2016-07-23T12:20:02+09:00 |

> [참고] 요청 시간은 ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)을 따릅니다.

##### 권한(Authorization) 생성 코드(Java)
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

#### JWT(JSON Web Token)

JWT(Json Web Token) 인증을 합니다.

![apigw_17_201812](https://static.toastoven.net/prod_apigateway/apigw_17_201812.png)

1. **플러그인 설정(Plugin Setting) > 인증(Authentication)** 플러그인 클릭 후 **JWT**를 선택합니다.

2. JWT Secret Key와 클록 스큐(clock skew) 값, 그리고 발급자(issuer)를 설정합니다.

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.

> [참고]
> API Gateway 서버의 시간과 클라이언트에서 보낸 만료 시간의 차가 클록 스큐(clock skew)보다 크면 JWT인증에 실패합니다.  
> 클록 스큐(clock skew)에는 0~86400 사이의 값을 입력할 수 있습니다.  

##### 인증(Authorization) > JWT (JSON Web Token) > JWT 인증 API 호출

JWT 인증을 사용하려면 다음 값을 Request Header에 포함해 요청해야 합니다.

- Authorization : Json Web Token

Request: GET /test/1?query1=1&query2=2<br>
 <span style="color:red">Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJpbnZhbGl...</span>

##### 권한(Authorization) 생성 코드(Java)

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

### CORS(Cross-Origin Resource Sharing)

Cross-Site 방식 내에서 XMLHttpRequest API 호출을 할 수 있게 합니다.

![apigw_18_201812](https://static.toastoven.net/prod_apigateway/apigw_18_201812.png)

1. **플러그인 설정(Plugin Setting) > CORS** 플러그인 클릭후 **CORS**를 선택합니다.

2. CORS 설정값을 입력합니다.

  - Access-Control-Allow-Credentials: 자격 증명으로 요청하는 경우 True로 설정해야 합니다.

  - Access-Control-Max-Age: 사전 전달 요청(Preflight)에 대한 응답을 얼마 동안 캐시할지 초 단위로 입력합니다. 0~86400 사이의 값을 입력할 수 있습니다.
  - Access-Control-Allow-Origin: 리소스에 액세스할 수 있는 원본/도메인을 입력합니다.
      - *로 입력하면 모든 도메인을 허용합니다.(단, \*로 지정할 경우 자격증명을 지원하지 않으므로 허용 원본(allowed origin)에 구체적인 도메인을 지정하셔야 합니다.) 
      - 지정된 도메인에서만 허용할 때는 ,(쉼표)로 구분해 입력합니다. 
      - 도메인은 URI(스킴, 도메인, 포트) 형식으로 입력해야 합니다(예: http://api-gw.toast.com:8080).
  - Access-Control-Allow-Methods: 리소스 접근에 허용할 메서드를 설정합니다. 여러 메서드를 지정할 경우 ','로 구분해 입력합니다.
  - Access-Control-Allow-Headers: 요청에서 사용할 수 있는 HTTP 헤더를 설정합니다. 여러 헤더를 설정할 경우 ','로 구분해 입력합니다.
  - Access-Control-Expose-Headers: 브라우저(클라이언트)가 접근할 수 있는 헤더를 설정합니다. 여러 헤더를 설정할 경우 ','로 구분해 입력합니다.
  - 자세한 CORS 규약은 https://www.w3.org/TR/cors/를 참고해 주세요.

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.


## 엔드포인트 플러그인 

### 사용자 정의 응답(Mock Response)

사용자가 미리 설정한 사용자 정의 응답을 반환합니다.
엔드포인트 경로에 해당하는 요청 URI(request URI)가 요청되면, 지정된 엔드포인트 서버로 요청을 포워딩하지 않고 사용자가 설정한 사용자 정의 응답이 반환됩니다. 

![apigw_21_201812](https://static.toastoven.net/prod_apigateway/apigw_21_201812.png)

1. **플러그인(Plugins) > 사용자 정의 응답(Mock Response)** 플러그인을 추가합니다.

2. 사용자 정의 응답(mock response) HTTP STATUS, Header, Body를 설정한 후 저장합니다.
  - HTTP Status: 응답의 상태 코드를 설정합니다.
  - Headers: 응답 헤더(response header)에 추가할 헤더와 헤더 값을 설정합니다.
  - Body: 응답 본문(response body) 내용을 설정합니다. 

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.

### 사전 호출 API(Pre API)

사전 호출 API(Pre API)는 엔드포인트를 호출하기 전에 호출되며 Pre API의 응답 코드에 따라 엔드포인트 호출 여부를 결정하는 인증 역할을 합니다.

API Gateway를 통해 들어온 요청 헤더를 포함하여 사전 호출 API(Pre API)를 호출하고, 사전 호출 API(Pre API)에서는 전달받은 헤더 내용에 따라 응답 코드를 반환합니다.

사전 호출 API(Pre API)의 응답 코드에 따라 200이면 엔드포인트를 호출하고, 응답 코드가 200이 아니면 사전 호출 API(Pre API)의 응답 결과를 반환합니다.
만약, 사전 호출 API(Pre API) 호출에 실패하면 오류를 반환합니다.

> [참고]  
> API Gateway는 요청의 헤더 정보만 사전 호출 API(Pre API)의 URL로 전달합니다.   
> Request URL 또는 Body 정보는 전달하지 않습니다.  

![apigw_22_201812](https://static.toastoven.net/prod_apigateway/apigw_22_201812.png)

1. **플러그인(plugins) > 사전 호출 API(Pre API)** 플러그인을 추가합니다.

2. 사전 API의 메서드 타입(method type)과 URL을 입력합니다.

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.


### 헤더 변조(Modify Headers)

헤더 변조(Modify Headers) 플러그인은 엔드 포인트 서버로 요청을 포워딩 할 때 헤더 값을 변조하거나, API Gateway가 클라이언트에 전달할 응답의 헤더를 변조할 수 있습니다.
![apigw_23_201812](https://static.toastoven.net/prod_apigateway/apigw_23_201812.png)

1. **플러그인(Plugins) > 헤더 변조(Modify Headers)** 플러그인을 추가합니다.

2. 설정 정보를 입력합니다.
  - Request Headers는 요청 헤더를 수정합니다.
  - Response Headers는 응답 헤더를 수정합니다.

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.

> [참고]
> 설정한 헤더 키가 이미 존재한다면 덮어쓰게 됩니다.



### 사용량 제한(Usage Quota)

일정 시간 경로별 API 사용량을 제한할 수 있습니다.

![apigw_24_201812](https://static.toastoven.net/prod_apigateway/apigw_24_201812.png)
​	

1. **플러그인(Plugins) > 사용량 제한(Usage Quota)** 플러그인을 추가합니다.

2. 설정한 시간(sec) 동안 최대 호출 가능 횟수를 입력합니다.
  - 사용량 제한 조건을 여러 개 추가할 수 있으며, 설정된 제한 조건 중 하나 이상의 조건이 제한량을 초과하면 사용이 제한됩니다. 

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.


> [주의]  
> '엔드포인트 사용량 제한'은 엔드포인트 경로별 사용량 제한입니다.    
> 도메인 사용량 제한이 필요한 경우 도메인 설정 페이지의 사용량 제한(Usage Quota)을 설정하세요.    
> 도메인과 엔드포인트에 각각 사용량 제한(Usage Quota) 플러그인을 설정한 경우 각각 사용 제한이 적용됩니다.   
> 도메인 사용량 초과 시 엔드포인트의 사용량이 초과되지 않아도 요청이 거부되며, 엔드포인트의 사용량 또한 증가됩니다.     

사용량 제한을 초과하면 아래의 HTTP STATUS 403 응답이 반환됩니다. 

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```

### URL 재작성(URL Rewrite)

Request URL을 패턴 표현식으로 재작성하는 플러그인입니다. 

![apigw_25_201812](https://static.toastoven.net/prod_apigateway/apigw_25_201812.png)

1. **플러그인(Plugins) > URL 재작성(URL Rewrite)** 플러그인을 추가합니다.

2. 설정 정보를 입력합니다.
  - URI 패턴에는 어떤 패턴 형식의 Request URL에 대해 재작성할 것인지 패턴 형식을 입력합니다. 
  - URI 재작성에는 (2)에서 작성한 URI 패턴 형식에 대해 URL을 재작성할 형식을 입력합니다. 

3. 설정 완료 후 **저장(Save)** 버튼을 클릭합니다.

#### [예시] /api/v2.0/\*\* -> /api/v1.0/\*\* 로 재작성하는 경우 

- URI 패턴: /api/v2.0/(.\*)
- URI 재작성: /api/v1.0/%1

위의 규칙을 적용하면 Request URL `/api/v2.0/members`가 ` /api/v1.0/members`로 변경되어 요청됩니다. 


## API 배포 

### API 배포

![apigw_26_201812](https://static.toastoven.net/prod_apigateway/apigw_26_201812.png)

1. 배포할 도메인의 **배포(Deploy)** 버튼을 클릭합니다. 

2. 배포한 API가 정상적으로 호출되는지 테스트합니다.
  도메인 URL에 등록한 엔드포인트 URL을 호출했을 때 기대한 응답(response)이 전달되는지 확인합니다. 

```bash
$ curl -s http://api-gw.cloud.toast.com/apigw/hello
hello world
```

## 통계 

### 통계 조회 

API 통계에서는 각 도메인별 API 호출 평균 응답 시간, 네트워크 트래픽 사용량을 확인할 수 있습니다. 배포(deploy)된 도메인의 통계 데이터만 출력됩니다.

도메인 목록의 도메인을 클릭하면 해당 도메인의 통계를 차트와 URI 패턴별로 자세히 확인할 수 있습니다. 
차트는 검색 기간에 따라 10분, 1시간, 1일 단위로 확인할 수 있습니다.

통계 데이터는 실시간으로 집계되지 않습니다. 
10분, 1시간 단위의 데이터는 10분마다, 1일 단위는 1시간마다 집계됩니다.

- 6시간 미만: 10분 단위 
- 6시간 이상~7일 미만: 1시간 단위 
- 7일 이상~30일: 1일 단위   
최대 검색 가능 기간은 30일이며, 10분 단위의 데이터에 대한 통계 데이터는 3개월 동안 보관됩니다. 

![apigw_27_201812](https://static.toastoven.net/prod_apigateway/apigw_27_201812.png)

1. **API Gateway > 대시보드(Dashboard)**를 클릭해 대시보드 화면으로 이동합니다.

2. 검색 기간을 설정하면 해당 기간 동안의 통계 데이터를 확인할 수 있습니다. 
  검색 기간은 최대 30일 이내입니다.

- 도메인 키: API 설정에서 등록한 도메인 고유 키
- API 호출 성공 수: 성공한 API 호출 수의 합계 
  - API 호출의 성공 기준은 Response HTTP Status Code가 400미만인 경우
- API 호출 실패 수: 실패한 API 호출의 수의 합계
  - API 호출의 실패 기준은 Response HTTP Status Code가 400이상인 경우
- API Gateway에서 바로 응답된 수: 엔드포인트 서버로 요청을 포워딩하지 않고 API Gateway에서 응답이 전달된 경우
  - 특정 플러그인은 API Gateway에서 응답을 반환하기도 합니다. 예를 들어 IP ACL에서 허용되지 않은 IP 소유자가 요청이 들어온 경우, API Gateway는 403 Forbidden를 반환합니다. 이와 같이 API Gateway의 Response가 클라이언트에게 전달된 API 호출의 합계입니다.  
- API 호출 수: 전체 API 호출 수 합계 
  - API Gateway로 인입된 전체 API 호출 수(Total API CALL Count = Success + Failures). 
- 평균 응답 시간(ms): 평균 응답 속도 
- 네트워크 아웃바운드 트래픽(bytes): API Gateway에서 클라이언트로 전송된 응답량의 합계 

3. 검색 기간을 설정해 검색 기간 내 도메인별 통계 정보를 확인할 수 있습니다.

4. 도메인 목록을 클릭해 도메인의 상세 통계를 확인할 수 있습니다. 

![apigw_28_201812](https://static.toastoven.net/prod_apigateway/apigw_28_201812.png)

상세 통계에서는 성공, 실패 API 호출 수, 평균 응답 시간, 네트워크 아웃바운드 트래픽의 그래프를 확인할 수 있습니다. 

아래 표에서 엔드포인트 경로별 상세한 통계를 확인할 수 있습니다.

>  [참고] CORS 플러그인 이용시 API 호출 수 사용량  
>  CORS 플러그인을 사용하는 경우 API 호출 수가 실제 사용량보다 크게 나올 수 있습니다.  
>  경우에 따라 CORS 요청은 하나의 요청에 대해 사전 전달(preflight) 요청 (OPTIONS 메서드)과 실제 요청, 총 2건을 요청합니다.
