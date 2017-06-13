## Upcoming Products > API Gateway > Developer's Guide

> ※ 본 문서는 alpha 개발 단계의 문서입니다.
> 사용에 관심이 있으신 분은 **support@cloud.toast.com**으로 문의해 주시기 바랍니다.

이 문서는 API Gateway의 구조와 기능 및 사용법을 서술합니다.

## 서비스 구조

![[그림1] 서비스 구조](http://static.toastoven.net/prod_apigateway/img_11.png)
<center>[그림1] 서비스 구조</center>

## 기능

#### Domain 관리

하나의 Domain은 대상 서버를 가리키는 Domain URL 하나에 대응됩니다. Domain은 생성, 편집, 삭제가 가능합니다. 그리고 Domain에 대해 플러그인을 설정할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_13.png)
<center>[그림2] Domain 리스트</center>

웹콘솔의 [API Gateway] > [API Setting] 을 클릭하여 Domain 관리 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_14.png)
<center>[그림3] Domain 관리 페이지 이동</center>

#### Endpoint 관리

Endpoint는 API에 접근 가능한 Endpoint를 의미합니다. 그러므로 하나의 Endpoint는 API 한 개에 대응됩니다. Endpoint는 생성, 편집, 삭제가 가능합니다. 그리고 Endpoint에 대해 플러그인을 추가, 편집, 삭제가 가능합니다.

![](http://static.toastoven.net/prod_apigateway/img_15.png)
<center>[그림4] Endpoint 리스트</center>

Domain 목록에서 관리할 Domain의 가장 우측에 있는 [Setting] > [Endpoint]를 클릭하여 Endpoint 관리 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_16.png)
<center>[그림5] Endpoint 관리 페이지 이동</center>

```
URI가 같더라도 HTTP Method가 다르면 다른 Endpoint입니다.
```

#### API 통계

API 통계는 사용자가 등록한 Domain들에서 발생한 API call의 사용량과 평균응답시간을 나타냅니다. Domain 목록 중 하나를 클릭하여 특정 Domain에 대한 통계를 차트와 Endpoint별 통계로 좀 더 자세히 확인할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_17.png)
<center>[그림6] API 통계 페이지</center>

![](http://static.toastoven.net/prod_apigateway/img_18.png)
<center>[그림7] API 통계 > UrlSuffix 별 통계</center>

웹콘솔에서 [API Gateway] > [Dashboard]를 클릭하여 통계 화면으로 접근할 수 있습니다.

![](http://static.toastoven.net/prod_apigateway/img_19.png)
<center>[그림8] API 통계 페이지 이동</center>

### 사용법

#### Domain 생성

1.[New Domain] 버튼을 클릭하여 Domain 생성화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_20.png)
<center>[그림9] Domain 생성</center>

2.Domain 설정 폼을 채우고 [Save] 버튼을 클릭하여 Domain을 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_21.png)
<center>[그림10] Domain 생성 정보 저장 </center>

#### Domain 편집

1.Domain 목록에서 편집할 Domain 우측에 있는 [Setting] > [Domain] 버튼을 클릭하여 Domain 편집 화면으로 이동합니다.

![](http://static.toastoven.net/prod_apigateway/img_22.png)
<center>[그림11] Domain 편집 </center>

2.Domain 설정을 변경하고 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_23.png)
<center>[그림12] Domain 폅집 정보 저장 </center>

#### Domain 삭제

1.Domain 목록에서 삭제할 Domain 우측에 있는 [Setting] > [Delete] 버튼을 클릭하면 Domain 삭제 팝업이 나타납니다.

