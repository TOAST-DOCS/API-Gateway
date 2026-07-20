<!-- pre-align:aligned sig=4c627ec8f307 -->

<a id="application-service-api-gateway-enum-code"></a>
## Application Service > API Gateway > Enumコード { #application-service-api-gateway-enum-code }

<a id="enum-code"></a>
## Enumコード { #enum-code }
API v1.0ガイド文書で参照されるEnumコード文書です。

<a id="api-gateway-region"></a>
### API Gatewayリージョン { #api-gateway-region }
- API Gatewayサーバーが位置するリージョンを意味します。

| 名前 | 説明 |
| --- | --- |
| KR1 | 韓国(パンギョ)リージョン |
| KR2 | 韓国(ピョンチョン)リージョン |


<a id="api-gateway-service-type"></a>
### API Gatewayサービスタイプ { #api-gateway-service-type }
- パブリック(Shared)または専用(Dedicated)区分に基づくAPI Gatewayのサービスタイプです。 
- 現在はパブリックAPI Gatewayサービスタイプのみサポートされます。 

| 名前 | 説明 |
| --- | --- |
| SHARED | パブリックAPI Gatewayサービスタイプ |


<a id="http-method-type"></a>
### HTTPメソッドタイプ { #http-method-type }
- サポートされるHTTPメソッドタイプです。

| 名前 | 説明 |
| --- | --- |
| GET | HTTP GETメソッド |
| POST | HTTP POSTメソッド | 
| DELETE | HTTP DELETEメソッド | 
| PUT | HTTP PUTメソッド | 
| OPTIONS | HTTP OPTIONSメソッド | 
| HEAD | HTTP HEADメソッド | 
| PATCH | HTTP PATCHメソッド | 


<a id="resource-plugin-type"></a>
### リソースプラグインタイプ { #resource-plugin-type }
- リソースに設定可能なプラグインタイプです。

| 名前 | 説明 | プラグイン適用可能な場所 |
| --- | --- | --- |
| HTTP | API Gatewayに受信したリクエストを定義されたバックエンドエンドポイントURLパスへ渡します。 | メソッド |
| MOCK | API Gatewayに受信したリクエストに対して定義されたレスポンスを返します。 | メソッド |
| CORS | Cross-Site方式内でXMLHttpRequest APIを呼び出せるようにします。 | リソースパス |
| SET_REQUEST_HEADER | リクエストヘッダの追加または変更を行います。 | リソースパス、メソッド |
| REMOVE_REQUEST_HEADER | リクエストヘッダを削除します。 | リソースパス、メソッド |
| SET_RESPONSE_HEADER | バックエンドレスポンスにヘッダを追加または変更します。 | リソースパス、メソッド |
| REMOVE_RESPONSE_HEADER | バックエンドレスポンスからヘッダを削除します。 | リソースパス、メソッド |
| ADD_REQUEST_QUERY_PARAMETER | バックエンドエンドポイントリクエストにクエリ文字列パラメータを追加します。 | リソースパス、メソッド |


<a id="resource-requestresponse-parameter-data-type"></a>
### リソースリクエスト/レスポンスパラメータデータ型 { #resource-requestresponse-parameter-data-type }
- リソースリクエスト/レスポンスパラメータで設定できるデータ型です。

| 名前 | 説明 |
| --- | --- |
| STRING | Stringデータ型 |
| BOOLEAN | Booleanデータ型 | 
| INTEGER | Integerデータ型 | 
| LONG | Longデータ型 | 
| FLOAT | Floatデータ型 | 
| DOUBLE | Doubleデータ型 | 
| FILE | Fileデータ型。リクエストパラメータ > フォームデータでのみ設定可能。 | 


<a id="stage-resource-plugin-type"></a>
### ステージリソース > プラグインタイプ { #stage-resource-plugin-type }
- ステージリソースパスまたはメソッドに設定可能なプラグインタイプです。 

| 名前 | 説明 | プラグイン適用可能な場所 |
| --- | --- | --- |
| IP_ACL | IPアクセス制限プラグイン | ルート(/)リソースパス |
| HMAC | HMACリクエスト検証プラグイン | ルート(/)リソースパス |
| JWT | JWTトークン検証プラグイン | ルート(/)リソースパス |
| API_KEY | API Key検証プラグイン | リソースパス、メソッド |
| REQUEST_VALIDATOR | リクエストバリデータープラグイン | リソースパス、メソッド |
| PRE_API | 事前呼び出しAPIプラグイン | リソースパス、メソッド |
| RATE_LIMIT | リクエスト数制限プラグイン | メソッド |


<a id="jwt-encryption-algorithm"></a>
### JWT > 暗号化アルゴリズム { #jwt-encryption-algorithm }
- JWTトークンの署名に使用する暗号化アルゴリズムです。

| 名前 | 説明 |
| --- | --- |
| HS256 | 対称鍵アルゴリズムです。HS256(HMAC with SHA-256)アルゴリズムを使用してトークンを署名します。  |
| RS256 | 非対称鍵アルゴリズムです。公開/秘密鍵を使用してRSA256(RSA Signature with SHA-256)アルゴリズムを使用してトークンを署名します。 | 


<a id="jwt-claim-data-type"></a>
### JWT > クレームデータ型 { #jwt-claim-data-type }
- JWTクレームのデータ型です。

| 名前 | 説明 |
| --- | --- |
| Array | 配列形式のデータ型です。  |
| String | 文字列形式のデータ型です。 | 
| NumericDate | ミリ秒を無視して1970-01-01T00:00:00Z UTCから指定されたUTC日/時間までの秒数を表すデータ型です。 |


