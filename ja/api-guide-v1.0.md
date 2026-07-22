<!-- pre-align:aligned sig=2aa8b378450a -->

<a id="application-service-api-gateway-api-v10-guide"></a>
## Application Service > API Gateway > API v1.0ガイド { #application-service-api-gateway-api-v10-guide }

NHN Cloud API Gatewayで提供するPublic API v1.0を説明します。

<a id="api-common-information"></a>
## API共通情報 { #api-common-information }

<a id="api-endpoint"></a>
### APIエンドポイント { #api-endpoint }

APIを呼び出すためのリージョン別エンドポイントは次のとおりです。

| リージョン | エンドポイント |
| --- | --- |
| 韓国(パンギョ)リージョン | https://kr1-apigateway.api.nhncloudservice.com |
| 韓国(ピョンチョン)リージョン | https://kr2-apigateway.api.nhncloudservice.com |
| 韓国(光州)リージョン | https://kr3-apigateway.api.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### 認証と権限 { #authentication-and-authorization }

API Gateway APIを使用するにはAppkeyまたはプロジェクト統合Appkeyが必要です。

Appkeyは、NHN Cloudの各サービスごとに発行される固有の認証キーであり、プロジェクト統合Appkeyは、NHN Cloudの1つのプロジェクト内の複数のサービスに対して共通で使用できる認証キーです。

Appkeyの確認及び使用に関する詳細は、[Appkey](/nhncloud/ja/public-api/appkey/)を参照してください。プロジェクト統合Appkeyの作成及び使用に関する詳細は、[プロジェクト統合Appkey](/nhncloud/ja/public-api/project-integrated-appkey/)を参照してください。

<a id="request-common-information"></a>
### リクエスト共通情報 { #request-common-information }

<a id="request-common-information-path-parameter"></a>
#### Path Parameter

すべてのAPIはアプリキーをPath Parameterで指定する必要があります。
* 例) /v1.0/appkeys/**{appKey}**/**

| 名前   | 説明                  |
| ------ | --------------------- |
| appKey | コンソールで発行されたアプリキー(Appkey) |

<a id="response-common-information"></a>
### レスポンス共通情報 { #response-common-information }

すべてのAPIリクエストに対して**200 OK**でレスポンスします。詳細なレスポンス結果は、次の例のようにレスポンス本文のヘッダを参照します。

<details>
  <summary><strong>成功レスポンス</strong></summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

</details>

| フィールド | タイプ | 説明 |
| --- | --- | --- |
| header               | Object  | ヘッダ領域 |
| header.isSuccessful  | Boolean | 成否 |
| header.resultCode    | Integer | 結果コード |
| header.resultMessage | String  | 結果メッセージ |

<details>
  <summary><strong>失敗レスポンス</strong></summary>

```json
{
  "header": {
    "isSuccessful": false,
    "resultCode": 400,
    "resultMessage": "Bad Request"
  },
  "errorList": [
    {
      "resultCode": 400,
      "errorProperty": "postApigwServiceRequest",
      "errorField": "apigwServiceName",
      "errorMessage": "Cannot be empty."
    }
  ]
}
```

</details>

| フィールド | タイプ | 説明 |
| --- | --- | --- |
| errorList            | List  | エラーリスト領域 |
| errorList[0].resultCode  | Integer | エラーコード |
| errorList[0].errorProperty | String | エラープロパティ(モデル) |
| errorList[0].errorField | String  | エラー詳細フィールド |
| errorList[0].errorMessage | String  | エラーメッセージ |

* 無効なAPIリクエストを行った場合、 errorListフィールドに詳細なエラー原因とフィールド情報がレスポンスされます。

<a id="api-gateway-service"></a>
## API Gatewayサービス { #api-gateway-service }

<a id="list-api-gateway-services"></a>
### API Gatewayサービスリスト照会 { #list-api-gateway-services }
- API Gatewayサービスリストを照会します。

<a id="list-api-gateway-services-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| regionCode | String | 必須 | なし | KR1, KR2 | [API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考 |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

<a id="list-api-gateway-services-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
   "header":{
      "isSuccessful":true,
      "resultCode":0,
      "resultMessage":"SUCCESS"
   },
   "paging":{
      "limit":10,
      "page":1,
      "totalCount":100
   },
   "apigwServiceList":[
      {
         "apigwServiceId":"{apigwServiceId}",
         "apigwServiceAlias":"{apigwServiceAlias}",
         "apigwServiceName":"test api gateway",
         "apigwServiceDescription":"description of test api gateway service",
         "apigwDomain":"api.nhncloudservice.com",
         "appKey":"{appKey}",
         "regionCode":"KR1",
         "serverGroupId":"{serverGroupId}",
         "dedicatedId":null,
         "createdAt":"2021-10-19T07:25:23.000Z",
         "updatedAt":"2021-10-19T07:25:23.000Z",
         "apigwServiceTypeCode":"SHARED"
      }
   ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | ページング領域                                      |
|paging.page                          |Integer | 現在のページ                                      |
|paging.limit                         |Integer | ページあたりの件数                                 |
|paging.totalCount                    |Integer | 総件数                                       |
|apigwServiceList                     |List    | API Gatewayサービスリスト領域                       |
|apigwServiceList[0].apigwDomain         |String  | API Gatewayサービスドメイン                |
|apigwServiceList[0].apigwServiceAlias   |String  | API Gatewayサービスエイリアス             |
|apigwServiceList[0].apigwServiceId      |String  | API GatewayサービスID                  |
|apigwServiceList[0].apigwServiceTypeCode|Enum    | [API GatewayサービスタイプEnumコード](./enum-code/#api-gateway-service-type)参考|
|apigwServiceList[0].appKey              |String  | AppKey                                        |
|apigwServiceList[0].dedicatedId         |String  | 専用API GatewayサービスのID                        |
|apigwServiceList[0].apigwServiceDescription         |String  | API Gatewayサービスの説明                                      |
|apigwServiceList[0].apigwServiceName                |String  | API Gatewayサービス名                                      |
|apigwServiceList[0].regionCode          |Enum    | [API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考 |
|apigwServiceList[0].serverGroupId       |String  | API Gatewayサービスが属すサーバーグループID                              |
|apigwServiceList[0].createdAt           |DateTime| API Gatewayサービス作成日時                                    |
|apigwServiceList[0].updatedAt           |DateTime| API Gatewayサービス修正日時                                    |


<a id="get-api-gateway-service"></a>
### 単一API Gatewayサービス照会 { #get-api-gateway-service }
- API GatewayサービスIDで単一API Gatewayサービスを照会します。

<a id="get-api-gateway-service-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |


<a id="get-api-gateway-service-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:28:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object  | API Gatewayサービス領域                       |
|apigwService.apigwDomain         |String  | API Gatewayサービスドメイン                |
|apigwService.apigwServiceAlias   |String  | API Gatewayサービスエイリアス                          |
|apigwService.apigwServiceId      |String  | API GatewayサービスID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API GatewayサービスタイプEnumコード](./enum-code/#api-gateway-service-type)参考 |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 専用API GatewayサービスのID                        |
|apigwService.apigwServiceDescription         |String  | API Gatewayサービスの説明                                      |
|apigwService.apigwServiceName                |String  | API Gatewayサービス名                                      |
|apigwService.regionCode          |Enum    |[API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考|
|apigwService.serverGroupId       |String  | API Gatewayサービスが属すサーバーグループID                              |
|apigwService.createdAt           |DateTime| API Gatewayサービス作成日時                                    |
|apigwService.updatedAt           |DateTime| API Gatewayサービス修正日時                                    |



<a id="create-api-gateway-service"></a>
### API Gatewayサービスの作成 { #create-api-gateway-service }
- API Gatewayサービスを作成します。
- API Gatewayサーバーが作成されるリージョンを選択できます。現在は韓国(パンギョ)リージョンのみサポートします。
- API Gatewayサービスを作成するとAPI GatewayサービスIDが自動発行されます。


<a id="create-api-gateway-service-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "regionCode": "KR1",
  "apigwServiceName": "service name",
  "apigwServiceDescription": "service description"
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | 必須 | なし | KR1, KR2 | [API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考|
| apigwServiceName | String | 必須 | なし | 最大50文字 | API Gatewayサービス名 |
| apigwServiceDescription | String | 任意 | なし | 最大200文字 | API Gatewayサービスの説明 |


<a id="create-api-gateway-service-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:28:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    | API Gatewayサービス領域                       |
|apigwService.apigwDomain         |String  | API Gatewayサービスドメイン                |
|apigwService.apigwServiceAlias   |String  | API Gatewayサービスエイリアス                          |
|apigwService.apigwServiceId      |String  | API GatewayサービスID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API GatewayサービスタイプEnumコード](./enum-code/#api-gateway-service-type)参考 |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 専用API GatewayサービスのID                        |
|apigwService.apigwServiceDescription         |String  | サービスの説明                                      |
|apigwService.apigwServiceName    |String  | API Gatewayサービス名                                      |
|apigwService.regionCode          |Enum    | [API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考|
|apigwService.serverGroupId       |String  | API Gatewayサービスが属すサーバーグループID                              |
|apigwService.createdAt           |DateTime| API Gatewayサービス作成日時                                    |
|apigwService.updatedAt           |DateTime| API Gatewayサービス修正日時                                    |


<a id="modify-api-gateway-service"></a>
### API Gatewayサービスの修正 { #modify-api-gateway-service }
- API Gatewayサービスの名前と説明を修正します。

<a id="modify-api-gateway-service-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| PUT  | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apigwServiceName": "update service name",
  "apigwServiceDescription": "test of api gateway service"
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceName | String | 必須 | なし | 最大50文字 | API Gatewayサービス名 |
| apigwServiceDescription | String | 任意 | なし | 最大200文字 | API Gatewayサービスの説明 |


<a id="modify-api-gateway-service-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:50:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    |API Gatewayサービス領域                       |
|apigwService.apigwDomain         |String  |API Gatewayサービスドメイン                |
|apigwService.apigwServiceAlias   |String  |API Gatewayサービスエイリアス                          |
|apigwService.apigwServiceId      |String  |API GatewayサービスID                            |
|apigwService.apigwServiceTypeCode|Enum    |[API GatewayサービスタイプEnumコード](./enum-code/#api-gateway-service-type)参考|
|apigwService.appKey              |String  |AppKey                                        |
|apigwService.dedicatedId         |String  |専用API GatewayサービスのID                        |
|apigwService.apigwServiceDescription         |String  |サービスの説明                                      |
|apigwService.apigwServiceName                |String  |サービス名                                      |
|apigwService.regionCode          |Enum    |[API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考|
|apigwService.serverGroupId       |String  |サービスが属すサーバーグループID                              |
|apigwService.createdAt           |DateTime|サービス作成日時                                    |
|apigwService.updatedAt           |DateTime|サービス修正日時                                    |

<a id="delete-api-gateway-service"></a>
### API Gatewayサービスの削除 { #delete-api-gateway-service }
- API Gatewayサービスを削除します。  
- API Gatewayサービスを削除するとすべてのステージが削除されます。  
- 削除しようとしているAPI Gatewayサービスのステージが使用量プランと関連付けられている場合は、削除できません。削除するには使用量プランに関連付けられているステージの関連付けを全て削除した後、削除してください。
- 削除されたAPI Gatewayサービスは復元できないため、注意してください。

<a id="delete-api-gateway-service-request"></a>
#### リクエスト

[URI]

| メソッド  | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

<a id="delete-api-gateway-service-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

</details>

<a id="resource"></a>
## リソース { #resource }

<a id="list-resources"></a>
### リソース照会 { #list-resources }

- リソースリストを照会します。

<a id="list-resources-request"></a>
#### リクエスト

[URI]

| メソッド | URI | 
| --- | --- | 
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |

<a id="list-resources-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "15ea79f5-a0fc-4f78-a498-c7c49898dcb4",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-10-25T05:05:23.000Z",
      "updatedAt": "2021-10-25T05:05:23.000Z",
      "resourcePluginList": []
    },
    {
      "resourceId": "f7906669-687b-423a-9101-6f86f2777d2f",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/path",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-10-25T05:06:10.000Z",
      "updatedAt": "2021-10-25T05:06:10.000Z",
      "resourcePluginList": []
    },
    {
      "resourceId": "cd66701a-e2a8-47d2-b3cb-245a6d8e0145",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/path",
      "methodType": "GET",
      "methodName": "example",
      "methodDescription": "This is a method description",
      "createdAt": "2021-10-25T05:06:10.000Z",
      "updatedAt": "2021-10-25T05:06:10.000Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "847efa44-f405-4b43-824b-95ec1a146ac4",
          "resourceId": "cd66701a-e2a8-47d2-b3cb-245a6d8e0145",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/path",
            "backendEndpointPath": "/anything"
          },
          "createdAt": "2021-10-25T05:06:10.000Z",
          "updatedAt": "2021-10-25T05:06:10.000Z"
        }
      ]
    }
  ]
}
```

</details>

| フィールド                                                   | タイプ     | 説明                                           |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | リソースリスト領域                                    |
| resourceList[0].resourceId                             | String   | リソースID                                         |
| resourceList[0].apigwServiceId                         | String   | API GatewayサービスID                             |
| resourceList[0].path                                   | String   | リソースパス                                       |
| resourceList[0].createdAt                              | DateTime | リソース作成日時                                     |
| resourceList[0].updatedAt                              | DateTime | リソース修正日時                                     |
| resourceList[2].methodType                             | Enum     | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourceList[2].methodName                             | String   | メソッドリソース名                                   |
| resourceList[2].methodDescription                      | String   | メソッドリソースの説明                                   |
| resourceList[2].resourcePluginList                     | List     | リソースプラグインリスト領域                               |
| resourceList[2].resourcePluginList[0].resourcePluginId | String   | リソースプラグインID                                    |
| resourceList[2].resourcePluginList[0].resourceId       | String   | リソースID                                         |
| resourceList[2].resourcePluginList[0].pluginType       | Enum     | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考  |
| resourceList[2].resourcePluginList[0].pluginConfigJson | Object   | [リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin)別のJSON設定値参考                 |
| resourceList[2].resourcePluginList[0].createdAt        | DateTime | リソースプラグインの作成日時                                |
| resourceList[2].resourcePluginList[0].updatedAt        | DateTime | リソースプラグインの修正日時                                |

<a id="create-resource-paths-and-methods"></a>
### リソースパスとメソッド作成 { #create-resource-paths-and-methods }
- 複数のリソースパスとメソッドを作成し、作成と同時にプラグインを設定できます。
- リソースメソッドは任意入力です。作成されたリソースパスの下にメソッドを追加するには[リソースメソッド作成](./api-guide-v1.0/#create-resource-methods) APIを使用する必要があります。
- リソースメソッドにはHTTPまたはMOCKプラグインのいずれかを必ず設定する必要があります。 HTTPとMOCKプラグインを同時に設定することはできません。
- 作成されたリソースパスは修正できません。
- pathPluginListフィールドに定義されているリソースパスプラグインは、そのパスのサブメソッドに適用されるプラグインリストです。

<a id="create-resource-paths-and-methods-request"></a>
#### リクエスト

[URI]

| メソッド | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
   "resourcePathList":[
      {
         "path":"/members/{memberId}",
         "pathPluginList":[
            {
               "pluginConfigJson":{
                  "allowedMethods":[
                     "GET",
                     "POST",
                     "DELETE",
                     "PUT",
                     "OPTIONS",
                     "HEAD",
                     "PATCH"
                  ],
                  "allowedHeaders":[
                     "*"
                  ],
                  "allowedOrigins":[
                     "*"
                  ],
                  "exposedHeaders":[
                     
                  ],
                  "maxCredentialsAge":null,
                  "allowCredentials":false
               },
               "pluginType":"CORS"
            }
         ],
         "methodList":[
            {
               "methodDescription":"Edit a member information",
               "methodName":"PutMember",
               "methodPluginList":[
                  {
                     "pluginConfigJson":{
                        "frontendEndpointPath":"/members/{memberId}",
                        "backendEndpointPath":"/api/v1/members/${request.path.memberId}"
                     },
                     "pluginType":"HTTP"
                  }
               ],
               "methodType":"PUT"
            },
            {
               "methodDescription":"Query a member",
               "methodName":"GetMember",
               "methodPluginList":[
                  {
                     "pluginConfigJson":{
                        "frontendEndpointPath":"/members/{memberId}",
                        "backendEndpointPath":"/api/v1/members/${request.path.memberId}"
                     },
                     "pluginType":"HTTP"
                  },
                  {
                     "pluginConfigJson":{
                        "parameters":{
                           "id":"${request.path.memberId}"
                        }
                     },
                     "pluginType":"ADD_REQUEST_QUERY_PARAMETER"
                  }
               ],
               "methodType":"GET"
            }
         ]
      }
   ]
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| resourcePathList | List | 必須 | なし | なし | リソースパスリスト |
| resourcePathList[0] | Object | 必須 | なし | なし | リソースパス領域 |
| resourcePathList[0].path | Object | 必須 | なし | 英字、数字、パス変数、制限文字(. + - /)で構成される有効なパス | リソースパス |
| resourcePathList[0].pathPluginList | List | 任意 | なし | なし | リソースパスプラグインリスト |
| resourcePathList[0].pathPluginList[0] | Object | 任意 | なし | なし | リソースパスプラグイン領域 |
| resourcePathList[0].pathPluginList[0].pluginType | Enum | 必須 | なし | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)のうちリソースパスに設定可能なプラグインタイプ |
| resourcePathList[0].pathPluginList[0].pluginConfigJson | Object | 必須 | なし | なし | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考。|
| resourcePathList[0].methodList | List | 任意 | なし | なし | リソースパス下のメソッドリスト |
| resourcePathList[0].methodList[0] | Object | 任意 | なし | なし | リソースパス下のメソッド領域 |
| resourcePathList[0].methodList[0].methodType | Enum | 必須 | なし | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourcePathList[0].methodList[0].methodName | String | 必須 | なし | 最大50文字 | メソッド名 |
| resourcePathList[0].methodList[0].methodDescription | String | 任意 | なし | 最大200文字 | メソッド説明 |
| resourcePathList[0].methodList[0].methodPluginList | List | 必須 | なし | なし | リソースメソッドプラグインリスト |
| resourcePathList[0].methodList[0].methodPluginList[0] | Object | 必須 | なし | なし | リソースメソッドプラグイン領域、 'HTTP'または'MOCK'のいずれかのプラグインは必須入力 |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginType | Enum | 必須 | なし | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)のうちリソースメソッドに設定可能なプラグインタイプ |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginConfigJson | Object | 必須 | なし | なし | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考。|

<a id="create-resource-paths-and-methods-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.297Z",
      "updatedAt": "2021-12-23T23:55:11.297Z",
      "resourcePluginList": [],
      "parentPath": "/"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.298Z",
      "updatedAt": "2021-12-23T23:55:11.298Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.298Z",
          "updatedAt": "2021-12-23T23:55:11.298Z"
        }
      ],
      "parentPath": "/members"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "PUT",
      "methodName": "PostMember",
      "methodDescription": "Edit a member info",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "24bef5d0-feaf-4469-9619-a31e9e35a622",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId": "321d99cc-cb26-473e-ab76-84249a82b262",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "GET",
      "methodName": "GetMember",
      "methodDescription": "Query a member",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "ADD_REQUEST_QUERY_PARAMETER",
          "pluginConfigJson": {
            "parameters": {
              "id": "${request.path.memberId}"
            }
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "OPTIONS",
      "methodName": "CORS",
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    }
  ]
}
```

</details>

| フィールド                                                   | タイプ     | 説明                                           |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | リソースリスト領域                                    |
| resourceList[1].resourceId                             | String   | リソースID                                         |
| resourceList[1].apigwServiceId                         | String   | API GatewayサービスID                             |
| resourceList[1].path                                   | String   | リソースパス                                       |
| resourceList[1].parentPath                             | String   | 親リソースパス                                       |
| resourceList[1].createdAt                              | DateTime | リソース作成日時                                     |
| resourceList[1].updatedAt                              | DateTime | リソース修正日時                                     |
| resourceList[1].methodType                             | Enum     | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourceList[1].methodName                             | String   | メソッドリソース名                                   |
| resourceList[1].methodDescription                      | String   | メソッドリソース説明                                   |
| resourceList[1].resourcePluginList                     | List     | リソースプラグインリスト領域                               |
| resourceList[1].resourcePluginList[0].resourcePluginId | String   | リソースプラグインID                                    |
| resourceList[1].resourcePluginList[0].resourceId       | String   | リソースID                                         |
| resourceList[1].resourcePluginList[0].pluginType       | Enum     | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考  |
| resourceList[1].resourcePluginList[0].pluginConfigJson | Object   | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考                 |
| resourceList[1].resourcePluginList[0].createdAt        | DateTime | リソースプラグイン作成日時                                |
| resourceList[1].resourcePluginList[0].updatedAt        | DateTime | リソースプラグイン修正日時                                |


<a id="create-resource-methods"></a>
### リソースメソッドの作成 { #create-resource-methods }
- 作成されたリソースパスの下にリソースメソッドを作成します。
- リソースメソッドにはHTTPまたはMOCKプラグインのいずれかを必ず設定する必要があります。 HTTPとMOCKプラグインを同時に設定することはできません。

<a id="create-resource-methods-request"></a>
#### リクエスト

[URI]

| メソッド | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/methods |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId | String | 必須  | なし | なし   | リソースパスID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "methodList": [
    {
      "methodType": "DELETE",
      "methodName": "DeleteMember",
      "methodDescription": "Delete a member",
      "methodPluginList": [
        {
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          }
        }
      ]
    }
  ]
}   
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| methodList | List | 必須 | なし | なし | リソースパス下のメソッドリスト |
| methodList[0] | Object | 必須 | なし | なし | リソースパス下のメソッド領域 |
| methodList[0].methodType | Enum | 必須 | なし | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| methodList[0].methodName | String | 必須 | なし | 最大50文字 | メソッド名 |
| methodList[0].methodDescription | String | 任意 | なし | 最大200文字 | メソッド説明 |
| methodList[0].methodPluginList | List | 必須 | なし | なし | リソースメソッドプラグインリスト |
| methodList[0].methodPluginList[0] | Object | 必須 | なし | なし | リソースメソッドプラグイン領域、'HTTP'または'MOCK'のいずれかのプラグインは必須入力 |
| methodList[0].methodPluginList[0].pluginType | Enum | 必須 | なし | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)のうち、リソースメソッドに設定可能なプラグインタイプ |
| methodList[0].methodPluginList[0].pluginConfigJson | Object | 必須 | なし | なし | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考。|

