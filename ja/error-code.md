
## Application Service > API Gateway > エラーコード

## 使用量制限(プロジェクト単位) 
プロジェクト単位の使用量制限を超えると、HTTP Status 429 (Too many request)レスポンスが返されます。
呼び出し数は毎秒10,000件に制限されます。

#### エラーコード

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


## 使用量制限(Usage Limit)

使用量制限を超えると、HTTP Status 403 responseが返されます。

#### エラーコード

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

HMAC認証失敗時、HTTP status 401 responseが返されます。

#### エラーコード

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

JWT認証失敗時、HTTP status 401 responseが返されます。

#### エラーコード

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

## 事前呼び出しAPI(Pre-call API)

Pre-call API認証失敗時、HTTP status 502 responseが返されます。

#### エラーコード

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

## URL再作成(Rewrite URL)

URIパターンまたはURL再作成形式を無効な文法で設定すると、HTTP status 500 responseが返されます。

#### エラーコード

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
