
## Application Service > API Gateway > リリースノート

### 2019.06.25

#### 機能改善/変更
* プロジェクト別API呼び出し数制限を追加 
  * プロジェクト別のAPI呼び出し数が、毎秒10,000回に制限されます。制限を超えるとリクエストは拒否され、429 Too many requestレスポンスが返されます。
  * 使用量制限の調整が必要な場合は、サポートへお問い合わせください。


### 2019.02.26

#### 機能改善/変更
* [Console]モニタリングプラグインのサービス中断 
  * モニタリングプラグインサービスが中断されます。サービス中断後は、コンソール画面でモニタリングプラグイン機能設定ができません。


### 2018.04.24

#### 機能改善/変更 
* プライベート証明書がインストールされたターゲットサーバーにプロキシができるように改善しました。 

### 2018.02.22

#### 機能改善/変更
* [Console]統計の高度化
  * ユーザーが選択した期間に応じて統計データを照会できます。 (最大検索期間は30日です。)
  * 統計検索期間に応じて統計単位が細分化されました。  
    * 検索期間が6時間未満の場合、10分単位(10分単位の統計は最大30日間提供されます。)
    * 検索期間が1日未満の場合は1時間単位
    * 検索期間が1日を超える場合は1日単位
  * 統計データの種類が追加されました。 
    * Response HTTP Status codeのグループ別件数を確認できます。
    * API Gateway Pluginで、Responseが返された件数を確認できます。
  * 2018.02.22以前の統計データは、高度化以前の統計照会ページで確認できます。 

* [Console]モニタリングプラグイン 
  * モニタリングプラグインで、ユーザーターゲットサーバーの障害を検知できます。 
    * ユーザーターゲットサーバーまたはAPI Gatewayから、Response HTTP Status Codeが400以上のコードがクライアントに返される場合、ユーザーが登録したメールまたは端末番号に通知を送信します。 
* [API] HTTP Deleteリクエストが、Request Bodyを含めてProxyできるように変更されました。 


### 2017.10.26

#### バグ修正
- UriRewrite Pluginのバグ修正
  - [API]有効なRewrite Patternを無効なパターンと認識するエラーを修正しました。 

### 2017.06.22

#### 機能改善/変更
- [Console] CORSプラグインの追加
  - Cross-site間HTTP Requestができるように設定できるCORSプラグインを追加しました。
  - 詳細は<a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#corscross-origin-resource-sharing" target="_blank">Developer`s Guide > Plugin > CORS</a>参照

### 2017.05.25

#### 機能改善/変更
- [Console] domain key入力時、path形式は入力できないように変更
  - path形式のdomain keyはサポートしていないため、path形式のdomain keyを入力できないように変更しました。  
- [Console] Swagger import & exportサポート
  - domain設定情報をswaggerファイルでimport & exportできます。  
  - 詳細は<a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#swagger-import-export" target="_blank">Developer`s Guide > Swagger import & Export</a>参照

#### バグ修正
- [Console] endpoint削除後、Deployボタンが有効にならないバグの修正
  - endpointが削除された場合、設定情報が変更されたのでDeployボタンが有効にならないといけませんが、無効化状態になっていたバグを修正しました。

### 2017.04.20

#### 機能改善/変更
- [Console]エラー発生時、詳細エラーメッセージをalertで表示
- [Console] Deploy実行時、瞬断が発生しないように修正
- [Console] Endpoint Plugin > Usage Quotaプラグインの追加
  - 詳細は<a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#usage-quota" target="_blank">Developer`s Guide > Endpoint Usage Quota</a>参照

### 2017.03.23

#### 機能改善/変更
- [Console] Domain複製機能の追加
  - 詳細は<a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#_5" target="_blank">Developer`s Guide > Domain clone</a>参照
- [API] Target Server API Connectionエラー発生時、詳細なレスポンスコードを返すように変更

### 2017.02.23

#### 機能改善/変更
- [Console] Maintenanceプラグイン機能追加
  - 詳細は<a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#maintenance" target="_blank">Developer`s Guide > Maintenance Plugin</a>参照

#### バグ修正
- [Console]特定Domain Deployが失敗するエラーの修正 
  - Domainを削除した時に一部のデータが残り、同じDomainを登録する場合にDeployが失敗する問題を修正

### 2016.10.06

#### 機能改善/変更
- [Console] Pre APIプラグイン機能追加
- [Console] Header変更プラグイン機能追加
- [API]ファイルアップロードサポート

#### バグ修正
- [API]ターゲットサーバーの401エラーコードなど、一部レスポンスを処理できない問題の修正

### 2016.08.30

#### バグ修正
- [API] HMAC認証エラーの修正
- [API] USAGE QUATA適用時、動作しなかった問題の修正

### 2016.08.18

#### 機能改善/変更
- [Console] Domain下位 IP ACLにsubnet形式追加可能
- [Console] Domain下位Usage Quota/Rate Limitプラグイン削除
- [Console] Domain下位Usage Quota条件を複数登録可能
- [Console] Endpoint下位URL Rewriteプラグインの追加
- [Console] Endpoint登録時、HEAD/PATCHタイプのメソッドを追加可能

#### バグ修正
- [Console]プラグイン設定値が特定条件で見えない問題を修正
- [Console]ドメイン新規登録時に追加したプラグインが抜ける問題を修正