<a id="create-resource-methods-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members/{memberId}",
      "methodType": "GET",
      "methodName": "GetMember",
      "methodDescription": "Query a member",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "ADD_REQUEST_QUERY_PARAMETER",
          "pluginConfigJson": {
            "parameters": {
              "id": "${request.path.memberId}"
            }
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ]
    },
    ...
  ]
}
```

</details>

| フィールド                                                   | タイプ     | 説明                                           |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | リソースリスト領域                                    |
| resourceList[0].resourceId                             | String   | リソースID                                         |
| resourceList[0].apigwServiceId                         | String   | API GatewayサービスID                             |
| resourceList[0].path                                   | String   | リソースパス                                       |
| resourceList[0].parentPath                             | String   | 親リソースパス                                       |
| resourceList[0].createdAt                              | DateTime | リソース作成日時                                     |
| resourceList[0].updatedAt                              | DateTime | リソース修正日時                                     |
| resourceList[0].methodType                             | Enum     | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourceList[0].methodName                             | String   | メソッドリソース名                                   |
| resourceList[0].methodDescription                      | String   | メソッドリソース説明                                   |
| resourceList[0].resourcePluginList                     | List     | リソースプラグインリスト領域                               |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | リソースプラグインID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | リソースID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考  |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考                 |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | リソースプラグイン作成日時                                |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | リソースプラグイン修正日時                                |


<a id="modifydelete-resource-path-plugins"></a>
### リソースパスプラグイン修正/削除 { #modifydelete-resource-path-plugins }
- リソースパスプラグインを追加、修正、削除します。
- リソースパスに追加されていないプラグインを設定するとプラグインが追加されます。
- リソースパスに追加されたプラグインを設定すると、リクエストしたプラグイン設定に変更されます。
- deleteフィールドをtrueに設定すると、リクエストしたプラグインタイプのプラグインが削除されます。 deleteフィールドがtrueの場合、pluginConfigJsonフィールドは定義する必要はありません。
- applyChildPathフィールドをtrueに設定すると、リソースパス下のすべてのパスとメソッドにプラグインが設定されます。
- applyChildPathとdeleteフィールドの両方をtrueに設定すると、リソースパス下のすべてのパスとメソッドからプラグインが削除されます。
- CORSプラグインを設定すると、サブメソッドとしてOPTIONSメソッドが自動的に作成されます。もし既に存在するOPTIONSメソッドがある場合は削除され、置き換えられるため注意してください。
- リソースパスに設定可能なプラグインのみ設定できます。詳細については、[リソースプラグイン](./api-guide-v1.0/#resource-plugin)を参照してください。

<a id="modifydelete-resource-path-plugins-request"></a>
#### リクエスト

[URI]

| メソッド | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-paths/{resourceId} |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId | String | 必須  | なし | なし   | リソースパスID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "pathPluginList":[
    {
      "applyChildPath": true,
      "delete": true,
      "pluginConfigJson":{
        "allowedMethods":[
            "GET",
            "POST",
            "DELETE",
            "PUT",
            "OPTIONS",
            "HEAD",
            "PATCH"
        ],
        "allowedHeaders":[
            "*"
        ],
        "allowedOrigins":[
            "*"
        ],
        "exposedHeaders":[
            
        ],
        "maxCredentialsAge":null,
        "allowCredentials":false
      },
      "pluginType":"CORS"
    }
  ]  
}   
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pathPluginList | List | 任意 | なし | なし | リソースパスプラグインリスト |
| pathPluginList[0] | Object | 任意 | なし | なし | リソースパスプラグイン領域 |
| pathPluginList[0].pluginType | Enum | 必須 | なし | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER,ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)のうち、リソースパスに設定可能なプラグインタイプ |
| pathPluginList[0].pluginConfigJson | Object | 条件付き必須 | なし | なし | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考、 deleteフィールドがfalseの場合は必須入力|
| pathPluginList[0].applyChildPath | Boolean | 任意 | false | true, false | サブパスとメソッドに上書きするかどうか |
| pathPluginList[0].delete | Boolean | 任意 | false | true, false | プラグインを削除するかどうか |

<a id="modifydelete-resource-path-plugins-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members",
      "methodType": "DELETE",
      "methodName": "DeleteMember",
      "methodDescription": "Delete a member",
      "createdAt": "2021-12-23T23:55:11.298Z",
      "updatedAt": "2021-12-23T23:55:11.298Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.298Z",
          "updatedAt": "2021-12-23T23:55:11.298Z"
        }
      ]
    }
    ...
  ]
}
```

</details>

| フィールド                                                   | タイプ     | 説明                                           |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | リソースリスト領域                                    |
| resourceList[0].resourceId                             | String   | リソースID                                         |
| resourceList[0].apigwServiceId                         | String   | API GatewayサービスID                             |
| resourceList[0].path                                   | String   | リソースパス                                       |
| resourceList[0].parentPath                             | String   | 親リソースパス                                       |
| resourceList[0].createdAt                              | DateTime | リソース作成日時                                     |
| resourceList[0].updatedAt                              | DateTime | リソース修正日時                                     |
| resourceList[0].methodType                             | Enum     | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourceList[0].methodName                             | String   | メソッドリソース名                                   |
| resourceList[0].methodDescription                      | String   | メソッドリソース説明                                   |
| resourceList[0].resourcePluginList                     | List     | リソースプラグインリスト領域                               |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | リソースプラグインID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | リソースID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考  |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考                 |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | リソースプラグイン作成日時                                |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | リソースプラグイン修正日時                                |


<a id="modifydelete-resource-method-information-and-plugins"></a>
### リソースメソッド情報とプラグイン修正/削除 { #modifydelete-resource-method-information-and-plugins }
- リソースメソッドの名前、説明を修正できます。
- リソースメソッドプラグインを追加、修正、削除します。
- リソースメソッドに追加されていないプラグインを設定するとプラグインが追加されます。
- リソースメソッドに追加されたプラグインを設定すると、リクエストしたプラグイン設定に変更されます。
- deleteフィールドをtrueに設定すると、リクエストしたプラグインタイプのプラグインが削除されます。 deleteフィールドがtrueの場合、pluginConfigJsonフィールドは定義する必要はありません。
- リソースメソッドに設定可能なプラグインのみ設定できます。詳細については[リソースプラグイン](./api-guide-v1.0/#resource-plugin)を参照してください。

<a id="modifydelete-resource-method-information-and-plugins-request"></a>
#### リクエスト

[URI]

| メソッド | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-methods/{resourceId} |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId | String | 必須  | なし | なし   | リソースメソッドID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "methodName":"PutMember",
  "methodDescription":"Edit a member information",
  "methodPluginList":[
    {
        "pluginConfigJson":{
          "frontendEndpointPath":"/members/{memberId}",
          "backendEndpointPath":"/api/v2/members/${request.path.memberId}"
        },
        "pluginType":"HTTP"
    },
    {
      "delete": true,
      "pluginType": "ADD_REQUEST_QUERY_PARAMETER"
    }
  ]
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| methodName | String | 必須 | なし | 最大50文字 | メソッド名 |
| methodDescription | String | 任意 | なし | 最大200文字 | メソッド説明 |
| methodPluginList | List | 任意 | なし | なし | リソースメソッドプラグインリスト |
| methodPluginList[0] | Object | 必須 | なし | なし | リソースメソッドプラグイン領域 |
| methodPluginList[0].pluginType | Enum | 必須 | なし | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)のうち、リソースメソッドに設定可能なプラグインタイプ |
| methodPluginList[0].pluginConfigJson | Object | 条件付き必須 | なし | なし | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考、 deleteフィールドがfalseの場合は必須入力|
| methodPluginList[0].delete | Boolean | 任意 | false | なし | プラグイン削除するかどうか |

