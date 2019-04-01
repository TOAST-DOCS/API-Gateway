## Application Service > API Gateway > 오류 코드



## 사용량 제한(Usage Quota)

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

## 사전 호출 API(Pre API)

Pre API 인증 실패 시 HTTP status 502 response가 반환됩니다.

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

## URL 재작성(URL Rewrite)

URI 패턴 또는 URI 재작성 형식을 잘못된 문법으로 설정하면 HTTP status 500 response가 반환됩니다.

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
