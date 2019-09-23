## Application Service > API Gateway > Error Codes

## Capacity Limit (by Project) 
If it exceeds the capacity limit by project,  the response shall return HTTP Status 429 (Too many requests).  
Calls are restricted to 10,000 cases per second. 

#### Error Code

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


## Usage Quota

If it exceeds usage quota, HTTP Status 403 response is returned. 

#### Error Codes 

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

If HMAC authentication fails,  HTTP status 401 response is returned. 

#### Error Codes

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

If JWT authentication fails,  HTTP status 401 response is returned. 

#### Error Codes

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

## Pre-Call API

If pre-call API authentication fails, HTTP status 502 response is returned. 

#### Error Codes 

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

## URL Rewrite

If URL pattern or URL rewrite format is configured in invalid grammar, HTTP status 500 response is returned.

#### Error Codes 

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

