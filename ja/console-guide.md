
## Application Service > API Gateway > コンソール使用ガイド

## API Gatewayの有効化 

API Gatewayサービスを有効にするには、コンソールでサービスを追加するプロジェクトを選択し、**サービス選択**で**Application Service > API Gateway**をクリックします。 

## ドメイン

API Gateway基本画面です。登録されているドメインのリストが表示されます。

![apigw_01_201812](https://static.toastoven.net/prod_apigateway/apigw_01_201812.png)

### ドメインの作成 

API Gatewayのドメインアドレス作成とクライアントのリクエストをフォワーディングするエンドポイントサーバーアドレスを設定するには、ドメインを作成する必要があります。

![apigw_02_201812](https://static.toastoven.net/prod_apigateway/apigw_02_201812.png)

1. **ドメイン作成(New Domain)**リストをクリックします。

2. **ドメイン作成(New Domain)**ボタンをクリックします。

3. ドメインを設定します。 
  - ドメイン名(Domain Name)：ドメインのエイリアスです。ドメインを区分する用途で使用できます。
  - ドメインキー(Domain Key)：ドメインの固有キーです。キー値はAPI GatewayのエンドポイントURLに使用されます。(api-gw.cloud.toast.com/{domainKey})
    - ドメインキーにはパス(path)形式の値は使用できません(例：/apis/gateway使用不可)。
  - エンドポイントサーバーURL：API Gatewayがリクエストを渡すユーザーAPIサーバーのURLを入力します。 
  - スキーム(Scheme)：API Gatewayが提供するドメインURLのスキームを選択します。
> [参考]エンドポイントサーバーURLのURI構文は、[RFC3986](https://tools.ietf.org/html/rfc3986)を参照してください。

4. **プラグイン設定(Plugin Setting)**でプラグインを追加します。 
  - ドメイン単位に適用したプラグインは、ドメイン下位のエンドポイントに共通に適用されます。

5. **保存(Save)**ボタンをクリックします。

### ドメインの編集

登録されたドメインの設定を修正できます。 

![apigw_03_201812](https://static.toastoven.net/prod_apigateway/apigw_03_201812.png)

1. 編集するドメインの**設定(Setting)**ボタンをクリックします。

2. **ドメイン(Domain)**ボタンをクリックし、ドメイン編集画面に移動します。

3. ドメイン設定を変更し、**保存(Save)**ボタンをクリックして保存します。

### ドメインの削除

登録されたドメインを削除できます。

![apigw_04_201812](https://static.toastoven.net/prod_apigateway/apigw_04_201812.png)

1. **削除(Delete)**ボタンをクリックすると、ドメイン削除ダイアログボックスが表示されます。

2. 削除するドメインをもう一度確認し、ドメインキーを入力します。

3. **削除(Delete)**ボタンをクリックします。

> [注意]ドメインキーを入力すると削除できます。削除したドメインは復旧できません。


### ドメインの複製

既に作成したドメイン設定を複製し、新しいドメインを作成できます。

![apigw_05_201812](https://static.toastoven.net/prod_apigateway/apigw_05_201812.png)

1. 複製するドメインの**設定(Setting) \> '___'から、ドメインの複製(Clone from '___' domain)**をクリックします。

2. 複製し、新たに作成するドメインで変更が必要な情報を修正します。

3. **保存(Save)**ボタンをクリックします。


### Swaggerファイルのインポート、エクスポート

swaggerファイルをインポートしてドメインを登録できます。また、登録されたドメインをswaggerファイルにエクスポートできます。

#### Swaggerファイルのインポート

1. Swaggerの仕様を確認し、swaggerファイルを作成します。
  - [Swagger Specification](http://swagger.io/docs/specification/what-is-swagger/)
2. TOASTクラウドAPI Gatewayで提供するプラグイン設定を追加するには、x-toastcloud-apigw拡張設定情報を追加します。
  - 例)
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

#### Swaggerファイルにエクスポート

![apigw_06_201812](https://static.toastoven.net/prod_apigateway/apigw_06_201812.png)

1. エクスポートするドメインの**設定(Setting) > Swaggerファイルにエクスポート(Export swagger)**をクリックすると、swaggerファイルがダウンロードされます。基本ファイル名はexport.jsonです。
#### ドメイン基本情報設定

- swagger：swaggerバージョンを入力します。基本サポートバージョンはswagger 2.0です。
- info：基本情報を入力します。
  - version：バージョンを入力します。
  - title：ドメイン名を入力します。
- host：API Gatewayドメインを入力します。
- basePath：ドメインキーを入力します。
- schemes：スキームを入力します(http/httpsのどちらかを入力)。
- paths：エンドポイントパスを入力します。

#### ドメインプラグイン設定

- ドメインプラグインは、最上位レベルのx-cloudtoast-apigwに設定情報を入力します。
- HTTP_PROXY：エンドポイントサーバーURLを入力します(* 入力必須)。
- IPACL：ドメインのアクセス制御(Access Control) > IPアクセス制御(IP ACL)プラグイン設定情報を入力します(アクセス制御グループの中から1つのみ入力可能)。
- HMAC：ドメインの認証(Authentication) > HAMCプラグイン設定情報を入力します(認証グループの中から1つのみ入力可能)。
- JWT：ドメインの認証(Authentication) > JSON Web Token (JWT)プラグイン設定情報を入力します(認証グループの中から1つのみ入力可能)。
- USAGE_QUOTA：ドメインの使用量制限(Quota Limit) > 使用量制限(Usage Quota)プラグイン設定情報を入力します(使用量制限グループの中から1つのみ入力可能)。
- MAINTENANCE：ドメインのメンテナンス(Maintenance) > メンテナンスレスポンス(Maintenance Response)プラグイン設定情報を入力します(メンテナンスグループの中から1つのみ入力可能)。

#### エンドポイントプラグイン設定

- エンドポイントプラグインは、各パスレベルのx-cloudtoast-apigwに設定情報を入力します。
- MOCK：ユーザー定義レスポンス(Mock Response)プラグイン設定情報を入力します。
- ENDPOINT_USAGE_QUOTA：使用量制限(Usage Quota)プラグイン設定情報を入力します。
- PRE_API：事前呼び出しAPI(Pre API)プラグイン設定情報を入力します。
- HEADER：ヘッダ修正(Modify Header)プラグイン設定情報を入力します。
- URI_REWRITE：URLの再作成(URL Rewrite)プラグイン設定情報を入力します。

![apigw_07_201812](https://static.toastoven.net/prod_apigateway/apigw_07_201812.png)

1. **Swaggerファイルでドメインのインポート(Import Domain)**ボタンをクリックします。

2. インポートするSwaggerファイルを添付します。

3. **インポート(Import)**ボタンをクリックすると、Swaggerファイルの設定情報通りにドメインが登録されます。

## エンドポイント

### エンドポイントの作成

エンドポイントは、ユーザーのエンドポイントAPIのうち、API Gatewayを通して提供するAPIを管理します。

![apigw_08_201812](https://static.toastoven.net/prod_apigateway/apigw_08_201812.png)

1. エンドポイントを作成するドメインの**設定(Setting)**>**エンドポイント(Endpoint)**をクリックします。 

2. **エンドポイント作成(New Endpoint)**ボタンをクリックし、エンドポイントのHTTPメソッドとパスを設定します。

3. プラグインを追加するには、**+**ボタンをクリックし、追加するプラグインを選択して値を入力します。

4. **保存(Save)**ボタンをクリックします。

>  [参考]エンドポイントのパス
> エンドポイントのパスにAntPattern形式で入力する場合、複数のAPIと対応させることができます。
>
>  [AntPatternの例]
>
>  - ?：1つの文字とマッチ。	例) /docs/te?t ： /docs/test, /docs/text 
>  - \*：0個以上の文字とマッチ。例) /docs/*.txt ： /docs/example1.txt, /docs/example2.txt
>  - \*\*：0個以上のパス(path)とマッチ。例) /docs/**： /docs/apigw/guide, /docs/image/guide
>  - {[a-z]+}：パス変数(path variable)にマッチ。例) /v1.0/appKeys/{appKey} ： /v1.0/appKeys/myAppKey1, /v1.0/appKeys/myAppKey2 


> [参考]エンドポイントパスのマッピング(endpoint path mapping)
> Request URIは複数のパスのパターンと一致することがあります。
> API Gatewayは、Request URIと最も一致するパスに接続します。   
>
> [例]
> エンドポイントパスに下記のパスが登録されていると仮定します。
>  - パス：/docs/apigw/guide
>  - パス2：/docs/**
>        Request URLが'/docs/apigw/guide'の場合、パス1、2はすべて一致します。 
>     パス1がパス2に比べてマッチするパターンが多いため、URIパス1に接続されます。
>       マッチしたパターンが文字の場合、AntPattern表現式より優先順位が高いです。

### エンドポイントの編集

登録されたエンドポイントの設定を編集できます。

![apigw_09_201812](https://static.toastoven.net/prod_apigateway/apigw_09_201812.png)

1. エンドポイントリストから、編集するエンドポイントの右にある**修正(Edit)**ボタンをクリックします。

2. 設定を修正し、右にある**保存(Save)**ボタンをクリックして保存します。

### エンドポイントの削除

登録されたエンドポイントを削除できます。

![apigw_10_201812](https://static.toastoven.net/prod_apigateway/apigw_10_201812.png)

1. エンドポイントリストから、削除するエンドポイントの右にある**削除(Delete)**ボタンをクリックします。

2. **確認(OK)**ボタンをクリックします。

### エンドポイントプラグインの編集

エンドポイントのプラグイン設定を編集できます。

![apigw_11_201812](https://static.toastoven.net/prod_apigateway/apigw_11_201812.png)

1. 編集するプラグインをクリックします。

2. 設定を修正し、**保存(Save)**ボタンをクリックします。


### エンドポイントプラグインの削除

登録されたエンドポイントのプラグインを削除できます。

![apigw_12_201812](https://static.toastoven.net/prod_apigateway/apigw_12_201812.png)

1. 削除するプラグインをクリックします。

2 .**削除(Delete)**ボタンをクリックします。

3 .**確認(OK)**ボタンをクリックします。

## プラグイン 

### プラグイン動作構造

API Gatewayは、アクセス制御、認証、使用量制限、メッセージ修正などの多様なプラグインを提供します。

プラグインは、ドメインとエンドポイントに適用できます。ドメイン階層に追加したプラグインは、該当ドメインの下にあるエンドポイントに共通で適用されます。

エンドポイント階層に追加したプラグインは、該当エンドポイントにのみ適用されます。 

![](http://static.toastoven.net/prod_apigateway/img_12.png)

API Gatewayがリクエストを受け取ると、設定されたプラグインのプロパティグループ順にプラグインが動作します。

- Access Control filterで、制限されたユーザーのリクエスト、使用制限を超えた時にリクエストを拒否します。 
- Authentification filterで、認証されていないリクエスト、改ざんされたリクエストに対してリクエストを拒否します。 
- Custom filterで、リクエスト/レスポンスに対するメッセージの修正、模擬(mock)レスポンスを処理します。 
- Proxy filterで、ユーザーのAPIサーバーにリクエストをフォワーディングし、レスポンス値を受け取り、リクエストした人に渡します。

## ドメインプラグイン 

### IPアクセス制御(IP ACL)

IP基盤のアクセス制限機能です。特定IPを許可または拒否することができます。

![apigw_13_201812](https://static.toastoven.net/prod_apigateway/apigw_13_201812.png)

1. **プラグイン設定(Plugin Setting) > アクセス制御(Access Control)**プラグインをクリックし、**IPアクセス制御(IP ACL)**を選択します。 

2. 許可(Permit)を通して、設定されたIPリストに対して許可するか拒否するかを設定します。 
  * trueに設定すると、ホワイトリストとして動作します(設定されたIPのみ許可、それ以外のすべてのIPは拒否)。
  * falseに設定すると、ブラックリストとして動作します(設定されたIPのみ拒否、それ以外のすべてのIPは許可)。

3. IPv4形式のIPを入力し、**追加(Add)**ボタンをクリックしてIPリストに追加します。 

4. 設定完了後、**保存(Save)**ボタンをクリックします。 


### 使用量制限(Quota Limit)

一定時間、APIの使用量を制限できます。

![apigw_14_201812](https://static.toastoven.net/prod_apigateway/apigw_14_201812.png)

1. **プラグイン設定(Plugin Setting) > 使用量制限(Quota Limit)**プラグインをクリックし、**使用量制限(Usage Quota)**を選択します。 

2. 使用量制限条件を設定します。 
  * 最大使用限度(Max Usage Quota)に最大API呼び出し可能回数を指定します。 
  * 時間(Per(sec))に秒単位の時間を指定します。 
  * 指定した時間内の最大呼び出し回数を超えた場合、APIの使用が制限されます。 
  * 使用量制限条件を複数追加でき、設定された制限条件のうち、1つ以上の条件が制限量を超えると使用が制限されます。 

> [参考]
> ドメイン設定ページで設定した**使用限度(Usage Quota)**プラグインは、ドメイン下位のすべてのエンドポイントのAPI使用量に対する制限です。  
> エンドポイントごとに使用量制限が必要な場合は、エンドポイントの**エンドポイント使用限度(EndPoint Usage Quota)**プラグインを適用してください。  

3. 設定を保存するには**保存(Save)**ボタンをクリックします。 

### メンテナンス(Maintenance)

定期メンテナンスなどの理由で、すべてのエンドポイントAPI呼び出しに、ユーザーが定義したレスポンス(response)を返すように設定するには、**メンテナンス(Maintenance)**プラグインを使用できます。

![apigw_15_201812](https://static.toastoven.net/prod_apigateway/apigw_15_201812.png)

1. **プラグイン設定(Plugin Setting) > メンテナンス設定(Maintenance)**プラグインをクリックし、**メンテナンス設定(Maintenance Response)**を選択します。

2. メンテナンス(Maintenance)レスポンス値を入力します。

3. 設定を保存するには**保存(Save)**ボタンをクリックします。

配布後、エンドポイントAPI呼び出しに、メンテナンス(Maintenance)プラグインに設定されたレスポンスが返ります。

### 認証(Authentication)

API Gateway認証方式は、HMACとJWT(JSON Web Token)方式があります。

#### HMAC

リクエストURLと時間をメッセージに使用して、HMAC認証を行います。

![apigw_16_201812](https://static.toastoven.net/prod_apigateway/apigw_16_201812.png)

1. **プラグイン設定(Plugin Setting) > 認証(Authentication)**プラグインをクリックし、**HMAC**を選択します。

2. HMACシークレットキー(secret key)とクロックスキュー(clock skew)値を設定します。
> [注意]クロックスキュー(clock skew)設定 
> API Gatewayサーバー時間とクライアントから送ったX-TC-Timestampの差がクロックスキュー(clock skew)より大きい場合は、HMAC認証に失敗します。  
> クロックスキュー(clock skew)値に設定可能な範囲は0～86400(sec)で、0の場合はクロックスキュー(clock skew)を無視します。

3. 設定完了後、**保存(Save)**ボタンをクリックします。

##### 認証(Authentication) > HMAC > 認証API呼び出し

HMAC認証を使用するには、次の値をRequest Headerに含めてリクエストする必要があります。

- Authorization : [Method + "\n "+ URL + "\n "+ Timestamp]を組み合わせ、HmacSHA1アルゴリズムで暗号化した後、Base64でエンコードした値

- X-TC-Timestamp : ISO datetime format (yyyy-MM-dd'T'HH:mm:ssZZ)

| リクエスト                                    | StringToSign                             |
| ---------------------------------------- | ---------------------------------------- |
| GET /test/1?query1=1&query2=2<br>X-TC-Timestamp: 2016-07-23T12:20:02+09:00<br><span style="color:red">Authorization: IqY8u/RZY8IMESwa/TPW9P9Z39Y=</span> | GET\n<br>/test/1?query1=1&query2=2\n<br>2016-07-23T12:20:02+09:00 |

> [参考]リクエスト時間はISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ)に従います。

##### 権限(Authorization)作成コード(Java)
```java
String secretKey = "Consoleで設定したSecret Key";
SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes(), "HmacSHA1");
Mac mac = Mac.getInstance("HmacSHA1");
mac.init(signingKey);

String message = "StringToSign";
byte[] rawHmac;
rawHmac = mac.doFinal(message.getBytes());
String authorization = new String(Base64.encodeBase64(rawHmac));
```

#### JWT(JSON Web Token)

JWT(Json Web Token)認証を行います。

![apigw_17_201812](https://static.toastoven.net/prod_apigateway/apigw_17_201812.png)

1. **プラグイン設定(Plugin Setting) > 認証(Authentication)**プラグインをクリックし、**JWT**を選択します。

2. JWT Secret Keyとクロックスキュー(clock skew)値、そして発行者(issuer)を設定します。

3. 設定完了後、**保存(Save)**ボタンをクリックします。

> [参考]
> API Gatewayサーバーの時間とクライアントから送った終了時間の差がクロックスキュー(clock skew)より大きい場合、JWT認証に失敗します。  
> クロックスキュー(clock skew)には0～86400の値を入力できます。  

##### 認証(Authorization) > JWT (JSON Web Token) > JWT認証API呼び出し

JWT認証を使用するには、次の値をRequest Headerに含めてリクエストする必要があります。

- Authorization : Json Web Token

Request: GET /test/1?query1=1&query2=2<br>
 <span style="color:red">Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJpbnZhbGl...</span>

##### 権限(Authorization)作成コード(Java)

```
<dependency>
    <groupId>org.bitbucket.b_c</groupId>
    <artifactId>jose4j</artifactId>
	<version>0.5.0</version>
</dependency>
```

```
String secretKey = "Consoleで設定したSecret Key";
int expireTimeMinutes = "トークン終了時間=現在時間 + expireTimeMinutes";
String issuer = "Consoleで設定したissuer";

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

Cross-Site方式内でXMLHttpRequest APIを呼び出せるようにします。

![apigw_18_201812](https://static.toastoven.net/prod_apigateway/apigw_18_201812.png)

1. **プラグイン設定(Plugin Setting) > CORS**プラグインをクリックし、**CORS**を選択します。

2. CORS設定値を入力します。

  - Access-Control-Allow-Credentials：資格証明でリクエストする場合、Trueに設定する必要があります。

  - Access-Control-Max-Age：事前リクエスト(Preflight)に対するレスポンスをどれくらいの間キャッシュするかを秒単位で入力します。 0～86400の値を入力できます。
  - Access-Control-Allow-Origin：リソースにアクセスできる原本/ドメインを入力します。
      - *を入力すると、すべてのドメインを許可します。(ただし\*を指定する場合、資格証明をサポートしないため、許可原本(allowed origin)に具体的なドメインを指定する必要があります。) 
      - 指定されたドメインからのみ許可する時は,(カンマ)で区切って入力します。 
      - ドメインはURI(スキーム、ドメイン、ポート)形式で入力する必要があります(例：http://api-gw.toast.com：8080)。
  - Access-Control-Allow-Methods：リソースへのアクセスを許可するメソッドを設定します。複数のメソッドを指定する場合は','で区切って入力します。
  - Access-Control-Allow-Headers：リクエストで使用できるHTTPヘッダを設定します。複数のヘッダを設定する場合は','で区切って入力します。
  - Access-Control-Expose-Headers：ブラウザ(クライアント)がアクセスできるヘッダを設定します。複数のヘッダを設定する場合は','で区切って入力します。
  - CORS規約の詳細はhttps://www.w3.org/TR/cors/を参照してください。

3. 設定完了後、**保存(Save)**ボタンをクリックします。


## エンドポイントプラグイン 

### ユーザー定義レスポンス(Mock Response)

ユーザーがあらかじめ設定したユーザー定義レスポンスを返します。
エンドポイントパスに該当するリクエストURI(request URI)がリクエストされたら、指定されたエンドポイントサーバーにリクエストをフォワーディングせず、ユーザーが設定したユーザー定義レスポンスが返されます。

![apigw_21_201812](https://static.toastoven.net/prod_apigateway/apigw_21_201812.png)

1. **プラグイン(Plugins) > ユーザー定義レスポンス(Mock Response)**プラグインを追加します。

2. ユーザー定義レスポンス(mock response) HTTP STATUS、Header、Bodyを設定し、保存します。
  - HTTP Status：レスポンスのステータスコードを設定します。
  - Headers：レスポンスヘッダ(response header)に追加するヘッダとヘッダ値を設定します。
  - Body：レスポンス本文(response body)内容を設定します。 

3. 設定完了後、**保存(Save)**ボタンをクリックします。

### 事前呼び出しAPI(Pre API)

事前呼び出しAPI(Pre API)は、エンドポイントを呼び出す前に呼び出され、Pre APIのレスポンスコードに応じてエンドポイントを呼び出すかどうかを決定する認証の役割を担います。

API Gatewayを通して入ったリクエストヘッダを含めて事前呼び出しAPI(Pre API)を呼び出し、事前呼び出しAPI(Pre API)では、渡されたヘッダ内容に応じてレスポンスコードを返します。

事前呼び出しAPI(Pre API)のレスポンスコードが200の場合はエンドポイントを呼び出し、レスポンスコードが200以外の時は事前呼び出しAPI(Pre API)のレスポンス結果を返します。
事前呼び出しAPI(Pre API)の呼び出しに失敗した場合は、エラーを返します。

> [参考]  
> API Gatewayは、リクエストのヘッダ情報のみを事前呼び出しAPI(Pre API)のURLに渡します。
> Request URLまたはBody情報は伝達しません。  

![apigw_22_201812](https://static.toastoven.net/prod_apigateway/apigw_22_201812.png)

1. **プラグイン(plugins) > 事前呼び出しAPI(Pre API)**プラグインを追加します。

2. 事前APIのメソッドタイプ(method type)とURLを入力します。

3. 設定完了後、**保存(Save)**ボタンをクリックします。


### ヘッダの修正(Modify Headers)

ヘッダ修正(Modify Headers)プラグインは、エンドポイントサーバーにリクエストをフォワーディングする時にヘッダ値を修正したり、API Gatewayがクライアントに渡すレスポンスのヘッダを修正したりできます。
![apigw_23_201812](https://static.toastoven.net/prod_apigateway/apigw_23_201812.png)

1. **プラグイン(Plugins) > ヘッダ修正(Modify Headers)**プラグインを追加します。

2. 設定情報を入力します。
  - Request Headersは、リクエストヘッダを修正します。
  - Response Headersは、レスポンスヘッダを修正します。

3. 設定完了後、**保存(Save)**ボタンをクリックします。

> [参考]
> 設定したヘッダキーがすでに存在する場合、上書きされます。



### 使用量制限(Usage Quota)

一定時間、パスごとにAPI使用量を制限できます。

![apigw_24_201812](https://static.toastoven.net/prod_apigateway/apigw_24_201812.png)
​	

1. **プラグイン(Plugins) > 使用量制限(Usage Quota)**プラグインを追加します。

2. 設定した時間(sec)中の呼び出しできる最大数を入力します。
  - 使用量制限条件を複数追加でき、設定された制限条件のうち1つ以上の条件が制限量を超えると使用が制限されます。 

3. 設定完了後、**保存(Save)**ボタンをクリックします。


> [注意]  
> 'エンドポイント使用量制限'は、エンドポイントパスごとの使用量制限です。    
> ドメイン使用量制限が必要な場合、ドメイン設定ページの使用量制限(Usage Quota)を設定してください。    
> ドメインとエンドポイントにそれぞれ使用量制限(Usage Quota)プラグインを設定した場合、それぞれ使用制限が適用されます。   
> ドメイン使用量を超過すると、エンドポイントの使用量が超過していなくてもリクエストが拒否され、エンドポイントの使用量も増加します。

使用量制限を超過すると、下記のHTTP STATUS 403レスポンスが返されます。

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```

### URL再作成(URL Rewrite)

Request URLをパターン表現式で再作成するプラグインです。 

![apigw_25_201812](https://static.toastoven.net/prod_apigateway/apigw_25_201812.png)

1. **プラグイン(Plugins) > URL再作成(URL Rewrite)**プラグインを追加します。

2. 設定情報を入力します。
  - URIパターンには、どんなパターン形式のRequest URLに対して再作成するかのパターン形式を入力します。 
  - URI再作成には、(2)で作成したURIパターン形式についてURLを再作成する形式を入力します。 

3. 設定完了後、**保存(Save)**ボタンをクリックします。

#### [例] /api/v2.0/\*\* -> /api/v1.0/\*\*で再作成する場合 

- URIパターン：/api/v2.0/(.\*)
- URI再作成：/api/v1.0/%1

上のルールを適用すると、Request URL `/api/v2.0/members`が` /api/v1.0/members`に変更されてリクエストされます。 


## API配布 

### API配布

![apigw_26_201812](https://static.toastoven.net/prod_apigateway/apigw_26_201812.png)

1. 配布するドメインの**配布(Deploy)**ボタンをクリックします。 

2. 配布したAPIが正常に呼び出されるかをテストします。
 ドメインURLに登録したエンドポイントURLを呼び出した時、期待したレスポンス(response)が返るかを確認します。 

```bash
$ curl -s http://api-gw.cloud.toast.com/apigw/hello
hello world
```

## 統計 

### 統計照会 

API統計では、ドメインごとのAPI呼び出し平均レスポンス時間、ネットワークトラフィック使用量を確認できます。配布(deploy)されたドメインの統計データのみ表示されます。

ドメインリストのドメインをクリックすると、該当ドメインの統計をチャートとURIパターンごとに詳細に確認できます。 
チャートは検索期間に応じて10分、1時間、1日単位で確認できます。

統計データはリアルタイムで集計されません。 
10分、1時間単位のデータは10分ごと、1日単位は1時間ごとに集計されます。

- 6時間未満：10分単位 
- 6時間以上～7日未満：1時間単位 
- 7日以上～30日：1日単位 
最大検索可能期間は30日で、10分単位のデータの統計データは3ヶ月間保管されます。 

![apigw_27_201812](https://static.toastoven.net/prod_apigateway/apigw_27_201812.png)

1. **API Gateway > ダッシュボード(Dashboard)**をクリックし、ダッシュボード画面に移動します。

2. 検索期間を設定すると、該当期間中の統計データを確認できます。 
 検索期間は最大30日以内です。

- ドメインキー：API設定で登録したドメイン固有キー
- API呼び出し成功数：APIの呼び出しに成功した数の合計 
  - API呼び出しの成功基準はResponse HTTP Status Codeが400未満の場合
- API呼び出し失敗数：APIの呼び出しに失敗した数の合計
  - API呼び出しの失敗基準はResponse HTTP Status Codeが400以上の場合
- API Gatewayからすぐにレスポンスが返された数：エンドポイントサーバーにリクエストをフォワーディングせず、API Gatewayからレスポンスが返された場合
  - 特定のプラグインは、API Gatewayからレスポンスを返すこともあります。例えば、IP ACLで許可されていないIP所有者がリクエストした場合、API Gatewayは403 Forbiddenを返します。このようにAPI GatewayのResponseがクライアントに渡したAPI呼び出しの合計です。  
- API呼び出し数：全API呼び出し数の合計 
  - API Gatewayに入った全API呼び出し数(Total API CALL Count = Success + Failures)。
- 平均レスポンス時間(ms)：平均レスポンス速度 
- ネットワークアウトバウンドトラフィック(bytes)：API Gatewayからクライアントに返したレスポンス量の合計 

3. 検索期間を設定し、検索期間内のドメイン別統計情報を確認できます。

4. ドメインリストをクリックし、ドメインの詳細統計を確認できます。 

![apigw_28_201812](https://static.toastoven.net/prod_apigateway/apigw_28_201812.png)

詳細統計では、API呼び出し成功、失敗数、平均レスポンス時間、ネットワークアウトバウンドトラフィックのグラフを確認できます。 

下記の表でエンドポイントパスごとの詳細な統計を確認できます。

>  [参考] CORSプラグイン利用時、API呼び出し数の使用量 
>  CORSプラグインを使用する場合、API呼び出し数が実際の使用量より多くなることがあります。
> 場合によって、CORSリクエストは1つのリクエストに対して、事前(preflight)リクエスト(OPTIONSメソッド)と実際のリクエストの合計2件をリクエストします。
