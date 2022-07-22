## Application Service > API Gateway > 오류 코드

## 요청 차단 
- 발생 원인: API Gateway 서비스와 백엔드 엔드포인트 서비스를 보호하는 목적으로 백엔드 엔드포인트 서비스가 응답을 하지 않거나 응답 지연(60초 이상)이 지속적으로 발생하는 경우, API Gateway 서비스는 해당 백엔드 엔드포인트 서비스에 대한 요청을 일시적으로 거부합니다. 
- 응답 HTTP 상태: 503 Service  Unavailable 
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 5030001,
        "resultMessage": "Upstream Service Unavailable (CircuitBreaker {detailErrorMessage})"
    }
}
```

> **[참고] 요청 차단**
> - 요청이 차단되면 요청 차단 오류 코드가 응답되며, 일정 시간 이후 차단이 해제됩니다.
> - 정상적인 운영 상태가 아닌 백엔드 엔드 포인트 서비스를 연동하거나 응답 지연(timeout)이 60초 이상 발생된 경우 차단되므로, API는 연동하지 않는 것을 권장합니다.

## HMAC
- 발생 원인: HMAC 인증에 필요한 요청 정보가 없거나 인증에 실패하는 경우 다음의 응답이 전달됩니다.
- 응답 HTTP 상태: 401 Unauthorized 
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4011001,
        "resultMessage": "Authorization is empty."
    }
}
```


| result code | resultMessage             |  설명|
| ---------------- | ----------- | -------------------------- |
| 4011001              | Authorization is empty.      | Authorization 요청 헤더가 없습니다.|
| 4011002              | HmacAlgorithm is empty or not supported algorithm      | 지원하지 않는 암호화 알고리즘 또는 알고리즘이 지정되지 않았습니다.|
| 4011003              | Signature is empty.      | signature 정보가 없습니다. |
| 4011004              | Not include some headers credential.      | 요청 헤더에 필수 검증 헤더가 포함되어 있지 않습니다. |
| 4011005              | x-nhn-date header is empty.      | x-nhn-date 요청 헤더가 없습니다.|
| 4011006              | Invalid x-nhn-date format. ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)      | x-nhn-date의 날짜 데이터 형식이 잘못되었습니다.|
| 4011007              | expired      | 요청 유효시간이 만료되었습니다.|
| 4011008              | Authorization is invalid.      | 요청의 인증 정보가 유효하지 않습니다.|
| 4011009              | Authorization header must start with the string hmac.      | Authorization 요청 헤더값이 hmac으로 시작하지 않아 유효하지 않습니다.|


## JWT
- 발생 원인: JWT 인증에 필요한 요청 정보가 없거나 인증에 실패하는 경우 다음의 응답이 전달됩니다.
- 응답 HTTP 상태: 401 Unauthorized 
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4012001,
        "resultMessage":  "Token is invalid."
    }
}
```

| result code | resultMessage             |  설명|
| ---------------- | ----------- | -------------------------- |
| 4012001          | Authorization is empty.      | Authorization 요청 헤더가 없습니다.|
| 4012002          | Token type is invalid.      | Authorization 요청 헤더의 토큰 타입이 유효하지 않습니다.|
| 4012003          | Token is invalid.      | 토큰값이 유효하지 않아 인증에 실패했습니다.|
| 5012001          | jwks url is unavailable.      | JWKS URL이 서비스 중이지 않습니다.|
| 5012002          | jwks format is invalid.      | JWKS URL의 응답이 JWKS 형식에 맞지 않습니다.|

    
## 사전 호출 API(Pre-call API)
- 발생 원인: 사전 호출 API 요청 실패 시 오류 응답이 반환됩니다.
- 응답 HTTP 상태 : 502 Bad Gateway
- 오류 응답 본문
```
{  
   "header":{  
      "isSuccessful":false,
      "resultCode":5021001,
      "resultMessage":"Pre API Connection Failed"
   }
}
```

## IP ACL

- 발생 원인: 접근이 허가되지 않은 IP의 요청을 거부할 때 오류 응답이 반환됩니다.
- 응답 HTTP 상태: 403 Forbidden
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031007,
        "resultMessage": "Request IP not allowed"
    }
}
```