<a id="jwt-rs256-encryption-algorithm-public-key-type"></a>
### JWT > RS256暗号化アルゴリズム > Public Key Type { #jwt-rs256-encryption-algorithm-public-key-type }
- RS256は公開鍵/秘密鍵ベースの暗号化アルゴリズムを使用します。公開鍵設定方式を設定します。

| 名前 | 説明 |
| --- | --- |
| RSA_PUBLIC_KEY | PEM形式の公開鍵を設定する方式です。 |
| JWKS_URI | 公開鍵を照会できるJson Web Key Sets URIに設定する方式です。|


<a id="request-number-limit-limit-key"></a>
### リクエスト数制限 > 制限キー { #request-number-limit-limit-key }
- リクエスト数制限が適用されるキーです。

| 名前 | 説明 |
| --- | --- |
| DEFAULT | リソースメソッドのリクエスト数制限を適用します。 |
| IP | クライアントIPごとにリソースメソッドのリクエスト数制限を適用します。 |
| HEADER | 指定されたヘッダ名の値ごとにリソースメソッドのリクエスト数制限を適用します。 |
| PATH_VARIABLE | パス変数ごとにリソースメソッドのリクエスト数制限を適用します。 |


<a id="stage-deployment-deployment-status"></a>
### ステージ配布 > 配布状態 { #stage-deployment-deployment-status }
- ステージ配布作業の状態です。

| 名前 | 説明 |
| --- | --- |
| DEPLOYING | 配布進行中 | 
| COMPLETE | 配布完了(成功) | 
| FAILURE | 配布失敗 | 


<a id="usage-plan-quota-period-unit"></a>
### 使用量プラン > 割り当て量期間単位 { #usage-plan-quota-period-unit }
- 割り当て量が初期化される期間単位です。

| 名前 | 説明 |
| --- | --- |
| DAY | 日単位で呼び出し量を制限。毎日UTC 00:00:00に初期化。| 
| MONTH | 月単位で呼び出し量を制限。毎月1日UTC 00:00:00に初期化。 | 


<a id="api-key-status"></a>
### API Keyの状態 { #api-key-status }
- API Keyの状態です。
- 無効になっているAPI Keyは、API Keyの認証に失敗してAPIを呼び出せません。

| 名前 | 説明 |
| --- | --- |
| ACTIVE | 有効状態 | 
| INACTIVE | 無効状態 |


<a id="api-key-type"></a>
### API Keyタイプ { #api-key-type }
- 発行されたAPI KeyのPrimary API KeyとSencondary API Keyのタイプです。 

| 名前 | 説明 |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |


<a id="api-key-subscription-status"></a>
### API Keyの購読状態 { #api-key-subscription-status }
- API Keyの購読状態です。

| 名前 | 説明 |
| --- | --- |
| APPROVAL | 承認状態 | 

<a id="statistics-data-time-unit"></a>
### 統計データ時間単位 { #statistics-data-time-unit }
- 統計データが収集される時間単位

| 名前 | 説明 |
| --- | --- |
| ONE_MINUTES | 1分間隔で統計データ収集 | 
| TEN_MINUTES | 10分間隔で統計データ収集 | 
| ONE_HOURS | 1時間間隔で統計データ収集 | 
| ONE_DAYS | 1日間隔で統計データ収集 | 


<a id="statistics-sort-top-10-services-by"></a>
### 統計 > Top10サービスソート基準 { #statistics-sort-top-10-services-by }
| 名前 | 説明 |
| --- | --- |
| CALL_COUNT | 全体API呼び出し数基準降順ソート | 
| FAIL_CALL_COUNT | 失敗API呼び出し数基準降順ソート | 
| AVG_RESPONSE_TIME | 平均レスポンス時間基準降順ソート | 


<a id="gateway-response-type"></a>
### ゲートウェイレスポンスタイプ { #gateway-response-type }
| ゲートウェイレスポンスタイプ | 基本ステータスコード | 説明 |
| ----------- | -------- | --- |
| UpstreamServiceUnavailable | 503 | バックエンドエンドポイントサービスが応答しない、または応答遅延(60秒以上)が継続的に発生する場合のレスポンスです。 |
| GatewayTimeout | 504 | ゲートウェイの最大応答時間(60秒)を超えた場合に発生するレスポンスです。 |
| Unauthorized | 401 | 認証に必要なリクエスト情報がない場合、または認証に失敗する場合発生するレスポンスです。 |
| JwksError | 500 | JWTのJWKSが正しく設定されていない場合に発生するレスポンスです。 |
| PreApiFailed | 502 | 事前呼び出しAPIがAPI Gatewayのリクエストに応答しない場合に発生するレスポンスです。事前呼び出しAPIのレスポンスステータスコードが200でない場合は、事前呼び出しAPIのレスポンスがそのままクライアントに伝達されます。 |
| Forbidden | 403 | アクセスが許可されていないリクエストを拒否するときに発生するレスポンスです。 |
| RateLimited | 429 | 制限されたリクエスト数を超えたリクエストを拒否するときに発生するレスポンスです。 |
| UsageQuotaExceeded | 429 | 制限されたリクエスト割り当て量を超過するリクエストを拒否したときに発生するレスポンスです。 |
| InvalidUri | 400 | バックエンドエンドポイントのURI構成が正しく設定されていない場合に発生するレスポンスです。 |
| NotFound | 404 | 登録されていないパス及びメソッドでリクエストした場合に発生するレスポンスです。 |
| BadGateway | 502 | バックエンドエンドポイントが応答しない、または応答を拒否した場合に発生するレスポンスです。 |
| InvalidContextVariable | 500 | 無効なコンテキスト変数設定が原因で発生するレスポンスです。 |
| BadRequest | 400 | 無効なクライアントリクエストが原因で発生するレスポンスです。 |
| InternalServerError | 500 | 予期せぬエラーが発生した場合のレスポンスです。 |
