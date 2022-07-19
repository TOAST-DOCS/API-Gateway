
## Application Service > API Gateway > エラーコード

## リクエスト遮断 
- 発生原因：API Gatewayサービスとバックエンドエンドポイントサービスを保護する目的でバックエンドエンドポイントサービスがレスポンスを行わなかったり、レスポンス遅延(60秒以上)が継続的に発生する場合、API Gatewayサービスは該当バックエンドエンドポイントサービスに対するリクエストを一時的に拒否します。 
- レスポンスHTTP状態：503 Service  Unavailable
- エラーレスポンス本文 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 5030001,
        "resultMessage": "Upstream Service Unavailable (CircuitBreaker {detailErrorMessage})"
    }
}
```

> **[参考]リクエスト遮断**
> - リクエストが遮断されるとリクエスト遮断エラーコードが返され、一定時間が経過すると遮断が解除されます。
> - 正常に稼働中の状態ではないバックエンドエンドポイントサービスを連携したり、レスポンス遅延(Timeout)が60秒以上発生する場合、遮断が発生するため、APIは連携しないことを推奨します。

## HMAC
- 発生原因：HMAC認証に必要なリクエスト情報がない場合や、認証に失敗した場合、次のレスポンスが伝達されます。
- レスポンスHTTP状態：401 Unauthorized 
- エラーレスポンス本文 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4011001,
        "resultMessage": "Authorization is empty."
    }
}
```


| result code | resultMessage             | 説明|
| ---------------- | ----------- | -------------------------- |
| 4011001              | Authorization is empty.      | Authorizationリクエストヘッダがありません。|
| 4011002              | HmacAlgorithm is empty or not supported algorithm      | サポートしていない暗号化アルゴリズム、またはアルゴリズムが指定されていません。|
| 4011003              | Signature is empty.      | signature情報がありません。 |
| 4011004              | Not include some headers credential.      | リクエストヘッダに必須検証ヘッダが含まれていません。 |
| 4011005              | x-nhn-date header is empty.      | x-nhn-dateリクエストヘッダがありません。|
| 4011006              | Invalid x-nhn-date format. ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)      | x-nhn-dateの日付データ形式が無効です。|
| 4011007              | expired      | リクエスト有効期限が切れました。|
| 4011008              | Authorization is invalid.      | リクエストの認証情報が有効ではありません。|
| 4011009              | Authorization header must start with the string hmac.      | Authorizationリクエストヘッダ値がhmacで始まっていないため有効ではありません。|


## JWT
- 発生原因：JWT認証に必要なリクエスト情報がない場合や、認証に失敗した場合、次のレスポンスが返されます。
- レスポンスHTTP状態：401 Unauthorized 
- エラーレスポンス本文
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4012001,
        "resultMessage":  "Token is invalid."
    }
}
```

| result code | resultMessage             | 説明|
| ---------------- | ----------- | -------------------------- |
| 4012001          | Authorization is empty.      | Authorizationリクエストヘッダがありません。|
| 4012002          | Token type is invalid.      | Authorizationリクエストヘッダのトークンタイプが有効ではありません。|
| 4012003          | Token is invalid.      | トークン値が有効ではないため、認証に失敗しました。|
| 5012001          | jwks url is unavailable.      | JWKS URLがサービス中ではありません。|
| 5012002          | jwks format is invalid.      | JWKS URLのレスポンスがJWKS形式に一致しません。|

## 事前呼び出しAPI(Pre-call API)
- 発生原因：事前呼び出しAPIのリクエストに失敗すると、エラーレスポンスが返されます。
- レスポンスHTTP状態: 502 Bad Gateway
- エラーレスポンス本文
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

- 発生原因：アクセスが許可されていないIPのリクエストを拒否する時、エラーレスポンスが返されます。
- レスポンスHTTP状態：403 Forbidden
- エラーレスポンス本文 
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031007,
        "resultMessage": "Request IP not allowed"
    }
}
```

## リクエストサイズ超過
- 発生原因：リクエストのサイズが10MB制限を超えた場合に発生します。
- レスポンスHTTP状態：413 Request Entity Too Large
- エラーレスポンス本文 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4131000,
        "resultMessage": "Request size is larger than permissible limit. the permissible limit is 10mb."
    }
}
```

## レスポンスサイズ超過
- 発生原因：レスポンスサイズが10MBを超えた場合に発生します。 
'- レスポンスサイズが超過した場合、API Gatewayサーバーはクライアントとの接続を切ります。
'- アクセスログには次のように記録されます。
    - レスポンスHTTPステータス：500 
    - エラーコード：500000001
    - エラーメッセージ：The download size of the response body has been exceeded. the permissible limit is 10mb.


## リクエスト数制限
- 発生原因：制限されたリクエスト数を超過するリクエストを拒否した時、エラーレスポンスが返されます。
- レスポンスHTTP状態：429 Too Many Requests
- エラーレスポンス本文
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291000,
        "resultMessage": "Too Many Requests"
    }
}
```

## リクエスト割り当て量制限
- 発生原因：制限されたリクエスト割り当て量を超過するリクエストを拒否する時にエラーレスポンスが返されます。
- レスポンスHTTPステータス：429 Too Many Requests
- エラーレスポンス本文
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4291001,
        "resultMessage": "Usage quota exceeded."
    }
}
```

## 無効なURIエラー 
- 発生原因：バックエンドエンドポイントのURI構成が正しくない時、エラーレスポンスが返されます。
    - URIの構成要素であるパスまたはクエリ文字列の値が正しくないか、エンコードできない場合に発生することがあります。
- レスポンスHTTPステータス：400 Bad Request
- エラーレスポンス本文
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4000003,
        "resultMessage": "Invalid URI."
    }
}
```

## パスまたはメソッドが見つからない
- 発生原因：APIリソースに登録されていないAPIパスおよびメソッドでリクエストした場合に発生します。
- レスポンスHTTP状態：404 Not Found
- エラーレスポンス本文 
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4041007,
        "resultMessage": "URL Not Found"
    }
}
```

## バックエンドエンドポイントサービス接続エラー 
- 発生原因：バックエンドエンドポイントが応答しなかったり、応答を拒否した場合に発生します。
- レスポンスHTTP状態：503 Service Unavailable 
- エラーレスポンス本文 
```
{
  "header" : {
    "resultCode" :  5030001,
    "resultMessage" :  "Upstream Service Unavailable ({error detail message})",
    "isSuccessful" :  false
  }
}
```
- 発生原因：バックエンドエンドポイントが応答しなかったり、応答を拒否した場合に発生します。
- レスポンスHTTP：502 Bad Gateway 
- エラーレスポンス本文 
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
- 発生原因：リクエストのAPI Key情報がないか、無効の場合、次のレスポンスが渡されます。
- レスポンスHTTPステータス：403 Forbidden
- エラーレスポンス本文
``` 
{
    "header": {
        "isSuccessful": false,
        "resultCode": 4031010,
        "resultMessage": "Request api key is empty."
    }
}
```

| result code | resultMessage             | 説明|
| ---------------- | ----------- | -------------------------- |
| 4031010          | Request api key is empty.    | x-nhn-apikeyリクエストヘッダがありません。|
| 4031011          | Request api key is inactive.    | リクエストされたAPI Keyが無効になっている状態です。 |
| 4031012          | Request api key is invalid.      | リクエストされたAPI Key値が有効ではありません。|