## 요청 크기 초과 
- 발생 원인: 요청 크기가 10MB를 초과한 경우 발생합니다.
- 응답 HTTP 상태: 413 Request Entity Too Large
- 오류 응답 본문 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4131000,
        "resultMessage": "Request size is larger than permissible limit. the permissible limit is 10mb."
    }
}
```

## 응답 크기 초과
- 발생 원인: 응답 크기가 10MB를 초과한 경우 발생합니다. 
- 응답 크기 초과 시 API Gateway 서버는 클라이언트와의 연결을 끊습니다.
- 액세스 로그에는 다음과 같이 기록됩니다.
    - 응답 HTTP 상태: 500 
    - 오류 코드: 500000001
    - 오류 메시지: The download size of the response body has been exceeded. the permissible limit is 10mb.


## 요청 수 제한
- 발생 원인: 제한된 요청 수를 초과하는 요청을 거부할 때 오류 응답이 반환됩니다.
- 응답 HTTP 상태: 429 Too Many Requests
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291000,
        "resultMessage": "Too Many Requests"
    }
}
```

## 요청 할당량 제한
- 발생 원인: 제한된 요청 할당량을 초과하는 요청을 거부할 때 오류 응답이 반환됩니다.
- 응답 HTTP 상태: 429 Too Many Requests
- 오류 응답 본문
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291001,
        "resultMessage": "Usage quota exceeded."
    }
}
```

## 잘못된 URI 오류 
- 발생 원인: 백엔드 엔드포인트의 URI 구성이 올바르지 않을 때 오류 응답이 반환됩니다. 
    - URI의 구성 요소인 경로 또는 쿼리 문자열의 값이 올바르지 않거나 인코딩할 수 없는 경우 발생할 수 있습니다.
- 응답 HTTP 상태: 400 Bad Request
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000003,
        "resultMessage": "Invalid URI."
    }
}
```

## 경로 또는 메서드를 찾을 수 없음
- 발생 원인: API 리소스에 등록되지 않은 API 경로 및 메서드로 요청한 경우 발생합니다.
- 응답 HTTP 상태: 404 Not Found
- 오류 응답 본문 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4041007,
        "resultMessage": "URL Not Found"
    }
}
```

## 백엔드 엔드포인트 서비스 연결 오류 
- 발생 원인: 백엔드 엔드포인트가 응답하지 않거나 응답을 거부하는 경우 발생합니다.
- 응답 HTTP 상태: 503 Service Unavailable 
- 오류 응답 본문 
```
{
  "header" : {
    "resultCode" :  5030001,
    "resultMessage" :  "Upstream Service Unavailable ({error detail message})",
    "isSuccessful" :  false
  }
}
```
- 발생 원인: 백엔드 엔드포인트가 응답 하지 않거나 응답을 거부하는 경우 발생합니다.
- 응답 HTTP 상태: 502 Bad Gateway 
- 오류 응답 본문 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 5020001,
        "resultMessage": "Upstream Bad Gateway ({error detail message})"
    }
}
```

## API Key 
- 발생 원인: 요청의 API Key 정보가 없거나 잘못된 경우 다음의 응답이 전달됩니다.
- 응답 HTTP 상태: 403 Forbidden
- 오류 응답 본문
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031010,
        "resultMessage": "Request api key is empty."
    }
}
```

| result code | resultMessage             |  설명|
| ---------------- | ----------- | -------------------------- |
| 4031010          | Request api key is empty.    | x-nhn-apikey 요청 헤더가 없습니다.|
| 4031011          | Request api key is inactive.    | 요청된 API Key 가 비활성화 상태입니다. |
| 4031012          | Request api key is invalid.      | 요청된 API Key 값이 유효하지 않습니다.|