<a id="modifydelete-resource-method-information-and-plugins-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members/{memberId}",
      "methodType": "PUT",
      "methodName": "PostMember",
      "methodDescription": "Edit a member info",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "24bef5d0-feaf-4469-9619-a31e9e35a622",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v2/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ]
    }
  ]
}
```

</details>

| フィールド                                                   | タイプ     | 説明                                           |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | リソースリスト領域                                    |
| resourceList[0].resourceId                             | String   | リソースID                                         |
| resourceList[0].apigwServiceId                         | String   | API GatewayサービスID                             |
| resourceList[0].path                                   | String   | リソースパス                                       |
| resourceList[0].parentPath                             | String   | 親リソースパス                                       |
| resourceList[0].createdAt                              | DateTime | リソース作成日時                                     |
| resourceList[0].updatedAt                              | DateTime | リソース修正日時                                     |
| resourceList[0].methodType                             | Enum     | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| resourceList[0].methodName                             | String   | メソッドリソース名                                   |
| resourceList[0].methodDescription                      | String   | メソッドリソース説明                                   |
| resourceList[0].resourcePluginList                     | List     | リソースプラグインリスト領域                               |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | リソースプラグインID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | リソースID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考  |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [リソースプラグインタイプ別のJSON設定値](./api-guide-v1.0/#resource-plugin)参考                 |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | リソースプラグイン作成日時                                |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | リソースプラグイン修正日時                                |


<a id="delete-resource"></a>
### リソースの削除 { #delete-resource }
- リソースを削除します。
- ルート("/")パスリソースは削除できません。
- CORSプラグインにより作成されたOPTIONSメソッドは削除できません。 
CORSプラグインにより作成されたOPTIONSメソッドは、CORSプラグインが設定されたリソースからプラグインを削除すると一括削除されます。
- パスリソースを削除すると、サブパスとメソッドリソースが全て削除されます。
- 削除されたリソースは復元できませ。

<a id="delete-resource-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| resourceId | String | 必須 | なし | なし | リソースID |

<a id="delete-resource-response"></a>
#### レスポンス

[Response Body]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

<a id="import-resource"></a>
### リソースのインポート { #import-resource }
- [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/)形式のファイルからリソースを取得します。
- リソースをインポートすると、そのサービスに作成されていた既存のリソースは全て削除され、インポートしたリソースで上書きされます。
- リソースをインポートすると、そのサービスに作成されていた既存のモデルは全て削除され、インポートしたモデルで上書きされます。
- Swagger paths > path > operationで有効ではないoperationのデータは無視され、登録されませんので注意してください。

<a id="import-resource-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| POST  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/import |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "swaggerData": {
    "info": {
      "title": "Swagger Petstore",
      "version": "1.0.5"
    },
    "paths": {
      "/pet/{petId}": {
        "get": {
          "summary": "Find pet by ID",
          "description": "Returns a single pet",
          "consumes": [
            "application/json"
          ],
          "parameters": [
            {
              "name": "userId",
              "in": "header",
              "required": false,
              "type": "string"
            }
          ],
          "produces": [
            "application/json"
          ],
          "responses": {
            "200": {
              "description": "successful operation",
              "headers": {
                "response-header1": {
                  "description": "This is a response header",
                  "type": "string"
                }
              },
              "schema": {
                "$ref": "#/definitions/Pet"
              }
            }
          },
          "x-nhncloud-apigateway": {
            "plugins": {
              "MOCK": {
                "statusCode": 200,
                "headers": {
                  "Content-Type": "application/json"
                },
                "body": "{\"id\":1,\"name\":\"Dog1\"}\"}"
              }
            }
          }
        }
      }
    },
    "definitions": {
      "Pet": {
        "type": "object",
        "required": [
          "name"
        ],
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| swaggerData | Object  | 必須  | なし | Swagger JSON形式 | [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) |
| swaggerData.info | Object | 必須 | なし | なし | APIのメタデータ領域。 [Info Object](https://swagger.io/specification/v2/#swagger-object)参考 |
| swaggerData.info.title | String | 任意 | なし | なし | APIのタイトル。 [Info Object](https://swagger.io/specification/v2/#info-object)参考 |
| swaggerData.info.version | String  | 任意 | なし | なし | APIのバージョン情報。 [Info Object](https://swagger.io/specification/v2/#info-object)参考 |
| swaggerData.paths | Object | 必須 | なし | なし | API Gatewayパスを設定するAPIのパス情報を持つオブジェクト領域。 [Paths Object](https://swagger.io/specification/v2/#paths-object)参考 |
| swaggerData.paths.{path} | Object | 必須 | なし | {path}最大255文字 | API Gatewayパス{path}と{path}内のメソッド情報を持つオブジェクト領域。 [Paths Item Object](https://swagger.io/specification/v2/#path-item-object)参考 |
| swaggerData.paths.{path}.{operation} | Object | 任意 | なし | {operation} get, post, put, delete, head, options, patch | API Gatewayメソッド{operation}とメソッド情報を持つオブジェクト領域。有効ではないoperationのデータは無視され、登録されません。 [Operation Object](https://swagger.io/specification/v2/#operation-object)参考 |
| swaggerData.paths.{path}.{operation}.summary | String | 任意 | {operation}大文字 | 最大50文字 | API Gatewayメソッド名。 |
| swaggerData.paths.{path}.{operation}.description | String | 任意 | {operation}大文字 | 最大200文字 | API Gatewayメソッド説明。 |
| swaggerData.paths.{path}.{operation}.consumes | Array | 任意 | Empty Array | なし | API Gatewayリソースリクエストパラメータ > コンテンツタイプリスト領域。 |
| swaggerData.paths.{path}.{operation}.consumes[0] | String  | 任意 | なし | \*/\* 形式 | API Gatewayリソースリクエストパラメータ > コンテンツタイプ。 |
| swaggerData.paths.{path}.{operation}.parameters | Array | 任意 | なし | なし | API Gatewayリソースリクエストパラメータ > クエリ文字列、ヘッダ、フォームデータ、リクエスト本文領域。 [Parameter Object](https://swagger.io/specification/v2/#parameter-object)参考 |
| swaggerData.paths.{path}.{operation}.parameters[0].name | String | 必須 | なし | 最大50文字 | API Gatewayリソースリクエストパラメータ > クエリ文字列、ヘッダ、フォームデータ、リクエスト本文の名前。 |
| swaggerData.paths.{path}.{operation}.parameters[0].in | String | 必須 | なし | query, header, formData, body | API Gatewayリソースリクエストパラメータ > クエリ文字列、ヘッダ、フォームデータ、リクエスト本文区分。 |
| swaggerData.paths.{path}.{operation}.parameters[0].description | String | 任意 | なし | 最大200文字 | API Gatewayリソースリクエストパラメータ > クエリ文字列、ヘッダ、フォームデータ、リクエスト本文の説明。 |
| swaggerData.paths.{path}.{operation}.parameters[0].required | Boolean | 必須 | なし | true, false | API Gatewayリソースリクエストパラメータ > クエリ文字列、ヘッダ、フォームデータ、リクエストが本文必須かどうか。 |
| swaggerData.paths.{path}.{operation}.produces | Array | 任意 | Empty Array | なし | API Gatewayリソースレスポンス > コンテンツタイプリスト領域。 |
| swaggerData.paths.{path}.{operation}.produces[0] | String | 任意 | なし | \*/\* 形式 | API Gatewayリソースレスポンス > コンテンツタイプ。 |
| swaggerData.paths.{path}.{operation}.responses | Object | 任意 | なし | なし | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード情報を持つオブジェクト領域。 [Responses Object](https://swagger.io/specification/v2/#response-object)参考 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode} | Object | 任意 | なし | {httpStatusCode} 100～599 | API Gatewayリソースレスポンス > レスポンスHTTPステータスコードオブジェクト領域。 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.description | String | 任意 | なし |最大200文字 | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > 説明。 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers | Object | 任意 | なし | なし | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > ヘッダオブジェクト領域。 [Header Object](https://swagger.io/specification/v2/#headers-object)参考 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName} | Object | 任意 | なし | {headerName}最大50文字 | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > ヘッダ領域。 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.description | String | 任意 | なし | 最大200文字 | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > ヘッダ > 説明。 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.type | String | 必須 | なし | string, number, integer, boolean | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > ヘッダ > データ型。 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema | Object | 任意 | なし | なし | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > レスポンス本文領域。|
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema.$ref | String | 必須 | なし | Swagger definitionsに宣言されたオブジェクト | API Gatewayリソースレスポンス > レスポンスHTTPステータスコード > レスポンス本文 > モデル。 |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway | Object | 任意 | なし | なし | API Gateway提供機能定義オブジェクト領域。 |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins | Object | 必須 | なし | なし | API Gatewayユーザー定義プラグインオブジェクト領域。 |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins.{pluginCode} | Object | 必須 | なし | {pluginCode} HTTP, MOCK, CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type)参考。 [リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin)別JSON設定値参考。 |
| swaggerData.definitions | Object | 任意 | なし | なし | API Gatewayリソースリクエストパラメータ、レスポンスで使用される本文オブジェクト定義領域。 [Definitions Object](https://swagger.io/specification/v2/#definitionsObject)参考 |




<a id="resource-plugin"></a>
## リソースプラグイン { #resource-plugin }

<a id="http"></a>
### HTTP { #http }
- API Gatewayでリクエストを受信するリソースパスにリクエストを伝達するバックエンドエンドポイントパスを設定します。
- リソースメソッドにのみ設定可能です。
- MOCKプラグインと同時に設定できません。

```json
{
  "frontendEndpointPath": "/path",
  "backendEndpointPath": "/anything"
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| frontendEndpointPath | String | 必須 | なし | 最大255文字 | API Gatewayでリクエストを受信するリソースパス |
| backendEndpointPath  | String | 必須 | なし | 最大255文字 | API Gatewayから受信したリクエストを伝達するバックエンドエンドポイントパス |

<a id="mock"></a>
### MOCK { #mock }
- 受信したリクエストに対して定義されたレスポンスを返します。
- リソースメソッドにのみ設定できます。
- HTTPプラグインと同時に設定できません。
```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"isSuccess\":true}\"}"
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| statusCode | String | 必須 | なし | 100～599 | ユーザー定義レスポンスHTTPステータスコード               |
| headers | Map | 任意 | なし | なし |ユーザー定義レスポンスヘッダオブジェクト領域                |
| headers[{HeaderName}] | Object | 必須 | なし | なし | ユーザー定義レスポンスヘッダのMap Entry(Key：ヘッダ名、 Value：ヘッダ値) |
| body                  | String | 任意 | なし | なし | ユーザー定義レスポンス本文                       |

<a id="cors"></a>
### CORS { #cors }
- Cross-Site方式内でXMLHttpRequest APIを呼び出せるようにします。
- リソースパスにのみ設定できます。
- CORSプラグインが設定されたパス下位にはOPTIONSメソッドが自動的に作成され、登録されたOPTIONSメソッドがある場合、置き換えられます。
```json
{
  "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
  "allowedHeaders": ["*"],
  "allowedOrigins": ["*"],
  "exposedHeaders": ["X-NHN-HEADER"],
  "maxCredentialsAge": 60,
  "allowCredentials": false
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| allowedMethods | List | 必須 | なし | なし | リソースへのアクセスを許可するメソッドリスト領域 |
| allowedMethods[0] | Enum | 必須 | なし | "GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH" | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| allowedHeaders | List | 必須 | なし | なし | リクエストで使用できるHTTPヘッダリスト領域 |
| allowedHeaders[0] | String | 必須 | なし | なし | リクエストで使用できるHTTPヘッダ(例：ワイルドカード形式： '\*'または'X-NHN-HEADER, Content-Type') |
| allowedOrigins    | List | 必須 | なし | なし | リソースにアクセスできるオリジンサーバーのドメインリスト領域 |
| allowedOrigins[0] | String | 必須 | なし | なし | リソースにアクセスできるオリジンサーバーのドメイン(例：ワイルドカード形式：'\*'または') |
| exposedHeaders    | List | 任意 | なし | なし | ブラウザ(クライアント)がアクセスできるヘッダリスト領域 |
| exposedHeaders[0] | String | 必須 | なし | なし |ブラウザ(クライアント)がアクセスできるヘッダ |
| maxCredentialsAge | Integer | 任意 | なし | -1～86400 |事前伝達リクエスト(Preflight)に対するレスポンスブラウザキャッシュ時間(秒単位) |
| allowCredentials  | Boolean | 必須 | なし |true/false | 資格情報でリクエストするかどうか |



<a id="setrequestheader"></a>
### SET_REQUEST_HEADER { #setrequestheader }
- リクエストヘッダを追加または変更します。 
- リソースパス、メソッドに設定できます。
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| headers | Map | 必須 | なし | なし | 追加/変更するリクエストヘッダオブジェクト領域 |
| headers[{HeaderName}] | Object | 必須 | なし | なし | 追加及び変更するリクエストヘッダのMap Entry(Key：ヘッダ名、 Value：ヘッダ値) |

<a id="removerequestheader"></a>
### REMOVE_REQUEST_HEADER { #removerequestheader }
- リクエストヘッダを削除します。  
- リソースパス、メソッドに設定できます。
```json
{
  "headers": [ 
    "Remove-Header-Name1", 
    "Remove-Header-Name2"
  ]
  
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| headers | List | 必須 | なし | なし | 削除するリクエストヘッダリスト領域 |
| headers[0] | String | 必須 | なし | なし | 削除するリクエストヘッダ名 |

<a id="setresponseheader"></a>
### SET_RESPONSE_HEADER { #setresponseheader }
- レスポンスヘッダ変更プラグインはバックエンドレスポンスにヘッダを追加または変更します。 
- リソースパス、メソッドに設定できます。
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| headers | Map | 必須 | なし | なし | 追加/変更するレスポンスヘッダオブジェクト領域 |
| headers[{HeaderName}] | String | 必須 | なし | なし | オブジェクトプロパティキー/値を追加/変更するレスポンスヘッダの名前と値 |

<a id="removeresponseheader"></a>
### REMOVE_RESPONSE_HEADER { #removeresponseheader }
- レスポンスヘッダを削除します。  
- リソースパス、メソッドに設定できます。
```json
{
  "headers": [ 
    "Remove-Header-Name1", 
    "Remove-Header-Name2"
  ]
  
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| headers | List | 必須 | なし | なし | 削除するレスポンスヘッダリスト領域 |
| headers[0] | Object | 必須 | なし | なし | 追加及び変更するレスポンスヘッダのMap Entry(Key：ヘッダ名、 Value：ヘッダ値) |


<a id="addrequestqueryparameter"></a>
### ADD_REQUEST_QUERY_PARAMETER { #addrequestqueryparameter }
- バックエンドエンドポイントリクエストにクエリ文字列パラメータを追加します。
- リソースパス、メソッドに設定できます。
```json
{
  "parameters": {
    "queryName1": "queryValue1"
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| parameters | Map| 必須 | なし | なし | 追加するリクエストクエリ文字列パラメータオブジェクト領域 |
| parameters[{QueryName}] | Object | 必須 | なし | なし | 値を追加するリクエストクエリ文字列パラメータのMap Entry(Key：クエリ名前、 Value：クエリ値) |
<a id="resource-parameter"></a>
## リソースパラメータ { #resource-parameter }

<a id="list-resource-parameters"></a>
### リソースパラメータ照会 { #list-resource-parameters }
- リソースパラメータのリストを照会します。

<a id="list-resource-parameters-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId     | String | 必須  | なし | なし   | API GatewayリソースID |

<a id="list-resource-parameters-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "queryStringList": [
    {
      "name": "query1",
      "description": "This is a query1",
      "dataType": "STRING",
      "required": false,
      "isArray": false
    }
  ],
  "headerList": [
    {
      "name": "header1",
      "description": "This is a header1",
      "dataType": "STRING",
      "required": false,
      "isArray": null
    }
  ],
  "formDataList": [
    {
      "name": "formDataString",
      "description": "This is a formData String",
      "dataType": "STRING",
      "required": false,
      "isArray": false
    },
    {
      "name": "formDataFile",
      "description": "This is a formData File",
      "dataType": "FILE",
      "required": false,
      "isArray": false
    }
  ],
  "requestBody": {
    "name": "requestBody",
    "description": "This is a requestBody",
    "modelId": "{modelId}"
  },
  "contentTypeList": [
    "application/json"
  ]
}
```

</details>

| フィールド                           | タイプ    | 説明                                                 |
| ------------------------------ | ------- | ---------------------------------------------------- |
| queryStringList                | List    | クエリ文字列リスト領域                                       |
| queryStringList[0].name        | String  | クエリ文字列名                                          |
| queryStringList[0].description | String  | クエリ文字列の説明                                          |
| queryStringList[0].dataType    | Enum    | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考|
| queryStringList[0].required    | Boolean | クエリ文字列が必須かどうか                                        |
| queryStringList[0].isArray     | Boolean | クエリ文字列がArrayかどうか                                     |
| headerList                     | List    | ヘッダリスト領域                                           |
| headerList[0].name             | String  | ヘッダ名                                              |
| headerList[0].description      | String  | ヘッダの説明                                              |
| headerList[0].dataType         | Enum    | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考 |
| headerList[0].required         | Boolean | ヘッダ必須かどうか                                            |
| headerList[0].isArray          | null    | ヘッダArrayかどうか未提供                                    |
| formDataList                   | List    | フォームデータリスト領域                                        |
| formDataList[0].name           | String  | フォームデータ名                                           |
| formDataList[0].description    | String  | フォームデータの説明                                           |
| formDataList[0].dataType       | Enum    | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考 |
| formDataList[0].required       | Boolean | フォームデータ必須かどうか                                         |
| formDataList[0].isArray        | Boolean | フォームデータArrayかどうか                                      |
| requestBody                    | Object  | リクエスト本文領域                                           |
| requestBody.name               | String  | リクエスト本文の名前                                           |
| requestBody.description        | String  | リクエスト本文の説明                                           |
| requestBody.modelId            | String  | リクエスト本文に関連付けられているモデルID                                     |
| contentTypeList                | List    | コンテンツタイプリスト領域                                       |
| contentTypeList[0]             | String  | コンテンツタイプ                                             |



<a id="create-resource-parameters"></a>
### リソースパラメータの作成 { #create-resource-parameters }
- リソースメソッドのパラメータを作成します。
- 既存リソースパラメータは削除され、リクエストされたリソースパラメータが作成されます。 

<a id="create-resource-parameters-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId     | String | 必須  | なし | なし   | API GatewayリソースID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "queryStringList": [
    {
      "name": "query1",
      "description": "This is a query1",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "headerList": [
    {
      "name": "header1",
      "description": "This is a header1",
      "dataType": "BOOLEAN",
      "required": true
    }
  ],
  "formDataList": [
    {
      "name": "formDataString",
      "description": "This is a formDataString",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "requestBody": {
    "name": "requestBody",
    "description": "This is a requestBody",
    "modelId": "{modelId}"
  },
  "contentTypeList": [
    "application/json"
  ]
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| queryStringList                | List    | 任意  | Empty List    | 最大50個                                            | クエリ文字列リスト領域                                       |
| queryStringList[0].name        | String  | 必須  | なし          | 最大50文字                                            | クエリ文字列名                                          |
| queryStringList[0].description | String  | 任意  | なし          | 最大200文字                                           | クエリ文字列の説明                                          |
| queryStringList[0].dataType    | Enum    | 必須  | なし          | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考|
| queryStringList[0].required    | Boolean | 必須  | なし          | true, false                                          | クエリ文字列必須かどうか                                        |
| queryStringList[0].isArray     | Boolean | 必須  | なし          | true, false                                          | クエリ文字列Arrayかどうか                                     |
| headerList                     | List    | 任意  | Empty List    | 最大50個                                            | ヘッダリスト領域                                           |
| headerList[0].name             | String  | 必須  | なし          | 最大50文字                                            | ヘッダ名                                              |
| headerList[0].description      | String  | 任意  | なし          | 最大200文字                                           | ヘッダ説明                                              |
| headerList[0].dataType         | Enum    | 必須  | なし          | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考|
| headerList[0].required         | Boolean | 必須  | なし          | true, false                                          | ヘッダ必須かどうか                                            |
| formDataList                   | List    | 任意  | Empty List    | 最大50個                                            | フォームデータリスト領域                                        |
| formDataList[0].name           | String  | 必須  | なし          | 最大50文字                                            | フォームデータ名                                           |
| formDataList[0].description    | String  | 任意  | なし          | 最大200文字                                           | フォームデータの説明                                           |
| formDataList[0].dataType       | Enum    | 必須  | なし          | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE, FILE  | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考|
| formDataList[0].required       | Boolean | 必須  | なし          | true, false                                          | フォームデータ必須かどうか                                         |
| formDataList[0].isArray        | Boolean | 必須  | なし          | true, false                                          | フォームデータArrayかどうか。 dataTypeがFILEの場合はfalse。            |
| requestBody                    | Object  | 任意  | Empty Object  | なし                                                 | リクエスト本文オブジェクト領域                                        |
| requestBody.name               | String  | 必須  | なし          | 最大50文字                                            | リクエスト本文の名前                                           |
| requestBody.description        | String  | 任意  | なし          | 最大200文字                                           | リクエスト本文の説明                                           |
| requestBody.modelId            | String  | 必須  | なし          | なし                                                 | リクエスト本文に関連付けられているモデルID                                    |
| contentTypeList                | List    | 任意  | Empty List    | 最大10個                                            | コンテンツタイプリスト領域                                       |
| contentTypeList[0]             | String  | 必須  | なし          | \*/\* 形式                                           | コンテンツタイプ                                             |

<a id="create-resource-parameters-response"></a>
#### レスポンス

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<a id="resource-response"></a>
## リソースレスポンス { #resource-response }

<a id="get-resource-response"></a>
### リソースレスポンス照会 { #get-resource-response }
- HTTPレスポンスステータスコード別ヘッダとリクエスト本文項目とコンテンツタイプを照会します。

<a id="get-resource-response-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId     | String | 必須  | なし | なし   | API GatewayリソースID |

<a id="get-resource-response-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "responseList": [
    {
      "responseStatusCode": 200,
      "description": "HTTP Status 200",
      "headerList": [
        {
          "name": "header1",
          "description": "This is a response header1",
          "dataType": "STRING"
        }
      ],
      "responseBody": {
        "name": "responseBody",
        "description": "This is a responseBody",
        "modelId": "{modelId}"
      }
    }
  ],
  "contentTypeList": [
    "application/json"
  ]
}
```

</details>

| フィールド                                      | タイプ    | 説明                                                 |
| ----------------------------------------- | ------- | ---------------------------------------------------- |
| responseList                              | List    | HTTPレスポンスステータスコード別レスポンス情報リスト領域                         |
| responseList[0].responseStatusCode        | Integer | HTTPレスポンスステータスコード                                      |
| responseList[0].description               | String  | HTTPレスポンスステータスコードの説明                                   |
| responseList[0].headerList                | List    | HTTPレスポンスヘッダリスト領域                                   |
| responseList[0].headerList[0].name        | String  | レスポンスヘッダ名                                           |
| responseList[0].headerList[0].description | String  | レスポンスヘッダの説明                                           |
| responseList[0].headerList[0].dataType    | Enum    | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考|
| responseList[0].responseBody              | Object  | HTTPレスポンス本文オブジェクト領域                                   |
| responseList[0].responseBody.name         | String  | レスポンス本文の名前                                           |
| responseList[0].responseBody.description  | String  | レスポンス本文の説明                                           |
| responseList[0].responseBody.modelId      | String  | レスポンス本文に関連付けられているモデルID                                     |
| contentTypeList                           | List    | コンテンツタイプリスト領域                                       |
| contentTypeList[0]                        | String  | コンテンツタイプ                                             |


<a id="create-resource-responses"></a>
### リソースレスポンスの作成 { #create-resource-responses }
- 既存リソースレスポンスは削除され、リクエストしたHTTPレスポンスステータスコード別ヘッダとリクエスト本文項目とコンテンツタイプを作成します。

<a id="create-resource-responses-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| 名前           | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明               |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 必須  | なし | なし   | API GatewayサービスID |
| resourceId     | String | 必須  | なし | なし   | API GatewayリソースID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "responseList": [
    {
      "responseStatusCode": 200,
      "description": "HTTP Status 200",
      "headerList": [
        {
          "name": "header1",
          "description": "This is a response header1",
          "dataType": "STRING",
        }
      ],
      "requestBody": {
        "name": "responseBody",
        "description": "This is a response body",
        "modelId": "{modelId}"
      }
    }
  ],
  "contentTypeList": [
    "application/json"
  ]
}
```

</details>

| 名前                                      | タイプ    | 必須かどうか | デフォルト値        | 有効範囲                                       | 説明                                                 |
| ----------------------------------------- | ------- | ----- | ------------ | --------------------------------------------- | ---------------------------------------------------- |
| responseList                              | List    | 任意  | Empty List   | なし                                           | HTTPレスポンスステータスコード別レスポンス情報リスト領域                         |
| responseList[0].responseStatusCode        | Integer | 必須  | なし          | 100～599                                       | HTTPレスポンスステータスコード                                      |
| responseList[0].description               | String  | 任意  | なし        | 最大200文字                                     | HTTPレスポンスステータスコードの説明                                   |
| responseList[0].headerList                | List    | 任意  | Empty List   | 最大50個                                      | HTTPレスポンスヘッダリスト領域                                   |
| responseList[0].headerList[0].name        | String  | 必須  | なし          | 最大50文字                                      | レスポンスヘッダ名                                           |
| responseList[0].headerList[0].description | String  | 任意  | なし        | 最大200文字                                     | レスポンスヘッダの説明                                           |
| responseList[0].headerList[0].dataType    | Enum    | 必須  | なし          | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE | [リソースリクエスト/レスポンスパラメータデータ型Enumコード](./enum-code/#resource-requestresponse-parameter-data-type)参考 |
| responseList[0].responseBody              | Object  | 任意  | Empty Object | なし                                           | HTTPレスポンス本文オブジェクト領域                                   |
| responseList[0].responseBody.name         | String  | 必須  | なし          | 最大50文字                                      | レスポンス本文名                                           |
| responseList[0].responseBody.description  | String  | 任意  | なし        | 最大200文字                                     | レスポンス本文の説明                                           |
| responseList[0].responseBody.modelId      | String  | 必須  | なし          | なし                                          | レスポンス本文に関連付けられているモデルID                                     |
| contentTypeList                           | List    | 任意  | Empty List   | 最大10個                                      | コンテンツタイプリスト領域                                       |
| contentTypeList[0]                        | String  | 必須  | なし          | \*/\* 形式                                      | コンテンツタイプ                                             |


<a id="create-resource-responses-response"></a>
#### レスポンス

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<a id="model"></a>
## モデル { #model }

<a id="list-models"></a>
### モデルリスト照会 { #list-models }
- モデルリストを照会します。

<a id="list-models-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |
| modelName | String | 任意 | なし | 最大50文字 | モデル名フィルタ条件。モデル名の文字列を含める必要があります。|

<a id="list-models-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "modelList": [
    {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 128
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:47.000Z"
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | ページング領域                                      |
|paging.page                          |Integer | 現在のページ                                      |
|paging.limit                         |Integer | ページあたりの件数                                 |
|paging.totalCount                    |Integer | 総件数                                       |
|modelList                     |List    | モデルリスト領域                       |
|modelList[0].apigwServiceId  |String  |API GatewayサービスID |
|modelList[0].modelId         |String  |モデルID              |
|modelList[0].modelName       |String  |モデル名            |
|modelList[0].modelDescription|String  |モデル説明            |
|modelList[0].modelSchema     |Object  |モデルの[JSON Schema](https://json-schema.org/) draft-04 JSONオブジェクト |
|modelList[0].createdAt       |DateTime|モデル作成日時          |
|modelList[0].updatedAt       |DateTime|モデル修正日時          |



<a id="create-model"></a>
### モデルの作成 { #create-model }
- モデルをJSON Schema形式で作成します。
- モデル名は重複してはいけません。

<a id="create-model-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "modelName": "UserModel",
  "modelDescription": "This is a user model.",
  "modelSchema": {
    "type": "object",
    "properties": {
      "userName": {
        "type": "string"
      },
      "userDescription": {
        "description": "user description",
        "type": "string",
        "maxLength": 128
      }
    },
    "required": [
      "userName"
    ]
  }
}
```

</details>

| 名前             | タイプ   | 必須かどうか | デフォルト値 | 有効範囲 | 説明                                                         |
| ---------------- | ------ | ----- | --- | ------- | ------------------------------------------------------------ |
| modelName        | String | 必須  | なし | 最大50文字 | モデル名                                                      |
| modelDescription | String | 任意  | なし | 最大200文字 | モデル説明                                                      |
| modelSchema      | Object | 必須  | なし | 最大65535文字| モデルの[JSON Schema](https://json-schema.org/) draft-04 JSONオブジェクト |

<a id="create-model-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 128
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:47.000Z"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | モデル領域                       |
|model.apigwServiceId  |String  |API GatewayサービスID |
|model.modelId         |String  |モデルID              |
|model.modelName       |String  |モデル名            |
|model.modelDescription|String  |モデル説明            |
|model.modelSchema     |Object  |モデルの[JSON Schema](https://json-schema.org/) draft-04 JSONオブジェクト |
|model.createdAt       |DateTime|モデル作成日時          |
|model.updatedAt       |DateTime|モデル修正日時          |


<a id="modify-model"></a>
### モデルの修正 { #modify-model }
- モデルの説明とスキーマを修正します。 
- モデル名は変更できません。 

<a id="modify-model-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| modelId | String | 必須 | なし | なし | モデルID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "modelDescription": "This is user model.",
  "modelSchema": {
    "type": "object",
    "properties": {
      "userName": {
        "type": "string"
      },
      "userDescription": {
        "description": "user description",
        "type": "string",
        "maxLength": 256
      }
    },
    "required": [
      "userName"
    ]
  }
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| modelDescription | String | 任意  | なし | 最大200文字 | モデル説明                                                      |
| modelSchema      | Object | 必須  | なし | 最大65535文字| モデルの[JSON Schema](https://json-schema.org/) draft-04 JSONオブジェクト |


<a id="modify-model-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 256
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:50.000Z"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | モデル領域                       |
|model.apigwServiceId  |String  |API GatewayサービスID |
|model.modelId         |String  |モデルID              |
|model.modelName       |String  |モデル名            |
|model.modelDescription|String  |モデル説明            |
|model.modelSchema     |Object  |モデルの[JSON Schema](https://json-schema.org/) draft-04 JSONオブジェクト |
|model.createdAt       |DateTime|モデル作成日時          |
|model.updatedAt       |DateTime|モデル修正日時          |


<a id="delete-model"></a>
### モデルの削除 { #delete-model }
- モデルを削除します。
- モデルがリソースのリクエストパラメータまたはレスポンスで参照されている場合にはモデルの削除ができません。参照を解除してからモデルを削除してください。

<a id="delete-model-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| modelId | String | 必須 | なし | なし | モデルID |

<a id="delete-model-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

</details>

<a id="stage"></a>
## ステージ { #stage }

<a id="list-stages"></a>
### ステージリスト照会 { #list-stages }
- ステージリストを照会します。

<a id="list-stages-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

<a id="list-stages-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "stageList": [
    {
      "stageId": "{stageId}",
      "apigwServiceId": "{apigwServiceId}",
      "regionCode": "KR1",
      "stageName": "alpha",
      "stageDescription": "alpha環境ステージ",
      "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "backendEndpointUrl": "https://backend.com",
      "resourceUpdatedAt": "2021-10-20T06:43:26.000Z",
      "createdAt": "2021-10-20T06:43:26.000Z",
      "updatedAt": "2021-10-20T06:43:26.000Z"
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | ページング領域                                      |
|paging.page                          |Integer | 現在のページ                                      |
|paging.limit                         |Integer | ページあたりの件数                                 |
|paging.totalCount                    |Integer | 総件数                                       |
|stageList        |List    | ステージリスト領域 |
|stageList[0].regionCode       |Enum    |[API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考              |
|stageList[0].apigwServiceId   |String  |API GatewayサービスID  |
|stageList[0].stageId          |String  |ステージID             |
|stageList[0].stageName        |String  |ステージ名           |
|stageList[0].stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
|stageList[0].stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
|stageList[0].stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
|stageList[0].stageAliasDomainList[0].createdAt   |DateTime  |ドメインエイリアス接続日時  |
|stageList[0].stageDescription |String  |ステージの説明           |
|stageList[0].backendEndpointUrl|String  |バックエンドエンドポイントURL       |
|stageList[0].resourceUpdatedAt|DateTime|最近ステージにリソースをインポートした日時 |
|stageList[0].createdAt        |DateTime|ステージ作成日時         |
|stageList[0].updatedAt        |DateTime|ステージ修正日時         |


<a id="swagger-export"></a>
### Swagger Export { #swagger-export }
- Swagger文書を照会します。 
- Swagger文書はAPI Gatewayに配布された設定ではなく、現在のステージ設定に基づいて抽出されます。

<a id="swagger-export-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/swagger |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

<a id="swagger-export-response"></a>
#### レスポンス

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "string"
  },
  "swaggerData": "{swaggerJson}"
}
```

|フィールド                                |タイプ   |説明                                         |
|-------------------------------------|--------|----------------------------------------------|
|swaggerData        |Object    | 現在ステージ基準Swagger JSONオブジェクト。 [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/)参考。 |


<a id="create-stage"></a>
### ステージの作成 { #create-stage }
- ステージを作成します。 

<a id="create-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "stageName": "alpha",
  "stageDescription": "alpha環境ステージ",
  "backendEndpointUrl": "https://backend.com"
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| stageName | String | 条件付き必須 | なし | 最大30文字、英小文字と数字のみ | ステージ名<br/>基本ステージではない場合は必須値です。  |
| stageDescription | String | 任意 | なし | 最大200文字 | ステージの説明 |
| backendEndpointUrl | String | 必須 | なし | 最大150文字、 URL形式 | バックエンドエンドポイントURL |

- stageNameフィールドの値は唯一でなければなりません。
- stageName(ステージ名)フィールドをnullに設定すると、基本ステージとして作成されます。基本ステージは1つだけ作成できます。 
- stageNameフィールドの値に応じてステージURLが変更されます。
    - ステージURLフォーマット：{regionCode}-{apigwServiceId}-{stageName}.api.nhncloudservice.com



<a id="create-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stage": {
    "stageId": "{stageId}",
    "apigwServiceId": "{apigwServiceId}",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alpha環境ステージ",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomDomainList": [],
    "backendEndpointUrl": "https://backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createddAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | ステージ領域 |
|stage.regionCode       |Enum    |[API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考              |
|stage.apigwServiceId   |String  |API GatewayサービスID  |
|stage.stageId          |String  |ステージID             |
|stage.stageName        |String  |ステージ名           |
|stage.stageUrl         |String  |ステージURL            |
|stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
|stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
|stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
|stage.stageDescription |String  |ステージの説明           |
|stage.backendEndpointUrl      |String  |バックエンドエンドポイントURL       |
|stage.resourceUpdatedAt|DateTime|最近ステージにリソースをインポートした日時 |
|stage.createdAt        |DateTime|ステージ作成日時         |
|stage.updatedAt        |DateTime|ステージ修正日時         |

<a id="modify-stage"></a>
### ステージの修正 { #modify-stage }
- ステージのバックエンドエンドポイントURLと説明を修正できます。
- ステージ名は変更できません。

<a id="modify-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "backendEndpointUrl": "https://v2.backend.com",
  "stageDescription": "alphaステージv2"
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| backendEndpointUrl | String | 必須 | なし | 最大150文字、 URL形式 | バックエンドエンドポイントURL |
| stageDescription | String | 任意 | なし | 最大200文字 | ステージの説明 |


<a id="modify-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stage": {
    "stageId": "{stageId}",
    "apigwServiceId": "{apigwServiceId}",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alphaステージv2",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomDomainList": [],
    "backendEndpointUrl": "https://v2.backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createdAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | ステージ領域 |
|stage.regionCode       |Enum    |[API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考              |
|stage.apigwServiceId   |String  |API GatewayサービスID  |
|stage.stageId          |String  |ステージID             |
|stage.stageName        |String  |ステージ名           |
|stage.stageUrl         |String  |ステージURL            |
|stage.stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
|stage.stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
|stage.stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
|stage.stageDescription |String  |ステージの説明           |
|stage.backendEndpointUrl      |String  |バックエンドエンドポイントURL       |
|stage.resourceUpdatedAt|DateTime|最近ステージにリソースをインポートした日時 |
|stage.createdAt        |DateTime|ステージ作成日時         |
|stage.updatedAt        |DateTime|ステージ修正日時         |


<a id="delete-stage"></a>
### ステージの削除 { #delete-stage }
- ステージを削除します。
- 削除しようとしているステージが使用量プランと関連付けられている場合は削除できません。使用量プランからステージの関連付けを削除してから削除してください。
- 削除されたステージは回復できません。

<a id="delete-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

<a id="delete-stage-response"></a>
#### レスポンス

[Response Body]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


<a id="list-stage-resources"></a>
### ステージリソースリストの照会 { #list-stage-resources }
* ステージに登録されたリソースリストを取得します。各リソースに設定されたステージリソースプラグイン情報が含まれます。
* ステージリソースプラグインの詳細については[ステージリソースプラグイン](./api-guide-v1.0/#stage-resource-plugin)を参照します。


<a id="list-stage-resources-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                  |
| ---- | ------------------------------------ |
| GET  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |


<a id="list-stage-resources-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |ステージリソースリスト領域                           |
|stageResourceList[0]      |Object    |ステージリソース領域                           |
|stageResourceList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].path                   |String  |ステージリソースパス                              |
|stageResourceList[0].parentPath             |String  |ステージ上位リソースパス(ルート(/)パスのparentPathはnull)|
|stageResourceList[0].stageId                |String  |ステージID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |バックエンドエンドポイント再定義URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
|stageResourceList[0].methodName             |String  |メソッド名                                   |
|stageResourceList[0].methodDescription      |String  |メソッドの説明                                   |
|stageResourceList[0].createdAt              |DateTime|ステージリソースの作成日時                            |
|stageResourceList[0].updatedAt              |DateTime|ステージリソースの修正日時                            |
|stageResourceList[0].stageResourcePluginList|List    |ステージリソースのプラグインリスト領域                     |
|stageResourceList[0].stageResourcePluginList[0]|Object    |ステージリソースのプラグイン領域                     |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |ステージリソースプラグインID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type), [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)参考                      |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin), [ステージプラグインタイプ](./api-guide-v1.0/#stage-resource-plugin)別設定JSON参考          |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|ステージリソースプラグインの作成日時                       |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|ステージリソースプラグインの修正日時                       |



<a id="import-resources-to-stage"></a>
### ステージにリソースをインポートする { #import-resources-to-stage }
* API Gatewayサービス > リソースをステージにインポートします。
* リソースをインポートすると、ステージリソース、ステージリソースプラグインは全て新しく作成されます。 
* 既存のリソースパス、メソッドに設定されたステージリソースプラグインの設定値はそのまま維持されます。 
* リソースに変更された事項がない場合は、実行されません。

<a id="import-resources-to-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |


<a id="import-resources-to-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |ステージリソースリスト領域                           |
|stageResourceList[0]      |Object    |ステージリソース領域                           |
|stageResourceList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].path                   |String  |ステージリソースパス                              |
|stageResourceList[0].parentPath             |String  |ステージ上位リソースパス(ルート(/)パスのparentPathはnull)|
|stageResourceList[0].stageId                |String  |ステージID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |バックエンドエンドポイント再定義URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考             |
|stageResourceList[0].methodName             |String  |メソッド名                                   |
|stageResourceList[0].methodDescription      |String  |メソッドの説明                                   |
|stageResourceList[0].createdAt              |DateTime|ステージリソースの作成日時                            |
|stageResourceList[0].updatedAt              |DateTime|ステージリソースの修正日時                            |
|stageResourceList[0].stageResourcePluginList|List    |ステージリソースのプラグインリスト領域                     |
|stageResourceList[0].stageResourcePluginList[0]|Object    |ステージリソースのプラグイン領域                     |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |ステージリソースプラグインID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type), [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)参考                      |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin), [ステージプラグインタイプ](./api-guide-v1.0/#stage-resource-plugin)別設定JSON参考|
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|ステージリソースプラグインの作成日時                       |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|ステージリソースプラグインの修正日時                       |



<a id="modify-stage-resource"></a>
### ステージリソースの修正 { #modify-stage-resource }
* リソースパスまたはリソースメソッドに設定されたバックエンドエンドポイントURLを再定義し、ステージリソースプラグインを修正します。
* ステージリソースを修正すると、登録されたステージリソースプラグインは全て削除され、リクエストしたリソースプラグインのみ新しく登録されます。
* ステージリソースプラグインの詳細については[ステージリソースプラグイン](./api-guide-v1.0/#stage-resource-plugin)を参照してください。

<a id="modify-stage-resource-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources/{stageResourceId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |
| stageResourceId | String | 必須 | なし | なし | ステージリソースID |


[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "customBackendEndpointUrl": "http://custom.backendpoint.com",
  "stageResourcePluginList": [
    {
      "pluginConfigJson": {"isActive": true},
      "pluginType": "API_KEY"
    }
  ]
}
```

</details>

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| customBackendEndpointUrl | String | 任意 | なし | 最大150文字、 URL形式 | バックエンドエンドポイント再定義URL |
| stageResourcePluginList | List | 必須 | なし | なし | ステージリソースプラグインリスト領域 |
| stageResourcePluginList[0] | Object | 必須 | なし | なし | ステージリソースプラグイン別JSON形式のオブジェクト<br>[ステージリソースプラグイン](./api-guide-v1.0/#stage-resource-plugin)参考|

* customBackendEndpointUrlフィールドはルート(/)リソースパスには設定できません。


<a id="modify-stage-resource-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |ステージリソースリスト領域                           |
|stageResourceList[0]      |Object    |ステージリソース領域                           |
|stageResourceList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].path                   |String  |ステージリソースパス                              |
|stageResourceList[0].parentPath             |String  |ステージ上位リソースパス(ルート(/)パスのparentPathはnull)|
|stageResourceList[0].stageId                |String  |ステージID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |バックエンドエンドポイント再定義URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考             |
|stageResourceList[0].methodName             |String  |メソッド名                                   |
|stageResourceList[0].methodDescription      |String  |メソッドの説明                                   |
|stageResourceList[0].createdAt              |DateTime|ステージリソースの作成日時                            |
|stageResourceList[0].updatedAt              |DateTime|ステージリソースの修正日時                            |
|stageResourceList[0].stageResourcePluginList|List    |ステージリソースのプラグインリスト領域                     |
|stageResourceList[0].stageResourcePluginList[0]|Object    |ステージリソースのプラグイン領域                     |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |ステージリソースプラグインID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type), [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)参考                      |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin), [ステージプラグインタイプ](./api-guide-v1.0/#stage-resource-plugin)別設定JSON参考          |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|ステージリソースプラグインの作成日時                       |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|ステージリソースプラグインの修正日時                       |


<a id="stage-resource-plugin"></a>
## ステージリソースプラグイン { #stage-resource-plugin }
* ステージのリソースにはアクセス制限、認証、使用量制御などの機能をプラグイン形式で設定できます。 
* プラグインは上位で設定すると下位すべてのメソッドに一括適用され、サブパス/メソッドで再定義できます。 

* [例]：プラグイン設定の再定義
    ```
    /
      /members
        - GET
        - POST
    ```
    * 設定 
        1. ルート(/)リソースパスでリクエスト数制限を1秒あたり100個に制限
        2. POSTリソースメソッドにリクエスト数制限を1秒あたり10個に制限(再定義)
    * 動作結果 
        - GET /membersはルート(/)に設定されたリクエスト数制限の1秒あたり100個に制限が適用されます。
        - POST /membersはルート(/)に設定されたリクエスト数制限の1秒あたり100個制限が無視され、1秒あたり10個制限で適用されます。

* リソースに応じて設定可能なプラグイン

| リソースタイプ | 設定可能なプラグインリスト |
| --- | --- |
| ルート(/)リソースパス |IP ACL、認証(JWTまたはHMACのいずれか)、事前呼び出しAPI、リクエスト数制限、 API Key |
| リソースパス |バックエンドエンドポイントURL再定義、事前呼び出しAPI、API Key |
| リソースメソッド |バックエンドエンドポイントURL再定義、事前呼び出しAPI、リクエスト数制限、 API Key |


<a id="ip-acl"></a>
### IP ACL { #ip-acl }
* IP ACLを使用して指定されたクライアントIPのAPI Gatewayリクエストを許可/拒否できます。
* すべてのリソースパス、メソッドに設定できます。設定内容は下位すべてのリソースに適用されます。

```json
{
  "pluginType": "IP_ACL",
  "pluginConfigJson": {
    "isPermit": false,
    "ipAclList": [
      {
        "ipCidrAddress": "192.168.0.1",
        "description": "ip format"
      },
      {
        "ipCidrAddress": "192.168.0.0/24",
        "description": "cidr format"
      }
    ]
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | IP_ACL | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のうちIP_ACL参考 |
| pluginConfigJson | Object | 必須 | なし | なし | IP ACLプラグイン設定領域 |
| pluginConfigJson.isPermit | Boolean | 必須 | なし | true, false | falseに設定すると、設定されたIP/CIDRのリクエストを拒否し、trueに設定すると設定されたIP/CIDRのみリクエストを許可します。  |
| pluginConfigJson.ipAclList | List | 必須 | なし | 1～100個 | リクエストを許可/拒否するIPまたはCIDRリスト領域 |
| pluginConfigJson.ipAclList[0].ipCidrAddress | String | 必須 | なし | IPまたはCIDR形式 | IPまたはCIDRを設定します。 |
| pluginConfigJson.ipAclList[0].description | String | 任意 | なし | 最大200文字 | 説明を設定します。 |


<a id="hmac"></a>
### HMAC { #hmac }
* HMAC署名検証を通じてクライアントリクエストの改ざんを検証するための設定です。 
* ルート(/)リソースパスにのみ設定できます。設定内容は下位すべてのリソースに適用されます。
* HMAC認証はJWT認証と同時に設定できません。
* 署名に使用する秘密鍵を設定します。
* 時間差で発生する検証失敗を防止するための検証有効時間を設定します。
* リクエストに必ず含める必要があるヘッダリストを設定します。

```json
{
  "pluginType": "HMAC",
  "pluginConfigJson": {
    "secretKey": "{secretKey}",
    "clockSkewSeconds": 0,
    "enforceHeaders": [
      "Authorization"
    ]
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | HMAC | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のHMAC参考 |
| pluginConfigJson | Object | 必須 | なし | なし | HMACプラグイン設定領域 |
| pluginConfigJson.secretKey | String | 必須 | なし | なし | 署名に使用される秘密鍵を設定します。32バイト以上の文字列に設定することを推奨します。|
| pluginConfigJson.clockSkewSeconds | Integer | 任意 | 0 | 0～86400 | リクエスト有効時間(単位：秒)を指定します。 |
| pluginConfigJson.enforceHeaders | Array | 任意 | Empty List | なし | 必須検証ヘッダの文字列配列を入力します。 |
| pluginConfigJson.enforceHeaders[0] | String | 必須 | なし | なし| 必須検証ヘッダの文字列 |


<a id="jwt"></a>
### JWT { #jwt }
* JWTトークンの署名とリクエストクレームを検証するための設定です。
* ルート(/)リソースパスにのみ設定できます。設定内容は下位すべてのリソースに適用されます。
* JWT認証はHMAC認証と同時に設定できません。
* 署名を検証するためのトークン暗号化アルゴリズムと暗号化アルゴリズム方式に基づく秘密鍵または公開鍵を設定します。
* リクエストクレームの値、必須かどうか、検証を行うためのクレーム検証条件を設定します。 
* 時間差で発生する検証失敗を防止するための検証有効時間を設定します。
* **暗号化アルゴリズムHS256** 
```json
{
  "pluginType": "JWT",
  "pluginConfigJson": {
    "encryptAlgorithm": "HS256",
    "hs256": {
      "secretKey": "{secretKey}"
    },
    "clockSkew": 0,
    "claimValidationCondition": {
      "iss": {
        "value": [],
        "dataType": "Array",
        "required": false,
        "validate": false
      },
      "aud": {
        "value": [],
        "dataType": "Array",
        "required": false,
        "validate": true
      },
      "sub": {
        "value": "",
        "dataType": "String",
        "required": false,
        "validate": false
      },
      "jti": {
        "value": "",
        "dataType": "String",
        "required": false,
        "validate": false
      },
      "exp": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      },
      "iat": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      },
      "nbf": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      }
    }
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | JWT | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のJWT参考 |
| pluginConfigJson | Object | 必須 | なし | なし | JWTプラグイン設定領域 |
| pluginConfigJson.encryptAlgorithm | Enum | 必須 | HS256 | HS256 | [JWT > 暗号化アルゴリズムEnumコード](./enum-code/#jwt-encryption-algorithm)参考 |
| pluginConfigJson.hs256 | Object | 必須 | なし | なし | HS256設定領域 |
| pluginConfigJson.hs256.secretKey | String | 必須 | なし | なし | 署名に使用される秘密鍵を設定します。32バイト以上の文字列に設定することを推奨します。|
| pluginConfigJson.clockSkew | Integer | 任意 | 0 | 0～86400 | exp, nbfクレームの検証有効時間(単位：秒)を指定します。 |
| pluginConfigJson.claimValidationCondition | Object | 任意 | Default Object | なし | クレーム検証条件領域 |
| pluginConfigJson.claimValidationCondition.iss | Object | 任意 | Default Object | なし | issクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.iss.value | Array | 必須 | Empty Array | なし |  issリクエストクレームの値のうち、許可するクレーム値を文字列配列で設定します。 |
| pluginConfigJson.claimValidationCondition.iss.value[0] | String | 任意 | なし | なし |  issリクエストクレームの値のうち、許可する文字列を設定します。 |
| pluginConfigJson.claimValidationCondition.iss.dataType | Enum | 任意 | Array | Array | issクレームのデータ型を設定します。 Arrayのみ有効です。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考 |
| pluginConfigJson.claimValidationCondition.iss.required | Boolean | 必須 | false | true, false | issリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.iss.validate | Boolean | 必須 | false | true, false | issリクエストクレーム値を検証するかどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.aud | Object | 任意 | Default Object | なし | audクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。  |
| pluginConfigJson.claimValidationCondition.aud.value | Array | 必須 | Empty Array | なし |  audリクエストクレームの値のうち、許可するクレーム値を文字列配列で設定します。 |
| pluginConfigJson.claimValidationCondition.aud.value[0] | String | 任意 | なし | なし |  audリクエストクレームの値のうち、許可する文字列を設定します。 |
| pluginConfigJson.claimValidationCondition.aud.dataType | Enum | 任意 | Array | Array | audクレームのデータ型を設定します。 Arrayのみ有効です。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考 |
| pluginConfigJson.claimValidationCondition.aud.required | Boolean | 必須 | false | true, false | audリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.aud.validate | Boolean | 必須 | true | true | audリクエストクレーム値を検証するかどうかを設定します。 trueのみ有効です。 |
| pluginConfigJson.claimValidationCondition.sub | Object | 任意 | Default Object | なし | subクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.sub.value | String | 必須 | Empty String | なし |  subリクエストクレームの値のうち、許可するクレーム文字列値を設定します。 |
| pluginConfigJson.claimValidationCondition.sub.dataType | Enum | 任意 | String | String | subクレームのデータ型を設定します。 Stringのみ有効です。<br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考|
| pluginConfigJson.claimValidationCondition.sub.required | Boolean | 必須 | false | true, false | subリクエストクレーム値が必須検証かどうかを設定します。 <br/> validateフィールド値がtrueの場合、 requriedは必ずtrueに設定する必要があります。  |
| pluginConfigJson.claimValidationCondition.sub.validate | Boolean | 必須 | false | true, false | subリクエストクレーム値を検証するかどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.jti | Object | 任意 | Default Object | なし | jtiクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.jti.value | String | 必須 | Empty String | なし | jtiクレームは許可する検証値設定を要求しないため、空の文字列に設定します。 |
| pluginConfigJson.claimValidationCondition.jti.dataType | Enum | 任意 | String | String | jtiクレームのデータ型を設定します。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考|
| pluginConfigJson.claimValidationCondition.jti.required | Boolean | 必須 | false | true, false | jtiリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.jti.validate | Boolean | 必須 | false | false | jtiリクエストクレーム値を検証するかどうかを設定します。 falseのみ有効です。|
| pluginConfigJson.claimValidationCondition.exp | Object | 任意 | Default Object | なし | expクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.exp.dataType | Enum | 任意 | NumericDate | NumericDate | expクレームのデータ型を設定します。 NumericDateのみ有効です。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考 |
| pluginConfigJson.claimValidationCondition.exp.required | Boolean | 必須 | false | true, false | expリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.exp.validate | Boolean | 任意 | true | true | expリクエストクレーム値を検証するかどうかを設定します。 trueのみ有効です。 |
| pluginConfigJson.claimValidationCondition.iat | Object | 任意 | Default Object | なし | iatクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.iat.dataType | Enum | 任意 | NumericDate | NumericDate | iatクレームのデータ型を設定します。 NumericDateのみ有効です。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考 |
| pluginConfigJson.claimValidationCondition.iat.required | Boolean | 必須 | false | true, false | iatリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.iat.validate | Boolean | 任意 | true | true | iatリクエストクレーム値を検証するかどうかを設定します。 trueのみ有効です。 |
| pluginConfigJson.claimValidationCondition.nbf | Object | 任意 | Default Object | なし | nbfクレーム検証条件領域。リクエストしない場合、各フィールドのデフォルト値で保存されます。 |
| pluginConfigJson.claimValidationCondition.nbf.dataType | Enum | 任意 | NumericDate | NumericDate | nbfクレームのデータ型を設定します。 NumericDateのみ有効です。 <br/> [JWT > クレームデータ型Enumコード](./enum-code/#jwt-claim-data-type)参考|
| pluginConfigJson.claimValidationCondition.nbf.required | Boolean | 必須 | false | true, false | nbfリクエストクレーム値が必須検証かどうかを設定します。 |
| pluginConfigJson.claimValidationCondition.nbf.validate | Boolean | 任意 | true | true | nbfリクエストクレーム値を検証するかどうかを設定します。 trueのみ有効です。 |


* **暗号化アルゴリズムRS256： (PEM形式の公開鍵設定方式)** 

```json
{
  "pluginType": "JWT",
  "pluginConfigJson": {
    "encryptAlgorithm": "RS256",
    "rs256": {
      "publicKeyType": "RSA_PUBLIC_KEY",
      "rsaPublicKey": "-----BEGIN PUBLIC KEY-----\n{publicPemKey}\n-----END PUBLIC KEY-----"
    },
    "clockSkew": 0,
    "claimValidationCondition": {
      ...
    }
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | JWT | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のJWT参考 |
| pluginConfigJson | Object | 必須 | なし | なし | JWTプラグイン設定領域 |
| pluginConfigJson.encryptAlgorithm | Enum | 必須 | RS256 | RS256 | [JWT > 暗号化アルゴリズムEnumコード](./enum-code/#jwt-encryption-algorithm)参考 |
| pluginConfigJson.rs256 | Object | 必須 | なし | なし | RS256設定領域 |
| pluginConfigJson.rs256.publicKeyType | Enum | 必須 | なし | RSA_PUBLIC_KEY | PEM形式の公開鍵設定[JWT > RS256暗号化アルゴリズム > Public Key TypeEnumコード](./enum-code/#jwt-rs256-encryption-algorithm-public-key-type)参考 |
| pluginConfigJson.rs256.rsaPublicKey | String | 必須 | なし | PEM形式の公開鍵 | PEM形式の公開鍵値を設定します。 改行文字(\n)を含めて入力する必要があります。 |
| pluginConfigJson.clockSkew | Integer | 任意 | 0 | 0～86400 | exp, nbfクレームの検証有効時間(単位：秒)を指定します。 |
| pluginConfigJson.claimValidationCondition | Object | 任意 | Default Object | なし | クレーム検証条件領域(暗号化アルゴリズム： HS256のclaimValidationConditionフィールド説明と同じです。) |


* **暗号化アルゴリズムRS256： (JSON Web Key Sets URI公開鍵設定方式)** 

```json
{
  "pluginType": "JWT",
    "pluginConfigJson": {
      "encryptAlgorithm": "RS256",
      "rs256": {
        "publicKeyType": "JWKS_URI",
        "jwksUri": "https://examp.com/.well-known/jwks.json"
      },
      "clockSkew": 0,
      "claimValidationCondition": {
        ...
    }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | JWT | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のJWT参考 |
| pluginConfigJson | Object | 必須 | なし | なし | JWTプラグイン設定領域 |
| pluginConfigJson.encryptAlgorithm | Enum | 必須 | RS256 | RS256 | [JWT > 暗号化アルゴリズムEnumコード](./enum-code/#jwt-encryption-algorithm)参考 |
| pluginConfigJson.rs256 | Object | 必須 | なし | なし | RS256設定領域 |
| pluginConfigJson.rs256.publicKeyType | String | 必須 | なし | JWKS_URI | JWKS(JSON Web Key Sets) URI形式で開鍵を設定します。 [JWT > RS256暗号化アルゴリズム > Public Key TypeEnumコード](./enum-code/#jwt-rs256-encryption-algorithm-public-key-type)参考 |
| pluginConfigJson.rs256.rsaPublicKey | String | 必須 | なし | なし | JSON Web Key Set URIを設定します。 |
| pluginConfigJson.clockSkew | Integer | 任意 | 0 | 0～86400 | exp, nbfクレームの検証有効時間(単位：秒)を指定します。 |
| pluginConfigJson.claimValidationCondition | Object | 任意 | Default Object | なし | クレーム検証条件領域(暗号化アルゴリズム： HS256のclaimValidationConditionフィールド説明と同じです。) |


<a id="pre-call-api"></a>
### 事前呼び出しAPI { #pre-call-api }
* 事前呼び出しAPIは、バックエンドエンドポイントを呼び出す前にユーザーが指定したAPIを呼び出して呼び出しのレスポンスコードが200 OKの場合にのみバックエンドエンドポイントを呼び出すようにします。
* すべてのリソースパス、メソッドに設定できます。 

```json
{
  "pluginType": "PRE_API",
  "pluginConfigJson": {
    "httpMethod": "POST",
    "url": "http://auth.check.com",
    "cacheTtl": 0
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | PRE_API | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のPRE_API参考 |
| pluginConfigJson | Object | 必須 | なし | なし | 事前呼び出しAPIプラグイン設定領域 |
| pluginConfigJson.httpMethod | Enum | 必須 | なし | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考 |
| pluginConfigJson.url | String | 必須 | なし | URL形式 | 事前呼び出しAPIのURLを入力します。 |
| pluginConfigJson.cacheTtl | Integer | 任意 | 0 | 0～86400 | 事前呼び出しAPIのレスポンスステータスコードのキャッシュ時間を設定します。 <br/>レスポンスステータスコードが200 OKの場合にのみ設定された時間キャッシュされ、キャッシュされている場合には事前呼び出しAPIを呼び出しません。 |


<a id="request-number-limit"></a>
### リクエスト数制限 { #request-number-limit }
* 1秒あたりのリクエスト数を制限します。 
* ルート(/)リソースパスとリソースメソッドに設定できます。 
* リクエスト制限キーを設定して、IP、ヘッダ、パス変数値ごとにリクエスト数制限を設定できます。

```json
{
  "pluginType": "RATE_LIMIT",
  "pluginConfigJson": {
    "requestPerSec": 100,
    "keyType": "DEFAULT",
    "extraKeyValue": null
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | RATE_LIMIT | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のRATE_LIMIT参考 |
| pluginConfigJson | Object | 必須 | なし | なし | リクエスト数制限プラグイン設定領域 |
| pluginConfigJson.keyType | Enum | 必須 | なし | DEFAULT, IP, HEADER, PATH_VARIABLE | [リクエスト数制限 > 制限キーEnumコード](./enum-code/#request-number-limit-limit-key)参考 |
| pluginConfigJson.extraKeyValue | String | 条件付き必須 | なし | なし | keyTypeがHEADERの場合、ヘッダ名を必ず設定する必要があります。<br/> keyTypeがPATH_VARIABLEの場合、 ${request.path.variable-name}形式のパス変数を必ず設定する必要があります。 |
| pluginConfigJson.requestPerSec | Integer | 必須 | なし | 1～5000 | 1秒あたりの最大リクエスト可能数を設定します。 |


<a id="api-key"></a>
### API Key { #api-key }

* APIの呼び出し時にAPI Keyの有効性を検証し、指定された使用量プランの使用量を超えているかを検証します。 
* ルート(/)リソースパスとリソースメソッドに設定できます。 


```json
{
  "pluginType": "API_KEY",
  "pluginConfigJson": {
    "isActive": true
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | API_KEY | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のAPI_KEY参考 |
| pluginConfigJson | Object | 必須 | なし | なし | API Keyプラグイン設定領域 |
| pluginConfigJson.isActive | Boolean | 必須 | なし | true | API Key検証を行うかどうかを設定します。必ずtrueに設定する必要があります。 |


<a id="request-validator"></a>
### リクエストバリデーター { #request-validator }

* リクエストパラメータで定義された設定に従ってクライアントのリクエストを検証します。
* 全てのリソースパス、メソッドに設定できます。設定内容は下位の全てのリソースに適用されます。


```json
{
  "pluginType": "REQUEST_VALIDATOR",
  "pluginConfigJson": {
    "isActive": true
  }
}
```

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 必須 | なし | REQUEST_VALIDATOR | [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)のうちREQUEST_VALIDATORを参照 |
| pluginConfigJson | Object | 必須 | なし | なし | リクエストバリデータープラグイン設定領域 |
| pluginConfigJson.isActive | Boolean | 必須 | なし | true | リクエストバリデーターを使用するかどうかを設定します。必ずtrueに設定する必要があります。 |

<a id="deploy-stage"></a>
## ステージ配布 { #deploy-stage }


<a id="deploy-stage-2"></a>
### ステージ配布 { #deploy-stage-2 }
- 現在のステージリソースと設定をAPI Gatewayサービスに配布します。 
- 変更された設定情報がない場合、ステージ配布リクエストが失敗します。
- ステージ配布が失敗した場合、既存の成功したステージ配布設定に戻ります。
- ステージ配布リクエスト後、ステージ配布成否は[最近のステージ配布結果照会](./api-guide-v1.0/#query-result-of-recent-stage-deployment)で確認できます。 

<a id="deploy-stage-2-request"></a>
#### リクエスト

[URI]

| メソッド  | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "deployDescription": "deploy description"
}
```

</details>
| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| deployDescription | String | 任意 | なし | 最大200文字 | 配布説明 |


<a id="deploy-stage-2-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

</details>


<a id="query-result-of-recent-stage-deployment"></a>
### 最近のステージ配布結果照会 { #query-result-of-recent-stage-deployment }
- [ステージ配布](./api-guide-v1.0/#deploy-stage)の結果を照会できます。
- ステージ配布リクエスト後に配布結果がアップデートされるまで最長1分ほどかかる場合があります。 


<a id="query-result-of-recent-stage-deployment-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/latest |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |


<a id="query-result-of-recent-stage-deployment-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "latestStageDeployResult": {
    "deployId": "{deployId}",
    "stageId": "{stageId}",
    "deployStatus": "COMPLETE",
    "deployDescription": "",
    "stageResourceList": [
        {
        "stageResourceId": "{stageResourceId}",
        "stageId": "{stageId}",
        "path": "/",
        "parentPath": null,
        "methodType": null,
        "methodName": null,
        "methodDescription": null,
        "customBackendEndpointUrl": null,
        "createdAt": "2021-10-22T04:43:14.000Z",
        "updatedAt": "2021-10-22T04:44:42.000Z",
        "stageResourcePluginList": [
            {
            "stageResourcePluginId": "{stageResourcePluginId}",
            "stageResourceId": "{stageResourceId}",
            "pluginType": "HMAC",
            "pluginConfigJson": {
                "secretKey": "hmac-secret-key",
                "clockSkewSeconds": 10,
                "enforceHeaders": []
            },
            "createdAt": "2021-10-22T04:44:42.000Z",
            "updatedAt": "2021-10-22T04:44:42.000Z"
            },
            {
            "stageResourcePluginId": "{stageResourcePluginId}",
            "stageResourceId": "{stageResourceId}",
            "pluginType": "RATE_LIMIT",
            "pluginConfigJson": {
                "requestPerSec": 10,
                "defaultKey": "kr1-{apigwServiceId}.api.nhncloudservice.com/:",
                "keyType": "DEFAULT",
                "extraKeyValue": null
            },
            "createdAt": "2021-10-22T04:44:42.000Z",
            "updatedAt": "2021-10-22T04:44:42.000Z"
            }
        ]
        }
    ],
    "isBase": false,
    "deployedAt": "2021-10-25T01:40:13.000Z",
    "rollbackAt": null
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|latestStageDeployResult              |Object  | ステージ配布結果領域                                      |
|latestStageDeployResult.deployId       |String    | 配布ID |
|latestStageDeployResult.stageId   |String  | ステージID  |
|latestStageDeployResult.deployDescription        |String  | 配布説明 |
|latestStageDeployResult.deployStatus        |Enum  | [ステージ配布 > 配布状態Enumコード](./enum-code/#stage-deployment-deployment-status)参考 |
|latestStageDeployResult.isBase         |String  | 現在のステージ設定のベースになる配布履歴かどうか |
|latestStageDeployResult.deployedAt          |DateTime  | 配布リクエスト日時 |
|latestStageDeployResult.rollbackAt   |DateTime  | ステージ復元リクエスト日時 |
|latestStageDeployResult.stageResourceList      |List    |ステージリソースリスト領域                           |
|latestStageDeployResult.stageResourceList[0]      |Object    |ステージリソース領域                           |
|latestStageDeployResult.stageResourceList[0].stageResourceId        |String  |ステージリソースID                                |
|latestStageDeployResult.stageResourceList[0].path                   |String  |ステージリソースパス                              |
|latestStageDeployResult.stageResourceList[0].parentPath             |String  |ステージ上位リソースパス(ルート(/)パスのparentPathはnull)|
|latestStageDeployResult.stageResourceList[0].stageId                |String  |ステージID                                    |
|latestStageDeployResult.stageResourceList[0].customBackendEndpointUrl      |String  |バックエンドエンドポイント再定義URL                          |
|latestStageDeployResult.stageResourceList[0].methodType             |Enum    |[HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考             |
|latestStageDeployResult.stageResourceList[0].methodName             |String  |メソッド名                                   |
|latestStageDeployResult.stageResourceList[0].methodDescription      |String  |メソッド説明                                   |
|latestStageDeployResult.stageResourceList[0].createdAt              |DateTime|ステージリソースの作成日時                            |
|latestStageDeployResult.stageResourceList[0].updatedAt              |DateTime|ステージリソースの修正日時                            |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList|List    |ステージリソースのプラグインリスト領域                     |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0]|Object    |ステージリソースのプラグイン領域                     |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |ステージリソースプラグインID                           |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |ステージリソースID                                |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type), [ステージリソース > プラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)参考                     |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin), [ステージプラグインタイプ](./api-guide-v1.0/#stage-resource-plugin)別設定JSON参考         |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|ステージリソースプラグインの作成日時                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|ステージリソースプラグインの修正日時                       |

<a id="delete-stage-deployment-history"></a>
### ステージ配布履歴の削除 { #delete-stage-deployment-history }
- ステージ配布履歴を削除します。
- 現在のステージのベース配布履歴(isBaseがtrueの場合)と現在API Gatewayサービスの配布履歴は削除できません。

<a id="delete-stage-deployment-history-request"></a>
#### リクエスト

[URI]

| メソッド  | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |
| deployId | String | 必須 | なし | なし | 削除する配布ID |

<a id="delete-stage-deployment-history-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

</details>


<a id="query-stage-deployment-history"></a>
### ステージ配布履歴の照会 { #query-stage-deployment-history }
- 配布成功状態のステージ配布履歴を照会します。 

<a id="query-stage-deployment-history-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

<a id="query-stage-deployment-history-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "stageDeployHistoryList": [
    {
      "deployId": "{deployId}",
      "stageId": "{stageId}",
      "deployedAt": "2021-10-25T01:58:34.000Z",
      "deployDescription": "",
      "isBase": true,
      "rollbackAt": null
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | ページング領域                                      |
|paging.page                          |Integer | 現在のページ                                      |
|paging.limit                         |Integer | ページあたりの件数                                 |
|paging.totalCount                    |Integer | 総件数                                       |
|stageDeployHistoryList        |List    | ステージ配布履歴リスト領域 |
|stageDeployHistoryList[0]        |Object    | ステージ配布履歴領域 |
|stageDeployHistoryList[0].deployId       |String    | 配布ID |
|stageDeployHistoryList[0].stageId   |String  | ステージID  |
|stageDeployHistoryList[0].deployDescription        |String  | 配布説明 |
|stageDeployHistoryList[0].isBase         |Boolean  | 現在のステージ設定のベースになる配布履歴かどうか |
|stageDeployHistoryList[0].deployedAt          |DateTime  | 配布リクエスト日時 |
|stageDeployHistoryList[0].rollbackAt   |DateTime  | ステージ復元リクエスト日時 |


<a id="rollback-stage"></a>
### ステージの復元 { #rollback-stage }
- 配布されたステージ設定履歴で現在のステージ設定を復元します。
- ステージを復元すると、現在のステージ設定は全て削除されますのでご注意ください。
- 復元されたステージ設定をAPI Gatewayサービスに適用するには、ステージを配布する必要があります。
- 配布失敗状態の配布履歴には復元できません。

<a id="rollback-stage-request"></a>
#### リクエスト

[URI]

| メソッド  | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId}/rollback |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |
| deployId | String | 必須 | なし | なし | 復元する配布ID |

<a id="rollback-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "resourceMethod": false,
      "resourcePath": true,
      "parentPath": null,
      "pathKey": "/",
      "rootPath": true,
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customEndpointUrl": null,
      "createdAt": "2021-10-25T08:23:41.139Z",
      "updatedAt": "2021-10-25T08:23:41.139Z",
      "stageResourcePluginList": []
    }
  ]
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |ステージリソースリスト領域                           |
|stageResourceList[0]      |Object    |ステージリソース領域                           |
|stageResourceList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].path                   |String  |ステージリソースパス                              |
|stageResourceList[0].parentPath             |String  |ステージ上位リソースパス(ルート(/)パスのparentPathはnull)|
|stageResourceList[0].stageId                |String  |ステージID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |バックエンドエンドポイント再定義URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考             |
|stageResourceList[0].methodName             |String  |メソッド名                                   |
|stageResourceList[0].methodDescription      |String  |メソッドの説明                                   |
|stageResourceList[0].createdAt              |DateTime|ステージリソースの作成日時                            |
|stageResourceList[0].updatedAt              |DateTime|ステージリソースの修正日時                            |
|stageResourceList[0].stageResourcePluginList|List    |ステージリソースのプラグインリスト領域                     |
|stageResourceList[0].stageResourcePluginList[0]|Object    |ステージリソースのプラグイン領域                     |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |ステージリソースプラグインID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |ステージリソースID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[リソースプラグインタイプEnumコード](./enum-code/#resource-plugin-type), [ステージプラグインタイプEnumコード](./enum-code/#stage-resource-plugin-type)参考                     |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[リソースプラグインタイプ](./api-guide-v1.0/#resource-plugin), [ステージプラグインタイプ](./api-guide-v1.0/#stage-resource-plugin)別設定JSON参考       |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|ステージリソースプラグインの作成日時                       |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|ステージリソースプラグインの修正日時                       |


<a id="gateway-response"></a>
## ゲートウェイレスポンス { #gateway-response }

<a id="get-a-list-of-gateway-responses"></a>
### ゲートウェイレスポンスリスト照会 { #get-a-list-of-gateway-responses }
- ユーザーが再定義したゲートウェイレスポンスリストを照会します。

<a id="get-a-list-of-gateway-responses-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/gateway-responses |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

<a id="get-a-list-of-gateway-responses-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "gatewayResponseList": [
    {
      "gatewayResponseId": "{gatewayResponseId}",
      "gatewayResponseType": "Unauthorized",
      "httpStatusCode": 401,
      "headers": { "test1": "test1" },
      "body": { "application/json": "{\"result\":\"fail\"}" },
      "createdAt": "2024-07-04T09:24:15.000Z",
      "updatedAt": "2024-07-04T09:24:15.000Z"
    }
  ]
}
```

</details>

| フィールド                            | タイプ     | 説明                                              |
| ------------------------------- | -------- | ------------------------------------------------- |
| gatewayResponseList                      | List     | ゲートウェイレスポンスリスト領域 |
| gatewayResponseList[0]                   | Object   | ゲートウェイレスポンス領域 |
| gatewayResponseList[0].gatewayResponseId  | String   | ゲートウェイレスポンスID |
| gatewayResponseList[0].gatewayResponseType | Enum   | [ゲートウェイレスポンスタイプEnumコード](./enum-code/#gateway-response-type)参考 |
| gatewayResponseList[0].httpStatusCode        | Integer   | ゲートウェイレスポンスHTTPステータスコード |
| gatewayResponseList[0].headers | Map   | ゲートウェイレスポンスヘッダオブジェクト領域 |
| gatewayResponseList[0].headers[{HeaderName}] | Object   | ゲートウェイレスポンスヘッダのMap Entry(Key：ゲートウェイレスポンスヘッダの名前、 Value：ヘッダ値) |
| gatewayResponseList[0].body     | Map   | ゲートウェイレスポンス本文オブジェクト領域 |
| gatewayResponseList[0].body[{ContentType}] | Object   | ゲートウェイレスポンス本文のMap Entry(Key： ContentType, Value：レスポンス本文) |
| gatewayResponseList[0].createdAt         | DateTime | ゲートウェイレスポンス作成日時                                    |
| gatewayResponseList[0].updatedAt         | DateTime | ゲートウェイレスポンス修正日時                                    |


<a id="redefine-gateway-response"></a>
### ゲートウェイレスポンス再定義 { #redefine-gateway-response }
- ゲートウェイレスポンスをユーザーが再定義します。

<a id="redefine-gateway-response-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/gateway-responses |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
    "gatewayResponseType": "NotFound",
    "httpStatusCode": 404,
    "headers": { "test1": "test1" },
    "body": { "application/json": "{\"result\":\"fail\"}" }
}
```

</details>

| 名前              | タイプ   | 必須かどうか | デフォルト値 | 有効範囲          | 説明                                              |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| gatewayResponseType        | Enum | 必須  | なし | [ゲートウェイレスポンスタイプEnumコード](./enum-code/#gateway-response-type) |  |
| httpStatusCode | Integer | 必須  | なし | 100~599 | ゲートウェイレスポンスHTTPステータスコード |
| headers      | Map   | 選択  | なし | なし | ユーザー定義レスポンスヘッダオブジェクト領域 |
| headers[{HeaderName}] | Object   | 必須  | なし | なし | ゲートウェイレスポンスヘッダのMap Entry(Key：ゲートウェイレスポンスヘッダの名前、 Value：ヘッダ値) |
| body      | Map   | 選択  | なし | なし | ゲートウェイレスポンス本文オブジェクト領域 |
| body[{ContentType}] | Object   | 必須  | なし | なし | ゲートウェイレスポンス本文のMap Entry(Key： ContentType, Value：レスポンス本文) |
<a id="redefine-gateway-response-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "gatewayResponse": {
        "gatewayResponseId": "{gatewayResponseId}",
        "gatewayResponseType": "NotFound",
        "httpStatusCode": 404,
        "headers": { "test1": "test1" },
        "body": { "application/json": "{\"result\":\"fail\"}" },
        "createdAt": "2024-07-05T00:24:37.000Z",
        "updatedAt": "2024-07-05T00:24:37.000Z"
    }
}
```

</details>


| フィールド                            | タイプ     | 説明                                              |
| ------------------------------- | -------- | ------------------------------------------------- |
| gatewayResponse                   | Object   | ゲートウェイレスポンス領域 |
| gatewayResponse.gatewayResponseId  | String   | ゲートウェイレスポンスID |
| gatewayResponse.gatewayResponseType | Enum   | [ゲートウェイレスポンスタイプEnumコード](./enum-code/#gateway-response-type)参考 |
| gatewayResponse.httpStatusCode        | Integer   | ゲートウェイレスポンスHTTPステータスコード |
| gatewayResponse.headers | Map   | ゲートウェイレスポンスヘッダオブジェクト領域 |
| gatewayResponse.headers[{HeaderName}] | Object   | ゲートウェイレスポンスヘッダのMap Entry(Key：ヘッダ名、 Value：ヘッダ値) |
| gatewayResponse.body     | Map   | ゲートウェイレスポンス本文オブジェクト領域 |
| gatewayResponse.body[{ContentType}]     | Object   | ゲートウェイレスポンス本文のMap Entry(Key： ContentType, Value：レスポンス本文) |
| gatewayResponse.createdAt         | DateTime | ゲートウェイレスポンス作成日時                                    |
| gatewayResponse.updatedAt         | DateTime | ゲートウェイレスポンス修正日時                                    |


<a id="reset-gateway-response"></a>
### ゲートウェイレスポンス初期化 { #reset-gateway-response }
- ゲートウェイレスポンスを基本レスポンスで初期化します。

<a id="reset-gateway-response-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/gateway-responses/{gatewayResponseId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| gatewayResponseId | String | 必須 | なし | なし | ゲートウェイレスポンスID |

<a id="reset-gateway-response-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

</details>


<a id="api-document"></a>
## API説明書 { #api-document }

<a id="query-api-document"></a>
### API説明書照会 { #query-api-document }
- 配布されたステージ設定基準でAPI説明書を照会します。 
- API説明書は[Swagger v2.0](https://swagger.io/specification/v2/)仕様のJSONオブジェクトでレスポンスされます。
- 配布されていないステージについてはAPI説明書を照会できず、404 Not Foundが返されます。


<a id="query-api-document-request"></a>
#### リクエスト

[URI]

| メソッド  | URI                                 |
| ------ | ------------------------------------ |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/documents/swagger |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

<a id="query-api-document-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "swagger": "2.0",
  "info": {
    "version": "2021-10-26T15:21:22.163+09:00",
    "title": "alpha"
  },
  "host": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
  "schemes": [
    "https",
    "http"
  ],
  "paths": {
    "/members/{proxy+}": {
      "get": {
        "summary": "会員API",
        "description": "",
        "consumes": [
          "application/json"
        ],
        "produces": [
          "application/xml",
          "application/json"
        ],
        "parameters": [
          {
            "name": "proxy+",
            "in": "path",
            "description": "proxy+",
            "required": true,
            "type": "string"
          },
          {
            "name": "memberId",
            "in": "query",
            "description": "member id",
            "required": false,
            "type": "string"
          },
          {
            "name": "x-request-id",
            "in": "header",
            "description": "リクエストID",
            "required": false,
            "type": "string"
          },
          {
            "in": "body",
            "name": "Member",
            "description": "会員オブジェクト",
            "required": false,
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "照会成功レスポンス",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "レスポンスID"
              }
            },
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "#/definitions/MemberModel"
            },
            "responseSchema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          },
          "404": {
            "description": "存在しない会員",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "レスポンスID"
              }
            }
          }
        },
        "security": [
          {
            "x-nhncloud-jwt": [
              
            ],
            "x-nhncloud-apikey": [
              
            ]
          }
        ],
        "x-nhncloud-apigateway": {
          "plugins": {
            "HTTP": {
              "frontendEndpointPath": "/members/{proxy+}",
              "backendEndpointPath": "/anything/${request.path.proxy+}"
            }
          }
        }
      },
      "post": {
        "summary": "会員API",
        "description": "",
        "parameters": [
          {
            "name": "proxy+",
            "in": "path",
            "description": "proxy+",
            "required": true,
            "type": "string"
          }
        ],
        "responses": {
          "200": {
            "description": "default response"
          }
        },
        "security": [
          {
            "x-nhncloud-jwt": [
              
            ],
            "x-nhncloud-apikey": [
              
            ]
          }
        ],
        "x-nhncloud-apigateway": {
          "plugins": {
            "HTTP": {
              "frontendEndpointPath": "/members/{proxy+}",
              "backendEndpointPath": "/api/${request.path.proxy+}"
            }
          }
        }
      }
    }
  },
  "securityDefinitions": {
    "x-nhncloud-jwt": {
      "type": "apiKey",
      "name": "Authorization",
      "in": "header"
    },
    "x-nhncloud-apikey": {
      "type": "apiKey",
      "name": "x-nhn-apikey",
      "in": "header"
    }
  },
  "definitions": {
    "MemberModel": {
      "type": "object",
      "required": [
        "name"
      ],
      "properties": {
        "name": {
          "type": "string"
        },
        "description": {
          "type": "string",
          "description": "member description",
          "maxLength": 128
        }
      }
    }
  }
}
```

</details>

|フィールド                                 |タイプ    |説明                                          |
|-------------------------------------|--------|----------------------------------------------|
|swagger                     |String    | Swagger仕様のバージョン。 [Swagger Object](https://swagger.io/specification/v2/#swagger-object)参考|
|info         | Object   | APIのメタデータ領域です。 [Info Object](https://swagger.io/specification/v2/#swagger-object)参考|
|info.version   |String  | APIのバージョン情報です。ステージ配布リクエスト日時が設定されます。 [Info Object](https://swagger.io/specification/v2/#info-object)参考|
|info.title      |String  | APIのタイトルです。ステージ名が設定されます。 [Info Object](https://swagger.io/specification/v2/#info-object)参考|
|host|String    |APIを提供するホストです。ステージURLが設定されます。 [Swagger Object](https://swagger.io/specification/v2/#swagger-object)参考|
|schemes              |Array  | APIのサポート転送プロトコルです。[http、https]が設定されます。 [Swagger Object > schemes](https://swagger.io/specification/v2/#swagger-object)参考|
|paths         | Object  | APIのパスです。リソースメソッドのパスが設定されます。 [Paths Object](https://swagger.io/specification/v2/#pathsObject)参考|
|paths.{path} | Object | {path}はAPIのパスです。リソースメソッドのパスが設定されます。 [Paths Object](https://swagger.io/specification/v2/#pathsObject)参考|
|paths.{path}.{operation}         |Object  | {operation}はAPIパスのオペレーションです。リソースメソッドに設定されます。 [Path Item Object](https://swagger.io/specification/v2/#path-item-object)参考|
|paths.{path}.{operation}.consumes         | Array  | APIパスのオペレーションが使用できるMIMEタイプリストです。 |
|paths.{path}.{operation}.consumes[0]         | String  | APIパスのオペレーションが使用できるMIMEタイプです。 |
|paths.{path}.{operation}.produces         | Array  | APIパスのオペレーションが作成できるMIMEタイプリストです。 |
|paths.{path}.{operation}.produces[0]         | String  | APIパスのオペレーションが作成できるMIMEタイプです。 |
|paths.{path}.{operation}.summary                |String  | APIの要約です。リソースの名前が設定されます。 [Operation Object](https://swagger.io/specification/v2/#operation-object)参考|
|paths.{path}.{operation}.description                |String  |APIの説明です。リソースの説明が設定されます。 [Operation Object](https://swagger.io/specification/v2/#operation-object)参考|
|paths.{path}.{operation}.parameters                | Object  | APIパラメータです。リソースのパス変数とリクエストパラメータが設定されます。 [Parameter Object](https://swagger.io/specification/v2/#parameter-object)参考|
|paths.{path}.{operation}.responses                | Object  | APIレスポンスです。リソースレスポンスが設定されます。 [Responses Object](https://swagger.io/specification/v2/#responses-object)参考|
|paths.{path}.{operation}.security     | Array  | APIオペレーションの作業に使用されるセキュリティ定義です。 API Key、認証(HMAC、JWT)設定時のAPI Gatewayのユーザー定義設定が含まれます。 |
|paths.{path}.{operation}.x-nhncloud-apigateway     | Object  | NHN Cloud API Gateway定義設定領域 |
|paths.{path}.{operation}.x-nhncloud-apigateway.plugins     | Object  | API Gatewayのユーザー定義プラグイン情報領域です。リソース > プラグイン設定とリソースとマッピングされたバックエンドエンドポイントパスの設定が含まれます。 |
|securityDefinitions          |Object    | セキュリティ定義オブジェクトです。 API Key、認証(HMAC、JWT)設定時にAPI Gatewayのユーザー定義設定が含まれます。 [Security Definitions Object](https://swagger.io/specification/v2/#securityDefinitionsObject)参考|
|definitions | Object | リクエストおよびレスポンスで使用されるデータ型の領域。リクエストパラメータ/レスポンスから参照したモデルの定義が設定されます。 [Definitions Object](https://swagger.io/specification/v2/#definitionsObject)参考| 

<a id="api-key-2"></a>
## API Key { #api-key-2 }

<a id="list-api-keys"></a>
### API Keyリスト照会 { #list-api-keys }
- API Keyリストを照会します。
- 複数のリクエストクエリパラメータがある場合、すべての条件を満たすリストを返します。

<a id="list-api-keys-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |
| apiKey | String | 任意 | なし | なし | PrimaryまたはSecondary API Keyフィルタ条件 |
| apiKeyId | String | 任意 | なし | なし | API Key IDフィルタ条件 |
| apiKeyName | String | 任意 | なし | なし | API Key名フィルタ条件。 API Key名の開始文字列は一致する必要があります。 |
| apiKeyStatus | Enum | 任意 | なし | ACTIVE, INACTIVE | API Key状態フィルタ条件。 [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |

<a id="list-api-keys-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiKeyList": [
    {
      "appKey": "{appkey}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "apiKeyDescription": "For User1",
      "primaryApiKey": "{primaryApiKey}",
      "secondaryApiKey": "{secondaryApiKey}",
      "apiKeyStatus": "ACTIVE",
      "createdAt": "2021-06-10T03:06:52.000Z",
      "updatedAt": "2021-06-10T03:06:52.000Z"
    }
  ]
}
```

</details>

| フィールド                            | タイプ     | 説明                                              |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | ページング領域                                          |
| paging.page                     | Integer  | 現在ページ                                          |
| paging.limit                    | Integer  | ページあたりの件数                                       |
| paging.totalCount               | Integer  | 総件数                                           |
| apiKeyList                      | List     | API Keyリスト領域                                   |
| apiKeyList[0]                   | Object   | API Key領域                                      |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key名                                      |
| apiKeyList[0].apiKeyDescription | String   | API Keyの説明                                      |
| apiKeyList[0].primaryApiKey     | String   | Primary API Keyの値                               |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Keyの値                             |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |
| apiKeyList[0].createdAt         | DateTime | API Keyの作成日時                                    |
| apiKeyList[0].updatedAt         | DateTime | API Keyの修正日時                                    |

<a id="create-api-key"></a>
### API Keyの作成 { #create-api-key }
- API Keyを作成します。 

<a id="create-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/apikeys |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE"
}
```

</details>

| 名前              | タイプ   | 必須かどうか | デフォルト値 | 有効範囲          | 説明                                              |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | 必須  | なし | 最大50文字         | API Key名                                      |
| apiKeyDescription | String | 任意  | なし | 最大200文字        | API Keyの説明                                      |
| apiKeyStatus      | Enum   | 必須  | なし | ACTIVE, INACTIVE | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |

<a id="create-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

</details>

| フィールド                     | タイプ     | 説明                                              |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key領域                                      |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key名                                      |
| apiKey.apiKeyDescription | String   | API Keyの説明                                      |
| apiKey.primaryApiKey     | String   | Primary API Key値                               |
| apiKey.secondaryApiKey   | String   | Secondary API Key値                             |
| apiKey.apiKeyStatus      | Enum     | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |
| apiKey.createdAt         | DateTime | API Key作成日時                                    |
| apiKey.updatedAt         | DateTime | API Key修正日時                                    |


<a id="modify-api-key"></a>
### API Keyの修正 { #modify-api-key }
- API Key名、説明、状態を修正します。
- API Keyの状態をINACTIVEに変更すると、API Keyが無効化され、APIの呼び出しができなくなります。

<a id="modify-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 必須 | なし | なし | API Key ID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE"
}
```

</details>

| 名前              | タイプ   | 必須かどうか | デフォルト値 | 有効範囲          | 説明                                              |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | 必須  | なし | 最大50文字         | API Key名                                      |
| apiKeyDescription | String | 任意  | なし | 最大200文字        | API Keyの説明                                      |
| apiKeyStatus      | Enum   | 必須  | なし | ACTIVE, INACTIVE | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |

<a id="modify-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

</details>

| フィールド                     | タイプ     | 説明                                              |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key領域                                      |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key名                                      |
| apiKey.apiKeyDescription | String   | API Keyの説明                                      |
| apiKey.primaryApiKey     | String   | Primary API Key値                               |
| apiKey.secondaryApiKey   | String   | Secondary API Key値                             |
| apiKey.apiKeyStatus      | Enum     | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |
| apiKey.createdAt         | DateTime | API Key作成日時                                    |
| apiKey.updatedAt         | DateTime | API Key修正日時                                    |


<a id="delete-api-key"></a>
### API Keyの削除 { #delete-api-key }
- API Keyを削除します。削除されたAPI Keyは復元できません。
- 使用量プランのステージに関連付けられているAPI Keyがある場合、 API Keyを削除できません。削除するにはAPI Keyを接続解除する必要があります。

<a id="delete-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 必須 | なし | なし | API Key ID |

<a id="delete-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

</details>

<a id="reissue-api-key"></a>
### API Keyの再発行 { #reissue-api-key }
- API Key値として使用されるPrimary API Key、Secondary API Keyはそれぞれ再発行できます。
- 再発行する場合、以前のAPI KeyではAPIを呼び出せません。再発行前のAPI Keyへ戻すことはできません。

<a id="reissue-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/regenerate |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 必須 | なし | なし | API Key ID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apiKeyType": "PRIMARY"
}
```

</details>

| 名前              | タイプ   | 必須かどうか | デフォルト値 | 有効範囲          | 説明                                              |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyType      | Enum   | 必須  | なし | PRIMARY、SECONDARY | 変更したいAPI Keyタイプ。 [API KeyタイプEnumコード](./enum-code/#api-key-type)参考 |

<a id="reissue-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

</details>

| フィールド                     | タイプ     | 説明                                              |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key領域                                      |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key名                                      |
| apiKey.apiKeyDescription | String   | API Keyの説明                                      |
| apiKey.primaryApiKey     | String   | Primary API Key値                               |
| apiKey.secondaryApiKey   | String   | Secondary API Key値                             |
| apiKey.apiKeyStatus      | Enum     | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |
| apiKey.createdAt         | DateTime | API Key作成日時                                    |
| apiKey.updatedAt         | DateTime | API Key修正日時                                    |

<a id="list-api-keys-that-can-be-connected-to-stage"></a>
### ステージに関連付けることができるAPI Keyリストの照会 { #list-api-keys-that-can-be-connected-to-stage }
- ステージに関連付けることができるAPI Keyリストを照会します。
- 複数のリクエストクエリパラメータがある場合、すべての条件を満たすリストを返します。

<a id="list-api-keys-that-can-be-connected-to-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/stages/{stageId}/apikeys/connectable |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| stageId | String | 必須 | なし | なし | Stage ID |


[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |
| apiKey | String | 任意 | なし | なし | primaryまたはsecondary API Key値 |
| apiKeyId | String | 任意 | なし | なし | API Key ID |
| apiKeyName | String | 任意 | なし | なし | API Key名の開始文字列 |
| apiKeyStatus | Enum | 任意 | なし | ACTIVE、INACTIVE | [API Keyの状態Enumコード](./enum-code/#api-key-status)参考 |

<a id="list-api-keys-that-can-be-connected-to-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiKeyList": [
    {
      "appKey": "{appkey}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "apiKeyDescription": "For User1",
      "primaryApiKey": "{primaryApiKey}",
      "secondaryApiKey": "{secondaryApiKey}",
      "apiKeyStatus": "ACTIVE",
      "createdAt": "2021-06-10T03:06:52.000Z",
      "updatedAt": "2021-06-10T03:06:52.000Z"
    }
  ]
}
```

</details>

| フィールド                            | タイプ     | 説明                                              |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | ページング領域                                          |
| paging.page                     | Integer  | 現在ページ                                          |
| paging.limit                    | Integer  | ページあたりの件数                                       |
| paging.totalCount               | Integer  | 総件数                                           |
| apiKeyList                      | List     | API Keyリスト領域                                   |
| apiKeyList[0]                   | Object   | API Key領域                                      |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key名                                      |
| apiKeyList[0].apiKeyDescription | String   | API Keyの説明                                      |
| apiKeyList[0].primaryApiKey     | String   | Primary API Keyの値                               |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Keyの値                             |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Keyの状態Enumコード](./enum-code/#enum-code/#api-key)参考 |
| apiKeyList[0].createdAt         | DateTime | API Keyの作成日時                                    |
| apiKeyList[0].updatedAt         | DateTime | API Keyの修正日時                                    |


<a id="usage-plan"></a>
## 使用量プラン { #usage-plan }

<a id="list-usage-plans"></a>
### 使用量プランリストの照会 { #list-usage-plans }
- 使用量プランリストを照会します。

<a id="list-usage-plans-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

<a id="list-usage-plans-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanList": [
    {
      "appKey": "{appKey}",
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic",
      "usagePlanDescription": "It's for Basic User",
      "rateLimitRequestPerSecond": 10,
      "quotaLimitPeriodUnitCode": "DAY",
      "quotaLimit": 100,
      "createdAt": "2021-09-09T05:04:37.000Z",
      "updatedAt": "2021-09-09T05:04:37.000Z"
    }
  ]
}
```

</details>

| フィールド                                       | タイプ     | 説明                                              |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | ページング領域                                          |
| paging.page                                | Integer  | 現在ページ                                          |
| paging.limit                               | Integer  | ページあたりの件数                                        |
| paging.totalCount                          | Integer  | 総件数                                           |
| usagePlanList                              | List     | 使用量プランリスト領域                                    |
| usagePlanList[0]                           | Object   | 使用量プラン領域                                       |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 使用量プランID                                         |
| usagePlanList[0].usagePlanName             | String   | 使用量プランの名前                                       |
| usagePlanList[0].usagePlanDescription      | String   | 使用量プランの説明                                       |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 1秒あたりのリクエスト数制限                                      |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| usagePlanList[0].quotaLimit                | Integer  | 割り当て量期間単位別リクエスト割り当て量                              |
| usagePlanList[0].createdAt                 | DateTime | 使用量プランの作成日時                                     |
| usagePlanList[0].updatedAt                 | DateTime | 使用量プランの修正日時                                     |



<a id="get-usage-plan"></a>
### 単一使用量プランの照会 { #get-usage-plan }
- 単一使用量プランを照会します。

<a id="get-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |

<a id="get-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "usagePlan": {
        "appKey": "{appKey}",
        "usagePlanId": "{usagePlanId}",
        "usagePlanName": "Basic",
        "usagePlanDescription": "It's for Basic User",
        "rateLimitRequestPerSecond": 10,
        "quotaLimitPeriodUnitCode": "MONTH",
        "quotaLimit": 2147483647,
        "createdAt": "2021-11-02T02:26:44.000Z",
        "updatedAt": "2021-11-02T02:26:44.000Z"
    }
}
```

</details>

| フィールド                                | タイプ     | 説明                                              |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 使用量プラン領域                                       |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 使用量プランID                                         |
| usagePlan.usagePlanName             | String   | 使用量プランの名前                                       |
| usagePlan.usagePlanDescription      | String   | 使用量プランの説明                                       |
| usagePlan.rateLimitRequestPerSecond | Integer  | 1秒あたりのリクエスト数制限                                      |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| usagePlan.quotaLimit                | Integer  | 割り当て量期間単位別リクエスト割り当て量                              |
| usagePlan.createdAt                 | DateTime | 使用量プランの作成日時                                     |
| usagePlan.updatedAt                 | DateTime | 使用量プランの修正日時                                     |

<a id="create-usage-plan"></a>
### 使用量プランの作成 { #create-usage-plan }
- 使用量プランを作成します。

<a id="create-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "usagePlanName": "string",
  "usagePlanDescription": "string",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

</details>

| 名前                      | タイプ    | 必須かどうか | デフォルト値 | 有効範囲      | 説明                                              |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | 必須  | なし | 最大50文字     | 使用量プランの名前                                       |
| usagePlanDescription      | String  | 任意  | なし | 最大200文字    | 使用量プランの説明                                       |
| rateLimitRequestPerSecond | Integer | 任意  | なし | 1～5000       | 1秒あたりのリクエスト数制限                                      |
| quotaLimitPeriodUnitCode  | Enum    | 任意  | なし | DAY, MONTH   | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| quotaLimit                | Integer | 条件付き必須 | なし | 1～2147483647 | quotaLimitPeriodUnitCodeが設定されている場合は必須。割り当て量期間単位別リクエスト割り当て量                              |

<a id="create-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "usagePlan": {
    "appKey": "{appKey}",
    "usagePlanId": "{usagePlanId}",
    "usagePlanName": "Basic",
    "usagePlanDescription": "It's for Basic User",
    "rateLimitRequestPerSecond": 10,
    "quotaLimitPeriodUnitCode": "MONTH",
    "quotaLimit": 2147483647,
    "createdAt": "2021-11-02T02:26:44.087Z",
    "updatedAt": "2021-11-02T02:26:44.087Z"
  }
}
```

</details>

| フィールド                                | タイプ     | 説明                                              |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 使用量プラン領域                                       |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 使用量プランID                                         |
| usagePlan.usagePlanName             | String   | 使用量プランの名前                                       |
| usagePlan.usagePlanDescription      | String   | 使用量プランの説明                                       |
| usagePlan.rateLimitRequestPerSecond | Integer  | 1秒あたりのリクエスト数制限                                      |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| usagePlan.quotaLimit                | Integer  | 割り当て量期間単位別リクエスト割り当て量                              |
| usagePlan.createdAt                 | DateTime | 使用量プランの作成日時                                     |
| usagePlan.updatedAt                 | DateTime | 使用量プランの修正日時                                     |


<a id="modify-usage-plan"></a>
### 使用量プランの修正 { #modify-usage-plan }
- 使用量プランを修正します。 
- 割り当て量期間単位を「なし」に修正すると、関連付けられているAPI Keyのリクエスト割り当て量使用量は初期化されます。

<a id="modify-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "usagePlanName": "Basic",
  "usagePlanDescription": "It's for Basic User",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

</details>

| 名前                      | タイプ    | 必須かどうか | デフォルト値 | 有効範囲      | 説明                                              |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | 必須  | なし | 最大50文字     | 使用量プランの名前                                       |
| usagePlanName             | String  | 任意  | なし | 最大200文字    | 使用量プランの説明                                       |
| rateLimitRequestPerSecond | Integer | 任意  | なし | 1～5000       | 1秒あたりのリクエスト数制限                                      |
| quotaLimitPeriodUnitCode  | Enum    | 任意  | なし | DAY, MONTH   | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| quotaLimit                | Integer | 条件付き必須 | なし | 1～2147483647 | quotaLimitPeriodUnitCodeが設定されている場合は必須。割り当て量期間単位別リクエスト割り当て量                              |

<a id="modify-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "usagePlan": {
    "appKey": "{appKey}",
    "usagePlanId": "{usagePlanId}",
    "usagePlanName": "Basic",
    "usagePlanDescription": "It's for Basic User",
    "rateLimitRequestPerSecond": 10,
    "quotaLimitPeriodUnitCode": "DAY",
    "quotaLimit": 100,
    "createdAt": "2021-11-02T02:26:44.087Z",
    "updatedAt": "2021-11-02T02:26:44.087Z"
  }
}
```

</details>

| フィールド                                | タイプ     | 説明                                              |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 使用量プラン領域                                       |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 使用量プランID                                         |
| usagePlan.usagePlanName             | String   | 使用量プランの名前                                       |
| usagePlan.usagePlanDescription      | String   | 使用量プランの説明                                       |
| usagePlan.rateLimitRequestPerSecond | Integer  | 1秒あたりのリクエスト数制限                                      |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| usagePlan.quotaLimit                | Integer  | 割り当て量期間単位別リクエスト割り当て量                              |
| usagePlan.createdAt                 | DateTime | 使用量プランの作成日時                                     |
| usagePlan.updatedAt                 | DateTime | 使用量プランの修正日時                                     |


<a id="delete-usage-plan"></a>
### 使用量プランの削除 { #delete-usage-plan }
- 使用量プランを削除します。
- 使用量プランに関連付けられたステージを全て解除した後、使用量プランを削除できます。

<a id="delete-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |

<a id="delete-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

</details>


<a id="list-stages-associated-with-usage-plan"></a>
### 使用量プランに関連付けられたステージリストの照会 { #list-stages-associated-with-usage-plan }
- 使用量プランに関連付けられたステージリストを照会します。

<a id="list-stages-associated-with-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |

<a id="list-stages-associated-with-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanStageList": [
    {
      "regionCode": "KR1",
      "apigwServiceId": "{apigwServiceId}",
      "apigwServiceName": "APIGW Example",
      "stageId": "{stageId}",
      "stageName": "custom",
      "stageUrl": "kr1-example-custom.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic"
    }
  ]
}
```

</details>

| フィールド                                  | タイプ    | 説明                   |
| ------------------------------------- | ------- | ---------------------- |
| paging                                | Object  | ページング領域               |
| paging.page                           | Integer | 現在ページ               |
| paging.limit                          | Integer | ページあたりの件数             |
| paging.totalCount                     | Integer | 総件数                |
| usagePlanStageList                    | List    | 使用量プランに関連付けられたステージリスト領域 |
| usagePlanStageList[0]                | Object  | 使用量プランに関連付けられたステージ領域  |
| usagePlanStageList[0].regionCode | Enum | [API GatewayリージョンEnumコード](./enum-code/#api-gateway-region)参考 |
| usagePlanStageList[0].apigwServiceId | String  | API GatewayサービスID     |
| usagePlanStageList[0].apigwServiceName      | String  | API Gatewayサービス名   |
| usagePlanStageList[0].stageId        | String  | ステージID                |
| usagePlanStageList[0].stageName      | String  | ステージ名              |
| usagePlanStageList[0].stageUrl       | String  | ステージURL               |
| usagePlanStageList[0].stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
| usagePlanStageList[0].stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
| usagePlanStageList[0].stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
| usagePlanStageList[0].usagePlanId    | String  | 使用量プランID              |
| usagePlanStageList[0].usagePlanName  | String  | 使用量プランの名前            |


<a id="connect-stage-to-usage-plan"></a>
### 使用量プランにステージを関連付ける { #connect-stage-to-usage-plan }
- 使用量プランにステージを関連付けます。

<a id="connect-stage-to-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |

<a id="connect-stage-to-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

</details>

<a id="disconnect-stage-from-usage-plan"></a>
### 使用量プランに関連付けられたステージの解除 { #disconnect-stage-from-usage-plan }
- 使用量プランに関連付けられたステージを解除します。
- ステージに関連付けられたAPI Keyが存在する場合は関連付けを削除できません。

<a id="disconnect-stage-from-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |

<a id="disconnect-stage-from-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

</details>

<a id="list-usage-plans-associated-with-stage"></a>
### ステージが関連付けられた使用量プランリスト照会 { #list-usage-plans-associated-with-stage }
- ステージが関連付けられた使用量プランリストを照会します。

<a id="list-usage-plans-associated-with-stage-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/stages/{stageId} |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

<a id="list-usage-plans-associated-with-stage-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanList": [
    {
      "appKey": "{appKey}",
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic",
      "usagePlanDescription": "It's for Basic User",
      "rateLimitRequestPerSecond": 10,
      "quotaLimitPeriodUnitCode": "DAY",
      "quotaLimit": 100,
      "createdAt": "2021-11-02T02:26:44.087Z",
      "updatedAt": "2021-11-02T02:26:44.087Z"
    }
  ]
}
```

</details>

| フィールド                                       | タイプ     | 説明                                              |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | ページング領域                                          |
| paging.page                                | Integer  | 現在ページ                                          |
| paging.limit                               | Integer  | ページあたりの件数                                        |
| paging.totalCount                          | Integer  | 総件数                                           |
| usagePlanList                              | List     | 使用量プランリスト領域                                    |
| usagePlanList[0]                           | Object   | 使用量プラン領域                                       |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 使用量プランID                                         |
| usagePlanList[0].usagePlanName             | String   | 使用量プランの名前                                       |
| usagePlanList[0].usagePlanDescription      | String   | 使用量プランの説明                                       |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 1秒あたりのリクエスト数制限                                      |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| usagePlanList[0].quotaLimit                | Integer  | 割り当て量期間単位別リクエスト割り当て量                              |
| usagePlanList[0].createdAt                 | DateTime | 使用量プランの作成日時                                     |
| usagePlanList[0].updatedAt                 | DateTime | 使用量プランの修正日時                                     |

<a id="api-key-subscription"></a>
## API Keyの購読 { #api-key-subscription }

<a id="list-api-key-subscriptions"></a>
### API Key購読リスト照会 { #list-api-key-subscriptions }
- API Keyが関連付けられたステージと使用量プラン情報のリストを照会します。

<a id="list-api-key-subscriptions-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/subscriptions |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 必須 | なし | なし | API Key ID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |
| stageUrl | String | 任意 | なし | なし | Stage Urlフィルタ条件 |

<a id="list-api-key-subscriptions-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "paging": {
        "limit": 10,
        "page": 1,
        "totalCount": 1
    },
    "subscribedStageAndUsagePlanList": [
        {
            "subscriptionId": "{subscriptionId}",
            "subscriptionStatus": "APPROVAL",
            "apiKeyId": "{apiKeyId}",
            "apigwServiceName": "test api gateway",
            "stageId": "{stageId}",
            "stageName": null,
            "stageUrl": "kr1-example.api.nhncloudservice.com",
            "stageCustomDomainList": [],
            "usagePlanId": "{usagePlanId}",
            "usagePlanName": "Basic",
            "usagePlanDescription": "It's for Basic User",
            "rateLimitRequestPerSecond": 10,
            "quotaLimitPeriodUnitCode": "DAY",
            "quotaLimit": 100
        }
    ]
}
```

</details>

| フィールド                                                         | タイプ    | 説明                                              |
| ------------------------------------------------------------ | ------- | ------------------------------------------------- |
| paging                                                       | Object  | ページング領域                                          |
| paging.page                                                  | Integer | 現在ページ                                          |
| paging.limit                                                 | Integer | ページあたりの件数                                        |
| paging.totalCount                                            | Integer | 総件数                                           |
| subscribedStageAndUsagePlanList                              | List    | API Keyが関連付けられたステージと使用量プランリスト領域              |
| subscribedStageAndUsagePlanList[0]                           | Object    | API Keyが関連付けられたステージと使用量プラン領域              |
| subscribedStageAndUsagePlanList[0].subscriptionId            | String  | 購読ID                                     |
| subscribedStageAndUsagePlanList[0].subscriptionStatus        | Enum    | [API Keyの購読状態Enumコード](./enum-code/#api-key-subscription-status)参考            |
| subscribedStageAndUsagePlanList[0].apiKeyId                  | String  | API Key ID                                        |
| subscribedStageAndUsagePlanList[0].apigwServiceName          | String  | API Gatewayサービス名                              |
| subscribedStageAndUsagePlanList[0].stageId                   | String  | ステージID                                           |
| subscribedStageAndUsagePlanList[0].stageName                 | String  | ステージ名                                         |
| subscribedStageAndUsagePlanList[0].stageUrl                  | String  | ステージURL                                          |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
| subscribedStageAndUsagePlanList[0].usagePlanId               | String  | 使用量プランID                                         |
| subscribedStageAndUsagePlanList[0].usagePlanName             | String  | 使用量プランの名前                                       |
| subscribedStageAndUsagePlanList[0].usagePlanDescription      | String  | 使用量プランの説明                                       |
| subscribedStageAndUsagePlanList[0].rateLimitRequestPerSecond | Integer | 1秒あたりのリクエスト数制限                                      |
| subscribedStageAndUsagePlanList[0].quotaLimitPeriodUnitCode  | Enum    | [使用量プラン > 割り当て量期間単位Enumコード](./enum-code/#usage-plan-quota-period-unit)参考 |
| subscribedStageAndUsagePlanList[0].quotaLimit                | Integer | 割り当て量期間単位別リクエスト割り当て量                              |


<a id="list-api-keys-subscribing-to-a-stage-in-the-usage-plan"></a>
### 使用量プランのステージを購読中のAPI Keyリスト照会 { #list-api-keys-subscribing-to-a-stage-in-the-usage-plan }
- 使用量プランのステージに関連付けられているAPI Keyリストを照会します。
- 複数のリクエストクエリパラメータがある場合、すべての条件を満たすリストを返します。

<a id="list-api-keys-subscribing-to-a-stage-in-the-usage-plan-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |
| apiKey | String | 任意 | なし | なし | PrimaryまたはSecondary API Keyフィルタ条件 |
| apiKeyId | String | 任意 | なし | なし | API Key IDフィルタ条件 |
| apiKeyName | String | 任意 | なし | なし | API Key名フィルタ条件。 API Key名の開始文字列は一致する必要があります。  |
| apiSubscriptionStatus | Enum | 任意 | なし | APPROVAL | [API Keyの購読状態Enumコード](./enum-code/#api-key-subscription-status)参考 |

<a id="list-api-keys-subscribing-to-a-stage-in-the-usage-plan-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiSubscriptionList": [
    {
      "subscriptionId": "{subscriptionId}",
      "subscriptionStatus": "APPROVAL",
      "subscriptionDescription": null,
      "stageId": "{stageId}",
      "usagePlanId": "{usagePlanId}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "createdAt": "2021-08-27T04:53:57.000Z",
      "updatedAt": "2021-09-10T00:26:03.000Z"
    }
  ]
}
```

</details>

| フィールド                                           | タイプ     | 説明                                 |
| ---------------------------------------------- | -------- | ------------------------------------ |
| paging                                         | Object   | ページング領域                             |
| paging.page                                    | Integer  | 現在ページ                             |
| paging.limit                                   | Integer  | ページあたりの件数                           |
| paging.totalCount                              | Integer  | 総件数                              |
| apiSubscriptionList                            | List     | 購読情報リスト領域    |
| apiSubscriptionList[0]                         | Object   | 購読情報領域    |
| apiSubscriptionList[0].subscriptionId          | String   | 購読ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Keyの購読状態Enumコード](./enum-code/#api-key-subscription-status)参考 |
| apiSubscriptionList[0].subscriptionDescription | String   | 購読の説明                              |
| apiSubscriptionList[0].stageId                 | String   | ステージID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 使用量プランID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key名                         |
| apiSubscriptionList[0].createdAt               | DateTime | 購読作成日時                            |
| apiSubscriptionList[0].updatedAt               | DateTime | 購読修正日時                            |


<a id="subscribe-to-api-key-connect-api-key"></a>
### API Key購読(API Key接続) { #subscribe-to-api-key-connect-api-key }
- 使用量プランのステージにリクエストしたAPI Keyリストを接続します。
- 関連付けられたAPI KeyのみAPI Keyの認証に成功し、使用量プランの使用量制限が適用されます。
- 異なる使用量プランの同じステージに関連付けられているAPI Keyは接続できません。

<a id="subscribe-to-api-key-connect-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apiKeyIdList": [
    "{apiKeyId}"
  ]
}
```

</details>

| 名前                      | タイプ    | 必須かどうか | デフォルト値 | 有効範囲      | 説明                                              |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiKeyIdList              | List  | 必須  | なし | 最大100個     | API Key IDリスト領域                                      |
| apiKeyIdList[0]           | String  | 必須  | なし | なし      | API Key ID                                        |

<a id="subscribe-to-api-key-connect-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiSubscriptionList": [
    {
      "subscriptionId": "{subscriptionId}",
      "subscriptionStatus": "APPROVAL",
      "subscriptionDescription": null,
      "stageId": "{stageId}",
      "usagePlanId": "{usagePlanId}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "createdAt": "2021-11-03T02:53:21.775Z",
      "updatedAt": "2021-11-03T02:53:21.775Z"
    }
  ]
}
```

</details>

| フィールド                                           | タイプ     | 説明                                 |
| ---------------------------------------------- | -------- | ------------------------------------ |
| apiSubscriptionList                            | List     | 購読情報リスト領域                        |
| apiSubscriptionList[0]                         | Object   | 購読情報領域                      |
| apiSubscriptionList[0].subscriptionId          | String   | 購読ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Keyの購読状態Enumコード](./enum-code/#api-key-subscription-status)参考 |
| apiSubscriptionList[0].subscriptionDescription | String   | 購読の説明                              |
| apiSubscriptionList[0].stageId                 | String   | ステージID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 使用量プランID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key名                         |
| apiSubscriptionList[0].createdAt               | DateTime | 購読作成日時                            |
| apiSubscriptionList[0].updatedAt               | DateTime | 購読修正日時                            |


<a id="unsubscribe-from-api-key-disconnect-api-key"></a>
### API Key購読キャンセル(API Key接続解除) { #unsubscribe-from-api-key-disconnect-api-key }
- 使用量プランのステージから、リクエストしたAPI Keyリストの関連付けを削除します。
- 関連付けが削除されたAPI KeyはAPI Keyの認証に失敗し、APIの呼び出しが失敗します。 

<a id="unsubscribe-from-api-key-disconnect-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| DELETE | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "apiSubscriptionIdList": [
    "{apiKeyId}"
  ]
}
```

</details>

| 名前                      | タイプ    | 必須かどうか | デフォルト値 | 有効範囲      | 説明                                              |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiSubscriptionIdList             | List  | 必須  | なし | 最大100個     | 購読IDリスト領域                                      |
| apiSubscriptionIdList[0]             | String  | 必須  | なし | なし      | 購読ID                                        |

<a id="unsubscribe-from-api-key-disconnect-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

</details>


<a id="change-usage-plan-of-api-key"></a>
### API Keyの使用量プラン変更 { #change-usage-plan-of-api-key }
- 選択したステージが関連付けられている他の使用量プランにのみ変更できます。
- 使用量プランを変更すると、API Keyリクエスト割り当て量の使用量は初期化されます。
    - 割り当て量期間単位が「日」または「月」の使用量プランに変更された場合、関連付けられているAPI Keyリクエスト割り当て量の使用量は維持されます。リクエスト割り当て量の限度が低い使用量プランに変更すると、使用量を超えることがあります。 
    - 割り当て量期間単位が「なし」の使用量プランに変更すると、関連付けられているAPI Keyリクエスト割り当て量の使用量は初期化されます。
  
<a id="change-usage-plan-of-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions/{subscriptionId}/change-usage-plan |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 必須 | なし | なし | 使用量プランID |
| stageId | String | 必須 | なし | なし | ステージID |
| subscriptionId | String | 必須 | なし | なし | 購読ID |

[Request Body]

<details>
  <summary><strong>リクエスト例</strong></summary>

```json
{
  "changeUsagePlanId": "{usagePlanId}"
}
```

</details>

| 名前                      | タイプ    | 必須かどうか | デフォルト値 | 有効範囲      | 説明                                              |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| changeUsagePlanId            | String  | 必須  | なし | なし      | 変更する使用量計画ID                                        |

<a id="change-usage-plan-of-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

</details>

<a id="statistics"></a>
## 統計 { #statistics }

<a id="query-by-stage-resource"></a>
### ステージリソース別照会 { #query-by-stage-resource }
- 照会期間中のリソース別統計データを照会します。


<a id="query-by-stage-resource-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/metrics |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| stageId | String | 必須 | なし | なし | ステージID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | 必須 | なし | なし | 統計照会開始日時 |
| endTime | DateTime | 必須 | なし | なし | 統計照会終了日時 |
| page | Integer | 任意 | 1 | なし | ページ |
| limit | Integer | 任意 | 10 | 最大1000 | ページあたりの件数 |

* startTime, endTimeフィールドは過去90日まで照会できます。
* stageTime, endTimeフィールドはISO8601形式の日文字列形式で入力します。 
    * UTC表記：yyyy-MM-dd'T'HH:mm:ssZ
    * UTC基準タイムオフセット表記：yyyy-MM-dd'T'HH:mm:ss±hh:mm


<a id="query-by-stage-resource-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 2
  },
  "data": [
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "GET",
      "successCount": 31,
      "failCount": 18,
      "status2xxCount": 29,
      "status3xxCount": 2,
      "status4xxCount": 18,
      "status5xxCount": 0,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 35,
      "networkOutboundByte": 26059
    },
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "POST",
      "successCount": 20,
      "failCount": 2,
      "status2xxCount": 18,
      "status3xxCount": 0,
      "status4xxCount": 0,
      "status5xxCount": 2,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 129,
      "networkOutboundByte": 3032
    }
  ],
  "metricsLatestUpdatedAt": "2021-11-29T08:50:57.000Z"
}
```

</details>

|フィールド                                 |タイプ    |説明                                       |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | ページング領域                                   |
|paging.page                          |Integer | 現在ページ                                  |
|paging.limit                         |Integer | ページあたりの件数                                |
|paging.totalCount                    |Integer | 総件数                                    |
|data                                 |List    | リソース別統計データリスト領域                    |
|data[0]                              |Object    | リソース別統計データ領域                    |
|data[0].uriPattern                   |String  | リソースパスまたはパスパターン                       |
|data[0].httpMethodType               |Enum  | [HTTPメソッドタイプEnumコード](./enum-code/#http-method-type)参考                           |
|data[0].successCount                 |Long    | API成功数(レスポンスHTTPステータスコードが2xx、3xxの場合) |
|data[0].failCount               |Long    | API失敗数(レスポンスHTTPステータスコードが4xx、5xxの場合) |
|data[0].status2xxCount               |Long    | レスポンスHTTPステータスコードが2xxのAPI呼び出し数 |
|data[0].status3xxCount               |Long    | レスポンスHTTPステータスコードが3xxのAPI呼び出し数 |
|data[0].status4xxCount               |Long    | レスポンスHTTPステータスコードが4xxのAPI呼び出し数 |
|data[0].status5xxCount               |Long    | レスポンスHTTPステータスコードが5xxのAPI呼び出し数 |
|data[0].statusEtcCount               |Long    | 2xx、3xx、4xx、5xx以外のレスポンスHTTPステータスコードAPI呼び出し数 |
|data[0].avgResponseTimeMs            |Long    | 平均APIレスポンス時間(ms) |
|data[0].networkOutboundByte          |Long    | アウトバウンドネットワークバイト合計(bytes) |
|metricsLatestUpdatedAt         | DateTime | 統計データ の最終更新日時 |



<a id="query-by-api-key"></a>
### API Key別照会 { #query-by-api-key }
- API Key別の日単位の統計を照会します。


<a id="query-by-api-key-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/metrics |

[Path Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 必須 | なし | なし | API GatewayサービスID |
| apiKeyId | String | 必須 | なし | なし | API Key ID |

[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | 必須 | なし | なし | 統計照会開始日時 |
| endTime | DateTime | 必須 | なし | なし | 統計照会終了日時 |

* startTime, endTimeフィールドは過去90日まで照会できます。
* stageTime, endTimeフィールドはISO8601形式の日付文字列形式で入力します。
    * UTC表記：yyyy-MM-dd'T'HH:mm:ssZ
    * UTC基準タイムオフセット表記：yyyy-MM-dd'T'HH:mm:ss±hh:mm

<a id="query-by-api-key-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "data": {
    "kr1-{apigwServiceId}-member.api.nhncloudservice.com": {
      "stageName": "member",
      "stageUrl": "kr1-{apigwServiceId1}-member.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 8
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    },
    "kr1-{apigwServiceId}-billing.api.nhncloudservice.com": {
      "stageName": "billing",
      "stageUrl": "kr1-{apigwServiceId}-billing.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 13
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    }
  },
  "metricsLatestUpdatedAt": "2021-11-29T08:50:57.000Z",
  "timeUnit": "ONE_DAYS"
}
```

</details>

|フィールド                                 |タイプ    |説明                                       |
|-------------------------------------|--------|----------------------------------------------|
|data                                 |Object  | API Key統計データ領域                       |
|data.{requestApigwEndpoint}          |Object  | API呼び出しエンドポイント別統計領域              |
|data.{requestApigwEndpoint}.stageName                    |String    | ステージ名          |
|data.{requestApigwEndpoint}.stageUrl                     |String    | ステージURL |
|data.{requestApigwEndpoint}.stageCustomDomainList   |List  |ステージユーザー指定ドメインリスト領域 |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].customDomain   |String  |ユーザー指定ドメイン |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].createdAt   |DateTime  |ユーザー指定ドメイン接続日時  |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries      |Object    | 集計時間単位別API Key統計領域|
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount               |List    | API呼び出し数統計リスト領域 |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0]               |Object    | API呼び出し数統計領域 |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].dateTime   |Long    | 統計時間(Unix time形式) |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].count      |Long    | 統計時間中のAPI呼び出し総数 |
|metricsLatestUpdatedAt         | DateTime | 統計データ の最終更新日時 |
|timeUnit          |Enum    | [統計データ時間単位Enumコード](./enum-code/#statistics-data-time-unit)ONE_DAYS参考 |

* 日単位の統計データは各日の00:00:00の時間データで集計されます。

<a id="query-top-10-services"></a>
### Top 10サービス照会 { #query-top-10-services }
- 全体API呼び出し数、失敗API呼び出し数、平均レスポンス時間を基準に上位10個のAPI Gatewayサービスリストと累積統計を照会できます。


<a id="query-top-10-services-request"></a>
#### リクエスト

[URI]

| メソッド | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/metrics/top-services |


[QueryString Parameter]

| 名前 | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明 |
| --- | --- | --- | --- | --- | --- |
| lastDays | Integer | 任意 | 7 | 1～30 | 照会期間の日数(当日を含む)  |
| order | Enum | 任意 | CALL_COUNT | CALL_COUNT,FAIL_CALL_COUNT,AVG_RESPONSE_TIME | [統計 > Top10サービスソート基準](./enum-code/#statistics-sort-top-10-services-by)|


<a id="query-top-10-services-response"></a>
#### レスポンス

[Response]

<details>
  <summary><strong>レスポンス例</strong></summary>

```json
{
        "header": {
            "isSuccessful": true,
            "resultCode": 0,
            "resultMessage": "SUCCESS"
        },
        "data": [
            {
                "rank": 1,
                "apigwServiceId": "{apigwServiceId1}",
                "apigwServiceName": "apigwservice-1",
                "status2xxCount": 100,
                "status3xxCount": 0,
                "status4xxCount": 0,
                "status5xxCount": 0,
                "statusEtcCount": 0,
                "callCount": 100,
                "failCallCount": 0,
                "successCallCount": 100,
                "avgResponseTimeMs": 6,
                "networkOutboundByte": 31202
            },
            {
                "rank": 2,
                "apigwServiceId": "apigwServiceId2",
                "apigwServiceName": "apigwservice-2",
                "status2xxCount": 50,
                "status3xxCount": 0,
                "status4xxCount": 0,
                "status5xxCount": 0,
                "statusEtcCount": 0,
                "callCount": 50,
                "failCallCount": 0,
                "successCallCount": 50,
                "avgResponseTimeMs": 8,
                "networkOutboundByte": 19220
            }
            ... 
        ],
        "metricsLatestUpdatedAt": "2023-07-19T02:21:08.000Z"
    }
```

</details>

| フィールド | タイプ | 説明 |
| --- | --- | --- |
|data | Object | Top 10サービス統計データ領域 |
|data[0].rank | Integer  | 順位番号 |
|data[0].apigwServiceId | String | API GatewayサービスID |
|data[0].apigwServiceName | String | API Gatewayサービス名 |
|data[0].successCount | Long | API成功数(レスポンスHTTPステータスコードが2xx, 3xxの場合) |
|data[0].failCount | Long | API失敗数(レスポンスHTTPステータスコードが4xx、5xxの場合) |
|data[0].status2xxCount | Long | レスポンスHTTPステータスコードが2xxのAPI呼び出し数 |
|data[0].status3xxCount | Long | レスポンスHTTPステータスコードが3xxのAPI呼び出し数 |
|data[0].status4xxCount | Long | レスポンスHTTPステータスコードが4xxのAPI呼び出し数 |
|data[0].status5xxCount | Long | レスポンスHTTPステータスコードが5xxのAPI呼び出し数 |
|data[0].statusEtcCount | Long | 2xx、3xx、4xx、5xx以外のレスポンスHTTPステータスコードAPI呼び出し数 |
|data[0].avgResponseTimeMs | Long | 平均APIレスポンス時間(ms) |
|data[0].networkOutboundByte | Long | アウトバウンドネットワークバイトの合計(bytes) |
|metricsLatestUpdatedAt | DateTime | 統計データの最新更新日時 |
