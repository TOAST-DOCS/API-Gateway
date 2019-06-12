## Application Service > API Gateway > 오류 코드


## 사용량 제한 (프로젝트 단위) 
프로젝트 단위의 사용량 제한을 초과하면 HTTP Status 429 (Too many request) 응답이 반환됩니다. 
호출량은 초당 10,000건으로 제한됩니다.

#### 오류 코드

```
{
  "header": {
    "resultCode": 200040,
    "resultMessage": "200040 Tenant quota exceeded",
    "isSuccessful": false
  }
}
```

| http status code | result code | result message             |
| ---------------- | ----------- | -------------------------- |
| 429              | 200040      | 200040 Tenant quota exceeded|

## 사용량 제한(Usage Limit)

사용량 제한을 초과하면 HTTP Status 403 response가 반환됩니다. 

#### 오류 코드

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```

| http status code | result code | result message             |
| ---------------- | ----------- | -------------------------- |
| 403              | 20004       | 20004 Usage quota exceeded |

## HMAC

HMAC 인증 실패 시 HTTP status 401 response가 반환됩니다.

#### 오류 코드

```
{
  "header" : {
    "resultCode" :  20001,
    "resultMessage" :  "20001 HMAC authentication failed (Exceeded expiration time)",
    "isSuccessful" :  false
  }
}
```

| http status code | result code | result message                           |
| ---------------- | ----------- | ---------------------------------------- |
| 401              | 20001       | 20001 HMAC authentication failed (The timestamp field is empty) |
| 401              | 20001       | 20001 HMAC authentication failed (Invalid timestamp format) |
| 401              | 20001       | 20001 HMAC authentication failed (Exceeded expiration time) |
| 401              | 20001       | 20001 HMAC authentication failed (The authorization field is empty) |
| 401              | 20001       | 20001 HMAC authentication failed (Invalid authorization) |

## JWT 

JWT 인증 실패 시 HTTP status 401 response가 반환됩니다.

#### 오류 코드

```
{  
   "header":{  
      "resultCode":20002,
      "resultMessage":"20002 JWT authentication failed (Exceeded expiration time)",
      "isSuccessful":false
   }
}
```

| http status code | result code | result message                           |
| ---------------- | ----------- | ---------------------------------------- |
| 401              | 20002       | 20002 JWT authentication failed (The authorization field is empty) |
| 401              | 20002       | 20002 JWT authentication failed (Exceeded expiration time) |
| 401              | 20002       | 20002 JWT authentication failed (Invalid authorization) |

## 사전 호출 API(Pre-call API)

Pre-call API 인증 실패 시 HTTP status 502 response가 반환됩니다.

#### 오류 코드

```
{  
   "header":{  
      "resultCode":20008,
      "resultMessage":"20008 Pre api connection failed",
      "isSuccessful":false
   }
}
```

| http status code | result code | result message                  |
| ---------------- | ----------- | ------------------------------- |
| 502              | 20008       | 20008 Pre api connection failed |

## URL 재작성(Rewrite URL)

URI 패턴 또는 URL 재작성 형식을 잘못된 문법으로 설정하면 HTTP status 500 response가 반환됩니다.

#### 오류 코드

```
{  
   "header":{  
      "resultCode":20005,
      "resultMessage":"20005 URI Pattern's syntax is invalid",
      "isSuccessful":false
   }
}
```

| http status code | result code | result message                  |
| ---------------- | ----------- | ------------------------------- |
| 500              | 20005       | URI Pattern's syntax is invalid |
| 500              | 20006       | Rewrite URI's syntax is invalid |