![](http://static.toastoven.net/prod_apigateway/img_24.png)
<center>[그림13] Domain 삭제</center>

2.삭제할 Domain을 다시 한번 확인하고 Domain 이름을 입력해서 삭제를 합니다.

![](http://static.toastoven.net/prod_apigateway/img_25.png)
<center>[그림14] Domain 삭제 확인</center>

> 주의 : 삭제한 Domain은 복구할 수없습니다. 삭제 시도시 사용자로부터 Domain 이름을 입력 받아서 확인을 합니다.

#### Endpoint 생성

1.Endpoint 목록에서 [New Endpoint] 버튼을 클릭하여 새 Endpoint를 추가합니다.

![](http://static.toastoven.net/prod_apigateway/img_26.png)
<center>[그림15] Endpoint 생성</center>

2.빈 칸을 채우고 우측에 있는 [Save] 버튼을 클릭하여 Endpoint를 생성합니다.

![](http://static.toastoven.net/prod_apigateway/img_27.png)
<center>[그림16] Endpoint 생성 정보 저장</center>

#### Endpoint 편집

1.Endpoint 목록에서 편집할 Endpoint 우측에 있는 [Edit] 버튼을 클릭하여 편집을 시작합니다.

![](http://static.toastoven.net/prod_apigateway/img_28.png)
<center>[그림17] Endpoint 편집</center>

2.설정을 수정하고 우측에 있는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_29.png)
<center>[그림18] Endpoint 편집 정보 저장</center>
#### Endpoint 삭제

1.Endpoint 목록에서 삭제할 Endpoint 우측에 있는 [Delete] 버튼을 클릭하여 삭제합니다.

![](http://static.toastoven.net/prod_apigateway/img_30.png)
<center>[그림19] Endpoint 삭제</center>

#### Endpoint Plugin 추가

1.Plugin을 추가할 Endpoint 우측에 있는 [+] 버튼을 클릭하면 나타나는 Plugin 목록에서 원하는 Plugin을 클릭합니다.

![](http://static.toastoven.net/prod_apigateway/img_31.png)
<center>[그림20] Endpoint Plugin 추가</center>

2.Plugin 설정 폼을 채우고 우측에 있는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_32.png)
<center>[그림21] Endpoint Plugin 생성 저장</center>

#### Endpoint Plugin 편집

1.편집할 Plugin을 클릭하여 편집 화면을 보이게 합니다.

![](http://static.toastoven.net/prod_apigateway/img_33.png)
<center>[그림22] Endpoint Plugin 편집</center>

2.설정을 수정하고 우측에 보이는 [Save] 버튼을 클릭하여 저장합니다.

![](http://static.toastoven.net/prod_apigateway/img_34.png)
<center>[그림23] Endpoint Plugin 편집 저장</center>

#### Endpoint Plugin 삭제

1.삭제할 Plugin을 클릭하여 편집 화면을 보이게 합니다.

![](http://static.toastoven.net/prod_apigateway/img_35.png)
<center>[그림24] Endpoint Plugin 편집</center>

2.우측에 보이는 [Delete] 버튼을 클릭하여 삭제합니다.

![](http://static.toastoven.net/prod_apigateway/img_36.png)
<center>[그림25] Endpoint Plugin 삭제</center>

## 플러그인

### 플러그인 동작 구조
![](http://static.toastoven.net/prod_apigateway/img_12.png)
<center>[그림26] Plugin 동작 구조</center>

Domain에 추가한 플러그인은 Domain에 속한 모든 API에 대해서 동작합니다. 마찬가지로 Endpoint에 추가한 플러그인은 Endpoint에 대해 API call이 수행될 때 동작합니다.

### IP ACL
#### Access Control > IP ACL
IP 기반 Access Control 기능 입니다.
특정 IP를 allow하거나 deny할 수 있습니다.

### Quota Limit
#### Quota Limit > Usage Quota
시간당 API 사용량을 제한할 수 있습니다.

### Maintenance
#### Maintenance > Maintenance Response
정기점검등의 이유로 모든 Endpoint API 호출에 대해서 사용자가 정의한 Response를 반환하도록 설정합니다.

1. [API Gateway > API Setting] 에서 도메인 셋팅을 위한 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_maintenance_1.png)
<center>[그림27] 도메인 셋팅 이동</center>


2. [Plugin Setting > Maintenance] 에서 Maintenance Response 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_maintenance_2.png)
<center>[그림28] Maintenance Response 플러그인 설정</center>

3. Response 정의한 후에 Deploy를 하게되면 모든 Endpoint API 호출에 대해서 정의된 Response가 반환됩니다.


### HMAC
#### Authentification > HMAC
요청 URL과 시간을 메시지로 사용하여 HMAC 인증을 합니다.

1. [API Gateway > API Setting] 에서 도메인 셋팅을 위한 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_hmac_1.png)
<center>[그림29] 도메인 셋팅 이동</center>

2. [Plugin Setting > Authentication] 에서 HMAC 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_hmac_2.png)
<center>[그림30] HMAC 플러그인 설정</center>

> [참고] Clock skew 설정
> APIGW 서버의 시간과 Client에서 보낸 X-TC-Timestamp 사이의 차가 Clock Skew보다 크면 HMAC 인증에 실패하게 됩니다.
> Clock Skew 값은 0~86400(sec)이며, 만약 0이라면 Clock Skew를 무시합니다.

#### Authentification > HMAC > 인증 API 호출

HMAC 인증을 사용하기 위해서 다음 값을 Request Header에 포함하여 요청해야 합니다.

- Authorization : [Method + "\n "+ URL + "\n "+ Timestamp] 를 조합하여 HmacSHA1 알고리즘으로 암호화 한후 Base64로 인코딩 한 값

- X-TC-Timestamp : ISO datetime format (yyyy-MM-dd'T'HH:mm:ssZZ)

| 요청 | StringToSign |
|-|-|
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

#### 에러코드
```
{
  "header" : {
    "resultCode" :  20001,
    "resultMessage" :  "20001 HMAC authentication failed (Exceeded expiration time)",
    "isSuccessful" :  false
  }
}
```

| http status code | result code | result message |
|-|-|-|
| 401 | 20001 | 20001 HMAC authentication failed (The timestamp field is empty) |
| 401 | 20001 | 20001 HMAC authentication failed (Invalid timestamp format) |
| 401 | 20001 | 20001 HMAC authentication failed (Exceeded expiration time) |
| 401 | 20001 | 20001 HMAC authentication failed (The authorization field is empty) |
| 401 | 20001 | 20001 HMAC authentication failed (Invalid authorization) |


### JWT
#### Authorization > JWT (JSON Web Token)
JWT(Json Web Token) 인증을 합니다.

1. [API Gateway > API Setting\] 에서 도메인 셋팅을 위한 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_jwt_1.png)
<center>[그림31] 도메인 셋팅 이동</center>


2. [Plugin Setting > Authentication] 에서 JWT 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_jwt_2.png)
<center>[그림32] JWT 플러그인 설정</center>

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

#### 에러코드

```
{  
   "header":{  
      "resultCode":20002,
      "resultMessage":"20002 JWT authentication failed (Exceeded expiration time)",
      "isSuccessful":false
   }
}
```

| http status code | result code | result message |
|-|-|-|-|
| 401 | 20002 | 20002 JWT authentication failed (The authorization field is empty) |
| 401 | 20002 | 20002 JWT authentication failed (Exceeded expiration time) |
| 401 | 20002 | 20002 JWT authentication failed (Invalid authorization) |

### CORS(Cross-Origin Resource Sharing)
#### CORS
Cross-Site의 방식 내에서의 XMLHttpRequest API 호출이 가능하도록 합니다.

1. [API Gateway > API Setting\] 에서 도메인 셋팅을 위한 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_cors_1.png)
<center>[그림33] 도메인 셋팅 이동</center>


2. [Plugin Setting > CORS] 에서 CORS 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_cors_2.png)
<center>[그림34] CORS 플러그인 설정</center>


- Allowed credentials: Request with Credential 방식을 사용할 수 있는지를 지정합니다.

- Max credentials Age: Preflight Request의 결과가 캐시에 얼마나 오래 남아 있는지를 지정합니다. 초 단위이며 0~86400 사이의 값을 입력할 수 있습니다.

- Allowed origins: 지정된 도메인만 서버의 리소스에 접근할 수 있도록 지정할 수 있습니다. \*로 입력할 경우 모든 도메인에 대해서 허용합니다. (단, \*로 지정할 경우 credentials를 지원하지 않으므로 구체적인 도메인을 지정하셔야 합니다.) 지정된 도메인에서만 허용하도록 할 경우 ,(comma)로 분리하여 입력합니다. 도메인은 URI(scheme, domain, port) 포맷으로 입력해야 합니다.(ex: http://api-gw.toast.com:8080)

- Allowed methods: 지정된 HTTP Method만 서버 리소스의 접근을 허용합니다.

- Allowed headers: 서버의 리소스의 접근을 허용할 HTTP Method를 지정합니다. 여러 Method를 입력할 경우 ,(comma)로 분리하여 입력합니다.

- Exposed headers: 브라우저에서 접근할 수 있는 허용 헤더를 지정합니다. 여러 헤더를 입력할 경우 ,(comma)로 분리하여 입력합니다.

- 자세한 CORS 규약은 https://www.w3.org/TR/cors/ 를 참고 해주세요.

### Mock Response
#### Endpoint > Mock Response
Response Mock 을 반환하도록 합니다.

### Cache
#### Endpoint > Cache
API 결과를 Caching 합니다.

###  Pre API
#### Endpoint > Pre API
Pre API는 Endpoint를 호출하기 전에 호출되며 Pre API의 응답코드에 따라 Endpoint를 호출여부를 결정하는 인증역할을 합니다.

API Gateway를 통해 들어온 요청 헤더를 포함하여 Pre API를 호출하고, Pre API에서는 전달 받은 헤더 내용에 따라 응답코드를 리턴하면 됩니다.

Pre API의 응답코드에 따라 200이면 Endpoint를 호출하고, 응답코드가 200이 아니면 Pre API의 응답결과를 리턴합니다.
만약, Pre API 호출에 실패할 경우 에러를 리턴하게 됩니다.

#### Pre API 설정

1. [API Gateway > Endpoint] 화면으로 이동
![](http://static.toastoven.net/prod_apigateway/img_plugin_preapi_1.png)
<center>[그림35] Endpoint 설정 화면 이동</center>

2. Plugins > Pre API를 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_preapi_2.png)
<center>[그림36] Pre API 플러그인 추가</center>

3. 호출한 Method type과 URL을 입력한 후 저장합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_preapi_3.png)
<center>[그림37] Pre API 플러그인 설정</center>

#### 에러코드

```
{  
   "header":{  
      "resultCode":20008,
      "resultMessage":"20008 Pre api connection failed",
      "isSuccessful":false
   }
}
```

| http status code | result code | result message |
| ---------------- | ----------- | -------------- |
| 502 | 20008 | 20008 Pre api connection failed |

### Modify Headers
#### Endpoint > Modify Headers
요청/응답 헤더의 값을 추가 합니다.
> [참고]
> 설정한 헤더 키가 이미 존재한다면 덮어쓰게 됩니다.

#### Modify Headers 설정

1. [API Gateway > Endpoint] 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_modifyheaders_1.png)
<center>[그림38] Endpoint 설정 화면 이동</center>

2. Plugins > Modify Headers 플러그인을 추가합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_modifyheaders_2.png)
<center>[그림39] Modify Headers 플러그인 추가</center>

3. Plugins > Modify Headers 플러그인 설정 정보를 입력합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_modifyheaders_3.png)
<center>[그림40] Modify Headers 플러그인 설정 정보 입력</center>

- Request Headers는 요청 헤더를 수정할 수 있습니다.

- Response Headers는 응답 헤더를 수정할 수 있습니다.

#### 에러코드
Modify Headers 플러그인은 별도의 에러코드가 없습니다.

### Endpoint Usage Quota
#### Endpoint > Usage Quota
단위 시간동안 API 사용량을 제한할 수 있습니다.

#### Usage Quota 설정

1. [API Gateway > Endpoint] 화면으로 이동합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_usagequota_1.png)
<center>[그림41] Endpoint 설정 화면 이동</center>

2. Plugins > Usage Quota 플러그인을 추가한 후 단위 시간(sec) 동안 최대 호출 가능 횟수를 입력합니다.
![](http://static.toastoven.net/prod_apigateway/img_plugin_usagequota_2.png)
<center>[그림42] Usage Quota 플러그인 추가</center>
