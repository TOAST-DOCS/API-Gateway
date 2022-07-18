## Application Service > API Gateway > Error Code

## Ban Request 
- Cause: If backend endpoint service does not respond or its response is delayed for more than 60 seconds to protect the API Gateway service and backend endpoint service, the API Gateway service will temporarily deny the backend endpoint service request. 
- Response HTTP status: 503 Service Unavailable 
- Error response body 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 5030001,
        "resultMessage": "Upstream Service Unavailable (CircuitBreaker {detailErrorMessage})"
    }
}
```

> **[Note] Ban requests**
> - If your request is banned, a ban request error code is returned, and the ban is disabled after a certain period of time.
> - In the event that your request is banned if you link a backend endpoint service with abnormal operating condition or response (timeout) is delayed for more than 60 seconds, it is recommended to not link any APIs.

## HMAC
- Cause: The following response appears when there is no request information required for HMAC authentication or when authentication fails.
- Response HTTP status: 401 Unauthorized 
- Error response body 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4011001,
        "resultMessage": "Authorization is empty."
    }
}
```


| result code | resultMessage             |  Description|
| ---------------- | ----------- | -------------------------- |
| 4011001              | Authorization is empty.      | Authorization request header does not  exist.|
| 4011002              | HmacAlgorithm is empty or not supported algorithm      | Encryption algorithm is not supported or  algorithm is not specified.|
| 4011003              | Signature is empty.      | There is no signature information. |
| 4011004              | Not include some headers credential.      |  Required validation header is not included  in the request header. |
| 4011005              | x-nhn-date header is empty.      | x-nhn-date request header does not exist.|
| 4011006              | Invalid x-nhn-date format. ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)      | Date data format of x-nhn-date is invalid.|
| 4011007              | expired      | The request is expired.|
| 4011008              | Authorization is invalid.      | The authentication information of the  request is invalid.|
| 4011009              | Authorization header must start with the string hmac.      | Invalid because the authorization request  header value does not start with hmac.|

## JWT
- Cause: The following response is returned when there is no request information required for JWT authentication or when authentication fails.
- Response HTTP Status: 401 Unauthorized
- Error Response Body  
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4012001,
        "resultMessage":  "Token is invalid."
    }
}
```

| result code | resultMessage             |  Description|
| ---------------- | ----------- | -------------------------- |
| 4012002          | Authorization is empty.      | Authorization request header does not exist.|
| 4012001          | Token type is invalid.      | Authorization request header’s token type is invalid.|
| 4012001          | Toekn is invalid.      | Authentication failed due to invalid token value.|
| 5012001          | jwks url is unavailable.      | The JWKS URL is not in service.|
| 5012002          | jwks format is invalid.      | The reply of JWKS URL does not match the form of JWKS.|

## Pre-call API
- Cause: Error response is returned when the request for Pre-call API fails.
- Response HTTP Status: 502 Bad Gateway
- Error Response Body
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

- Cause: Returns an error response when denying requests from unauthorized IPs.
- Response HTTP Status: 403 Forbidden
- Error response body 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031007,
        "resultMessage": "Request IP not allowed"
    }
}
```

## Request Size Exceeded
- Cause: Occurs when the request size exceeds 10MB.
- Response HTTP Status: 413 Request Entity Too Large
- Error response body 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4131000,
        "resultMessage": "Request size is larger than permissible limit. the permissible limit is 10mb."
    }
}
```

## Response Size Exceeded
- Cause: Occurs when the response size exceeds 10MB. 
- When the response size exceeds 10MB, the API Gateway server disconnects the client.
- The following items are recorded in the access log.
    - Response HTTP Status: 500 
    - Error code: 500000001
    - Error message: The download size of the response body has been exceeded. the permissible limit is 10mb.

## Request Number Limit
- Cause: Returns an error response when a request exceeding the request number limit is rejected.
- Response HTTP Status: 429 Too Many Requests
- Error Response Body  
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291000,
        "resultMessage": "Too Many Requests"
    }
}
```

## Request Quota Limit
- Cause: Returns an error response when a request exceeding the request quota limit is rejected.
- Response HTTP Status: 429 Too Many Requests
- Error Response Body
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291001,
        "resultMessage": "Usage quota exceeded."
    }
}
```

## Invalid URI error  
- Cause: If the URI configuration of the backend endpoint is incorrect, an error response is returned.  
    - It might occur when the value of the path or query string, which is a part of the URI, is incorrect or the value cannot be encoded.
- Response HTTP Status: 400 Bad Request
- Error Response Body 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000003,
        "resultMessage": "Invalid URI."
    }
}
```

## Could Not Find The Path Or Method
- Cause: Occurs when a request is made with an API path and method not registered in API Resource.
- Response HTTP Status: 404 Not Found
- Error response body 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4041007,
        "resultMessage": "URL Not Found"
    }
}
```

## Backend Endpoint Service Connection Error 
- Cause: Occurs when backend endpoint does not respond or refuses to respond.
- Response HTTP Status: 503 Service Unavailable 
- Error response body 
```
{
  "header" : {
    "resultCode" :  5030001,
    "resultMessage" :  "Upstream Service Unavailable ({error detail message})",
    "isSuccessful" :  false
  }
}
```
- Cause: Occurs when backend endpoint does not respond or refuses to respond.
- Response HTTP Status: 502 Bad Gateway 
- Error response body 
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
- Cause: The following response is sent when the API key information of the request is missing or incorrect.
- Response HTTP Status: 403 Forbidden
- Error Response Body
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031010,
        "resultMessage": "Request api key is empty."
    }
}
```

| result code | resultMessage             |  Description|
| ---------------- | ----------- | -------------------------- |
| 4031010          | Request api key is empty.    | x-nhn-apikey request header does not exist.|
| 4031011          | Request api key is inactive.    | Requested API key is inactive. |
| 4031012          | Request api key is invalid.      | Requested API key is invalid. |
