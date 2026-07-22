<!-- pre-align:aligned sig=59cfa82951f4 -->

<a id="application-service-api-gateway-release-note"></a>
## Application Service > API Gateway > リリースノート { #application-service-api-gateway-release-note }

<a id="july-28-2026"></a>
### 2026. 07. 28. { #july-28-2026 }

<!-- TODO: translate body -->

<a id="july-28-2026-added-features"></a>
#### 機能追加

<!-- TODO: translate body -->

<a id="november-11-2025"></a>
### 2025. 11. 11. { #november-11-2025 }
<a id="november-11-2025-feature-updates"></a>
#### 機能改善・変更
* ユーザーコンソールのUI/UX改善
   * ユーザビリティ向上のため、ユーザーインターフェースを改善しました。
   
<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }
<a id="august-27-2024-feature-updates"></a>
#### 機能改善・変更 
* ゲートウェイレスポンス機能を追加
    * ゲートウェイで定義されたエラーレスポンス設定をユーザーが再定義できます。 
    * 詳細は[コンソールガイド > ゲートウェイレスポンス](./console-guide/#gateway-response)を参照してください。
* サービスゲートウェイ連動 
    * サービスゲートウェイを通じて、NHN Cloud内部ネットワーク内のクライアントがインターネットを経由せずにAPI Gatewayと通信できます。
* ゲートウェイ <-> バックエンドエンドポイント区間で、バックエンドエンドポイントがTLS 1.2未満しかサポートしていない場合、通信がサポートされなくなります。

<a id="july-23-2024"></a>
### 2024. 07. 23. { #july-23-2024 }
<a id="july-23-2024-feature-updates"></a>
#### 機能改善・変更 
* リクエストバリデータープラグインを追加 
    * リクエストバリデーターは、リソースのリクエストパラメータに定義された設定に従ってクライアントのリクエストを検証する機能です。詳細は[コンソールガイド > リクエストバリデーター](./console-guide/#validate-requests)を参照してください。
* コンテキスト変数名にハイフン(-)が含まれている場合、API呼び出しが失敗する現象を改善しました。
* リクエストヘッダ及びレスポンスヘッダ削除機能を追加


<a id="april-23-2024"></a>
### 2024. 04. 23. { #april-23-2024 }
<a id="april-23-2024-feature-updates"></a>
#### 機能改善・変更 

* コンテキスト変数の拡張
    * リクエストとレスポンスに関連する様々なコンテキスト変数が追加されました。追加されたコンテキスト変数は、リソースとステージ設定で活用可能です。
* 詳細は[コンソールガイド > コンテキスト変数](./console-guide/#context-variables)を参照してください。


<a id="august-29-2023"></a>
### 2023. 08. 29. { #august-29-2023 }
<a id="august-29-2023-feature-updates"></a>
#### 機能改善・変更 
* リクエスト制限ポリシー機能の追加 
    * リクエスト制限ポリシーは、リクエストのパス変数またはリクエストヘッダの値ごとにIP ACLとリクエスト数制限を設定できる機能です。
    * 詳細は[コンソール使用ガイド > リクエスト制限ポリシー](./console-guide/#request-restriction-policy)を参照してください。
* ユーザー指定ドメイン機能の追加
    * ステージドメインのPrefixをユーザーが指定した値に設定してドメインを指定できる機能です。
    * 詳細は[コンソール使用ガイド > ユーザー指定ドメイン](./console-guide/#custom-domain)を参照してください。
    * APIレスポンスにユーザー指定ドメイン関連フィールド名がstageAliasDomainListからstageCustomDomainListに変更されました。
* API Keyのインポート/エクスポート機能を追加
    * CSVファイルでAPI Keyをインポートしたり、登録したAPI Keyをエクスポートできます。
    * 詳細は[コンソール使用ガイド > API Keyのインポート](./console-guide/#import-api-key)と[コンソール使用ガイド > API Keyのエクスポート](./console-guide/#export-api-key)を参照してください。
* ユーザー指定Primary/Secondary API KeyでAPI Key作成 
    * ユーザーが指定したPrimary/Sencodary API KeyでAPI Keyを作成できます。
    * 詳細は[コンソール使用ガイド > API Key作成](./console-guide/#create-api-key)を参照してください。
* Top 10サービス照会統計API追加 
    * 全体API呼び出し数、失敗API呼び出し数、平均レスポンス時間を基準に上位10個のAPI Gatewayサービスリストと累積統計を照会できます。
    * 詳細は[API v1.0ガイド > Top 10サービス照会](./api-guide-v1.0/#query-top-10-services)を参照してください。

<a id="july-26-2022"></a>
### 2022. 07. 26. { #july-26-2022 }
<a id="july-26-2022-feature-updates"></a>
#### 機能改善・変更 
* 韓国(ピョンチョン)リージョンオープン
* バックエンドエンドポイントに使用可能なポート範囲が変更されました。
    * 変更前：80, 443, 5000～12000
    * 変更後：80, 443, 10000～12000

<a id="may-24-2022"></a>
### 2022. 05. 24. { #may-24-2022 }
<a id="may-24-2022-feature-updates"></a>
#### 機能改善・変更 
* アクセスログ機能追加 
    * API GatewayのアクセスログをLog & Crash Searchサービスに保管できる機能です。詳細については[アクセスログ](./console-guide/#access-log)を参照してください。

<a id="january-25-2022"></a>
### 2022. 01. 25. { #january-25-2022 }
<a id="january-25-2022-feature-updates"></a>
#### 機能改善・変更
* リソースパスに設定されたプラグインがある場合にサブメソッドを作成すると、リソースパスに設定されたプラグインが追加されるように変更されました。
* リソースの作成と修正に関連するPublic APIが追加されました。
  * [リソースパスとメソッドの作成API](./api-guide-v1.0/#create-resource-paths-and-methods)
  * [リソースメソッド作成API](./api-guide-v1.0/#create-resource-methods)
  * [リソースパスプラグイン修正/削除API](./api-guide-v1.0/#modifydelete-resource-path-plugins)
  * [リソースメソッド情報修正とプラグイン修正API](./api-guide-v1.0/#modifydelete-resource-method-information-and-plugins)
* 統計APIレスポンスフィールドの追加
  * 統計APIのレスポンスに最近の統計データの更新日時のmetricsLatestUpdatedAtフィールドが追加されました。
  * API Key別照会APIのレスポンスに統計データの時間単位のtimeUnitフィールドが追加されました。
  * 詳細については[API v1.0ガイド > 統計 > ステージリソース別照会](./api-guide-v1.0/#query-by-stage-resource), [API v1.0ガイド > 統計 > API Key別照会](./api-guide-v1.0/#query-by-api-key)を参照してください。
* 事前呼び出しAPIのエンドポイント、バックエンドエンドポイントに使用可能なポートの範囲が制限されました。
  * 使用可能なポート番号：80、443、5000~12000

<a id="november-23-2021"></a>
### 2021. 11. 23. { #november-23-2021 }
<a id="november-23-2021-feature-updates"></a>
#### 機能改善・変更 
* API Gateway Public APIサポート 
    * APIを介してAPI Gatewayサービスを利用できます。詳細については[API v1.0ガイド](./api-guide-v1.0/)を参照してください。

<a id="august-24-2021"></a>
### 2021. 08. 24. { #august-24-2021 }
<a id="august-24-2021-feature-updates"></a>
#### 機能改善・変更 
* API説明書追加
    * 詳細は[コンソールガイド > API説明書](./console-guide/#api-documentation)を参照してください。

<a id="july-6-2021"></a>
### 2021.07.06. { #july-6-2021 }
<a id="july-6-2021-feature-updates"></a>
#### 機能改善・変更 
* リクエストクエリ文字列パラメータ追加プラグインを追加
    * 詳細な内容は[コンソールガイド > プラグイン > リクエストクエリ文字列パラメータ追加](./console-guide/#add-request-query-string-parameter)を参照してください。

<a id="june-29-2021"></a>
### 2021.06.29. { #june-29-2021 }
<a id="june-29-2021-feature-updates"></a>
#### 機能改善・変更
* 使用量計画、 API Key機能を追加
    * 詳細な内容は[コンソールガイド > 使用量計画](./console-guide/#usage-plan)、[コンソールガイド > API Key](./console-guide/#api-key), [コンソールガイド > ステージ > API Key](./console-guide/#api-key)を参照してください。

<a id="may-25-2021"></a>
### 2021.05.25. { #may-25-2021 }
<a id="may-25-2021-feature-updates"></a>
#### 機能改善・変更
* ステージパスでバックエンドエンドポイントURLの再定義機能を追加
    * 詳細な内容は[コンソールガイド > バックエンドエンドポイントURL再定義](./console-guide/#backend-endpoint-url-override)を参照してください。
* 配布履歴の確認と、配布履歴のステージ設定で現在のステージ設定を変更する機能を追加
    * 詳細な内容は[コンソールガイド > ステージ配布履歴](./console-guide/#stage-deployment-history)を参照してください。
* 統計データ作成周期の変更
    * 詳細な内容は[コンソールガイド > 統計データ参考事項](./console-guide/#note-on-statistical-data)の統計データ作成周期の内容を参照してください。
* Swaggerファイルでリソースのインポートと、ステージエクスポート機能を追加 
    * Swaggerファイルでリソースをインポートできます。
    * ステージのリソースをSwaggerファイルにエクスポートできます。
    * 詳細な内容は[コンソールガイド > リソース > リソースのインポート](./console-guide/#import-resource)と[コンソールガイド > ステージエクスポート](./console-guide/#export-stage)を参照してください。
* JWTプラグインのJSON Web Key Sets URIをサポート
    * 詳細な内容は[コンソールガイド > JWT](./console-guide/#authentication-jwt)を参照してください。

<a id="march-23-2021"></a>
### 2021.03.23. { #march-23-2021 }
<a id="march-23-2021-feature-updates"></a>
#### 機能改善・変更
* 事前呼び出しAPI(Pre-call API)プラグイン機能を追加
    * 詳細については[コンソールガイド > 事前呼び出しAPI](./console-guide/#pre-call-api)を参照してください。
* リクエスト数制限プラグイン機能を追加
    * 詳細については[コンソールガイド > リクエスト数制限](./console-guide/#request-number-limit)を参照してください。
* 認証 > JWTプラグイン機能を追加
    * 詳細については[コンソールガイド > 認証 > JWT](./console-guide/#authentication-jwt)を参照してください。
* コンテキスト変数${request.clientIp}追加
    * 詳細については[コンソールガイド > コンテキスト変数](./console-guide/#context-variables)を参照してください。

<a id="february-23-2021"></a>
### 2021.02.23. { #february-23-2021 }
<a id="february-23-2021-new-service-release"></a>
#### 新規サービスリリース
* API Gatewayは、簡単にAPIを統合して管理できるサービスです。
* サービスのコード修正や配布を行わずに付加機能を追加できます。 
* ダッシュボードからAPI統計指標を確認することができ、モニタリングおよびAPI品質指標として活用できます。
