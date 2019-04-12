## Application Service > API Gateway > 概要

## API Gatewayの概要 

API Gatewayは、ユーザーのAPI作成と配布管理を簡単にできるサービスです。 
アクセス制限、トラフィック制御、メッセージ改ざん防止などの、便利なプラグインを提供します。 


## 主な機能 

#### APIの作成、配布、管理 
- API Gatewayは、ユーザーのAPIのリソースとメソッドを手軽に管理し、配布できます。
- API Gatewayで提供するフロントエンドポイントを通して、ユーザーのAPIを表示できます。 
- ユーザーAPIサーバーごとにAPI Gatewayを作成する必要がないので、費用が削減できます。

#### 多様なプラグインの提供 
- アクセス制限(IP ACL)、メッセージ改ざん防止(HMAC、JWT)、トラフィック管理(throttling)などの多様なプラグイン機能を提供します。
- API Gatewayプラグインで提供する機能を利用すると、開発者は主要なビジネスロジックの開発にのみ集中できます。 

#### 多様な統計情報の提供 
- API呼び出し数、HTTPレスポンスコード(response code)別統計、平均レスポンス速度、ネットワークトラフィック使用量などの情報を提供します。

## API Gatewayサービスの流れ

![[図1]サービスの構造](http://static.toastoven.net/prod_apigateway/overview/service_flow.png)

クライアントは、API Gatewayで提供するドメインURLを通して、ユーザーのエンドポイントAPIサーバー(endpoint API server)のURLを呼び出すことができます。

API Gatewayのコンソールで追加のプラグインを設定するだけで、アクセス制御、認証などの機能を追加できます。 
