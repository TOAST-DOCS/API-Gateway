## Application Service > API Gateway > 오류 코드



## Usage Quota 

사용량 제한을 초과하였을 경우 HTTP Status 403 response가 반환 됩니다. 

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```

### HMAC

HMAC 인증 실패시 HTTP status 401 response가 반환됩니다.

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

| http status code | result code | result message                           |
| ---------------- | ----------- | ---------------------------------------- |
| 401              | 20001       | 20001 HMAC authentication failed (The timestamp field is empty) |
| 401              | 20001       | 20001 HMAC authentication failed (Invalid timestamp format) |
| 401              | 20001       | 20001 HMAC authentication failed (Exceeded expiration time) |
| 401              | 20001       | 20001 HMAC authentication failed (The authorization field is empty) |
| 401              | 20001       | 20001 HMAC authentication failed (Invalid authorization) |

## JWT 

JWT 인증 실패시 HTTP status 401 response가 반환됩니다.

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

| http status code | result code | result message                           |
| ---------------- | ----------- | ---------------------------------------- |
| 401              | 20002       | 20002 JWT authentication failed (The authorization field is empty) |
| 401              | 20002       | 20002 JWT authentication failed (Exceeded expiration time) |
| 401              | 20002       | 20002 JWT authentication failed (Invalid authorization) |

## PRE API 

PRE API 인증 실패시 HTTP status 502 response가 반환됩니다.

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

| http status code | result code | result message                  |
| ---------------- | ----------- | ------------------------------- |
| 502              | 20008       | 20008 Pre api connection failed |