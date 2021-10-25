## 스테이지

### 스테이지 목록 조회 
- 스테이지 목록을 조회합니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |

[QueryString Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |

#### 응답

[Response]

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
      "stageDescription": "alpha 환경 스테이지",
      "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
      "stageCustomUrl": null,
      "backendEndpointUrl": "https://backend.com",
      "resourceUpdatedAt": "2021-10-20T06:43:26.000Z",
      "createdAt": "2021-10-20T06:43:26.000Z",
      "updatedAt": "2021-10-20T06:43:26.000Z"
    }
  ]
}
```

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                        |
|paging.page                          |Integer | 현재 페이지                                        |
|paging.limit                         |Integer | 페이지 당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|stageList        |List    | 스테이지 목록 영역 |
|stageList[0].regionCode       |Enum    |[API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode)                |
|stageList[0].apigwServiceId   |String  |API Gateway 서비스 ID  |
|stageList[0].stageId          |String  |스테이지 ID             |
|stageList[0].stageName        |String  |스테이지 이름             |
|stageList[0].stageUrl         |String  |스테이지 URL            |
|stageList[0].stageCustomUrl   |String  |스테이지 사용자 정의 URL   |
|stageList[0].stageDescription |String  |스테이지 설명             |
|stageList[0].backendEndpointUrl|String  |백엔드 엔드포인트 URL       |
|stageList[0].resourceUpdatedAt|DateTime|최근 스테이지 리소스 가져오기 수행 일시 |
|stageList[0].createdAt        |DateTime|스테이지 생성일시           |
|stageList[0].updatedAt        |DateTime|스테이지 수정일시           |


## Swagger Export
- Swagger문서를 조회합니다. 
- Swagger문서는 API Gateway에 배포된 설정 기준이 아닌 현재 스테이지 설정을 기준으로 추출됩니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/swagger |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

#### 응답 


``` json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "string"
  },
  "swaggerData": "{swaggerJson}"
}
```

|필드                                  |타입     |설명                                           |
|-------------------------------------|--------|----------------------------------------------|
|swaggerData        |Object    | 현재 스테이지 기준 Swagger Json 객체 |


### 스테이지 생성
- 스테이지를 생성합니다. 

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |


[Request Body]
```json
{
  "name": "string",
  "description": "string",
  "backendEndpointUrl": "https://backend.com"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| name | String | 조건부 필수 | 없음 | 최대 30자, 영소문자와 숫자만 | 스테이지 이름<br/>기본 스테이지가 아닌 경우 필수 값입니다.  |
| description | String | 선택 | 없음 | 최대 200자  | 스테이지 설명 |
| backendEndpointUrl | String | 필수 | 없음 | 최대 150자, URL형식  | 백엔드 엔드포인트 URL |
- name 필드 값은 유일해야합니다. 
- name(스테이지 이름) 필드를 null로 설정하면 기본 스테이지로 생성됩니다. 기본 스테이지는 하나만 생성할 수 있습니다. 
- name 필드 값에 따라 스테이지 URL이 변경됩니다.
  - 스테이지 URL 포맷: {regionCode}-{apigwServiceId}-{stageName}.api.nhncloudservice.com



#### 응답

[Response]

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
    "stageDescription": "alpha환경 스테이지",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomUrl": null,
    "backendEndpointUrl": "https://backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createddAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | 스테이지 영역 |
|stage.regionCode       |Enum    |[API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode)                |
|stage.apigwServiceId   |String  |API Gateway 서비스 ID  |
|stage.stageId          |String  |스테이지 ID             |
|stage.stageName        |String  |스테이지 이름             |
|stage.stageUrl         |String  |스테이지 URL            |
|stage.stageCustomUrl   |String  |스테이지 사용자 정의 URL   |
|stage.stageDescription |String  |스테이지 설명             |
|stage.backendEndpointUrl      |String  |백엔드 엔드포인트 URL       |
|stage.resourceUpdatedAt|DateTime|최근 스테이지 리소스 가져오기 수행 일시 |
|stage.createdAt        |DateTime|스테이지 생성일시           |
|stage.updatedAt        |DateTime|스테이지 수정일시           |

### 스테이지 수정 
- 스테이지의 백엔드 엔드포인트 URL과 설명을 수정할 수 있습니다.
- 스테이지 이름은 변경할 수 없습니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |


[Request Body]
``` json
{
  "backendEndpointUrl": "https://v2.backend.com",
  "description": "alpha 스테이지 v2"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| description | String | 선택 | 없음 | 최대 200자  | 스테이지 설명 |
| backendEndpointUrl | String | 필수 | 없음 | 최대 150자, URL형식  | 백엔드 엔드포인트 URL |


#### 응답

[Response]

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
    "stageDescription": "alpha 스테이지 v2",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomUrl": null,
    "backendEndpointUrl": "https://v2.backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createdAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | 스테이지 영역 |
|stage.regionCode       |Enum    |[API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode)                |
|stage.apigwServiceId   |String  |API Gateway 서비스 ID  |
|stage.stageId          |String  |스테이지 ID             |
|stage.stageName        |String  |스테이지 이름             |
|stage.stageUrl         |String  |스테이지 URL            |
|stage.stageCustomUrl   |String  |스테이지 사용자 정의 URL   |
|stage.stageDescription |String  |스테이지 설명             |
|stage.backendEndpointUrl      |String  |백엔드 엔드포인트 URL       |
|stage.resourceUpdatedAt|DateTime|최근 스테이지 리소스 가져오기 수행 일시 |
|stage.createdAt        |DateTime|스테이지 생성일시           |
|stage.updatedAt        |DateTime|스테이지 수정일시           |


### 스테이지 삭제
- 스테이지를 삭제합니다.
- 삭제하려는 스테이지가 사용량 계획에 연결된 경우 삭제가 불가합니다. 사용량 계획에서 스테이지 연결해제 후 삭제해주세요.
- 삭제된 스테이지는 복구가 불가합니다.

#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

#### 응답

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


## 스테이지 리소스 목록 조회 
* 스테이지에 등록된 리소스 목록을 가져옵니다. 스테이지 리소스 플러그인을 포함합니다.
* 스테이지 리소스 플러그인에 대한 자세한 내용은 [스테이지 리소스 플러그인]()을 참조합니다.


#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| GET  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |


#### 응답

[Response]
``` json
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |스테이지 리소스 목록 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |스테이지 리소스 메서드의 HTTP Method 타입               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[스테이지 플러그인 타입 참고]()                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |String  |[스테이지 플러그인 타입]()별 설정 Json의 문자열             |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정일시                         |



### 스테이지에 리소스 가져오기
* API Gateway 서비스 > 리소스에 등록된 리소스를 스테이지 리소스로 가져옵니다. 
* 리소스를 가져오면 스테이지 리소스, 스테이지 리소스 플러그인는 모두 새로 생성됩니다. 
* 기존 리소스 경로,메서드에 설정된 스테이지 리소스 플러그인의 설정 값은 그대로 유지됩니다. 


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |


#### 응답

[Response]
``` json
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |스테이지 리소스 목록 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |스테이지 리소스 메서드의 HTTP Method 타입               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[스테이지 플러그인 타입 참고]()                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |String  |[스테이지 플러그인 타입]()별 설정 Json의 문자열             |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정일시                         |



### 스테이지 리소스 플러그인 설정
* 특정 스테이지 리소스에 스테이지 리소스 플러그인을 설정합니다.
* 스테이지 리소스 플러그인에 대한 자세한 정보는 [스테이지 리소스 플러그인]()을 참고합니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources/{stageResourceId} |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |
| stageResourceId | String | 필수 | 없음 | 없음 | 스테이지 리소스 ID |


[Request Body]

``` json
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| customBackendEndpointUrl | String | 선택 | 없음 | 최대 150자, URL형식 | 백엔드 엔드포인트 재정의 URL |
| stageResourcePluginList | List | 선택 | 없음 | 없음 | 스테이지 리소스 플러그인 목록 영역 |
| stageResourcePluginList[0] | Object | 필수 | 없음 | 없음 | 스테이지 리소스 플러그인 별 Json형식의 객체<br>[스테이지 리소스 플러그인 참고]() |



#### 응답

[Response]
``` json
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
      "customEndpointUrl": null,
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |스테이지 리소스 목록 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |스테이지 리소스 메서드의 HTTP Method 타입               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[스테이지 플러그인 타입 참고]()                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |String  |[스테이지 플러그인 타입]()별 설정 Json의 문자열             |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정일시                         |

## 스테이지 리소스 플러그인
* 스테이지의 리소스마다 접근 제한, 인증, 사용량 제어등의 기능을 플러그인 형태로 설정할 수 있습니다. 
* 플러그인은 상위에서 설정하면 하위 모든 메서드에 일괄 적용되며, 하위 경로/메서드에서 재정의할 수 있습니다. 
* [예시]: 플러그인 설정 재정의
  ```
  /
    /members
      - GET
      - POST
  ```
  * 설정 
    1. 루트(/) 리소스 경로에 요청 수 제한을 초당 100개로 제한
    2. POST 리소스 메서드는 요청 수 제한을 초당 10개로 제한 
  * 동작 결과 
    - GET /members는 루트(/)에 설정된 요청 수 제한의 초당 100개로 제한이 적용됩니다.
    - POST /members는 루트(/)에 설정된 요청 수 제한의 초당 100개 제한이 무시되고, 초당 10개로 제한으로 적용됩니다.

* 리소스에 따라 설정 가능한 플러그인

| 리소스 타입 | 설정 가능한 플러그인 목록 | 
| --- | --- |
| 루트(/) 리소스 경로 |IP ACL, 인증(JWT 또는 HMAC 중 하나), 사전 호출 API, 요청 수 제한, API Key |
| 리소스 경로 |백엔드 엔드포인트 URL 재정의, 사전 호출 API, API Key |
| 리소스 메서드  |백엔드 엔드포인트 URL 재정의, 사전 호출 API, 요청 수 제한, API Key |


#### IP ACL 
* IP ACL을 통해 지정된 클라이언트 IP에 대해 API Gateway 요청을 허용/거부할 수 있습니다.
* 루트(/) 리소스 경로에만 설정 할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.

``` json
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | IP_ACL | [플러그인 타입]() 중 IP_ACL 참고 |
| pluginConfigJson | Object | 필수 |  |  | IP ACL 플러그인 설정 영역 |
| pluginConfigJson.isPermit | Boolean | 필수 | false | true, false | false로 설정하면 설정된 IP/CIDR에 대해 요청을 거부하고, true로 설정하면 설정된 IP/CIDR만 요청을 허용합니다.  |
| pluginConfigJson.ipAclList | List | 필수 |  | 최대 100개 | 요청을 허용/거부할 IP 또는 CIDR 목록 영역 |
| pluginConfigJson.ipAclList[0].ipCidrAddress | String | 필수 | 없음 | IP 또는 CIDR 형식 | IP 또는 CIDR을 설정합니다. |
| pluginConfigJson.ipAclList[0].description | String | 필수 | 없음 | 최대 200자 | 설명을 설정합니다. |


#### HMAC
* HMAC 서명 검증을 통해 클라이언트 요청의 변조를 검증하기 위한 설정입니다. 
* 루트(/) 리소스 경로에만 설정 할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.
* HMAC 인증은 JWT 인증과 동시에 설정이 불가합니다. 
* 서명에 사용하는 비밀키를 설정합니다.
* 시간 차로 발생하는 검증 실패를 방지하기 위한 검증 유효 시간을 설정합니다.
* 요청에 필수로 포함되어야하는 헤더 목록을 설정합니다.

```
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | HMAC | [플러그인 타입]() 중 HMAC 참고 |
| pluginConfigJson | Object | 필수 |  |  | HMAC 플러그인 설정 영역 |
| pluginConfigJson.secretKey | String | 필수 | 없음 | 없음 | 서명에 사용되는 비밀키를 설정합니다. 최소 32바이트 이상 문자열로 설정하는 것을 권장합니다.|
| pluginConfigJson.clockSkewSeconds | Integer | 필수 | 0 | 0~86400 | 요청 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.enforceHeaders | Array | 필수 | [] |  | 필수 검증 헤더의 문자열 배열을 입력합니다. |
| pluginConfigJson.enforceHeaders[0] | String | 필수 | 없음 | | 필수 검증 헤더의 문자열 배열을 입력합니다. |


#### JWT 
* JWT 토큰의 서명과 요청 클레임을 검증하기 위한 설정입니다.
* 루트(/) 리소스 경로에만 설정 할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.
* JWT 인증은 HMAC 인증과 동시에 설정이 불가합니다.
* 서명 검증을 위한 토큰 암호화 알고리즘과 암호화 알고리즘 방식에 따른 비밀키 혹은 공개키를 설정합니다.
* 요청 클레임의 값, 필수 여부 검증을 위한 클레임 검증 조건을 설정합니다. 
* 시간 차로 발생하는 검증 실패를 방지하기 위한 검증 유효 시간을 설정합니다.

* **암호화 알고리즘 HS256** 
``` json
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [플러그인 타입]() 중 JWT 참고 |
| pluginConfigJson | Object | 필수 |  |  | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | HS256 | HS256 | [JWT > 암호화 알고리즘]() 참고  |
| pluginConfigJson.hs256.secretKey | String | 필수 | 없음 | 없음 | 서명에 사용되는 비밀키를 설정합니다. 최소 32바이트 이상 문자열로 설정하는 것을 권장합니다.|
| pluginConfigJson.clockSkew | Integer | 필수 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition.iss | Object | 필수 |  |  | iss 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.iss.value | Array | 필수 | [] | 없음 |  iss 요청 클레임의 값 중 허용할 클레임 값을 문자열 배열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.value[0] | String | 필수 | 없음 | 없음 |  iss 요청 클레임의 값 중 허용할 문자열을 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.dataType | String | 필수 | Array | Array | iss 클레임의 데이터 타입을 설정합니다. Array만 유효합니다. <br/> [JWT > 클레임 데이터 타입]() 참고 |
| pluginConfigJson.claimValidationCondition.iss.required | Boolean | 필수 | false | true, false | iss 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.validate | Boolean | 필수 | false | true, false | iss 요청 클레임 값의 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud | Object | 필수 |  |  | aud 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.aud.value | Array | 필수 | [] | 없음 |  aud 요청 클레임의 값 중 허용할 클레임 값을 문자열 배열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.value[0] | String | 필수 | 없음 | 없음 |  aud 요청 클레임의 값 중 허용할 문자열을 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.dataType | String | 필수 | Array | Array | aud 클레임의 데이터 타입을 설정합니다. Array만 유효합니다. <br/> [JWT > 클레임 데이터 타입]() 참고 |
| pluginConfigJson.claimValidationCondition.aud.required | Boolean | 필수 | false | true, false | aud 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.validate | Boolean | 필수 | true | true | aud 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.sub | Object | 필수 | 없음 |  | sub 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.sub.value | String | 필수 | "" | 없음 |  sub 요청 클레임의 값 중 허용할 클레임 문자열 값을 설정합니다. |
| pluginConfigJson.claimValidationCondition.sub.dataType | String | 필수 | String | String | sub 클레임의 데이터 타입을 설정합니다. String만 유효합니다.<br/> [JWT > 클레임 데이터 타입]() |
| pluginConfigJson.claimValidationCondition.sub.required | Boolean | 필수 | false | true, false | sub 요청 클레임 값의 필수 검증 여부를 설정합니다. <br/> validate 필드값이 true인 경우, requried는 반드시 true로 설정되어야합니다.  |
| pluginConfigJson.claimValidationCondition.sub.validate | Boolean | 필수 | false | true, false | sub 요청 클레임 값의 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti | Object | 필수 |  |  | jti 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.jti.value | String | 필수 | "" | 없음 | jti 클레임은 허용할 검증 값 설정을 요구하지 않으므로 빈 문자열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti.dataType | String | 필수 | String | String | jti 클레임의 데이터 타입을 설정합니다. <br/> [JWT > 클레임 데이터 타입]() 참고|
| pluginConfigJson.claimValidationCondition.jti.required | Boolean | 필수 | false | true, false | jti 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti.validate | Boolean | 필수 | false | false | jti 요청 클레임 값의 검증 여부를 설정합니다. false만 유효합니다.|
| pluginConfigJson.claimValidationCondition.exp | Object | 필수 | 없음 |  | exp 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.exp.value | String | 필수 | "" | 없음 | exp 클레임은 허용할 검증 값 설정을 요구하지 않으므로 빈 문자열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.exp.dataType | NumericDate | 필수 | String | NumericDate | exp 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/> [JWT > 클레임 데이터 타입]() 참고 |
| pluginConfigJson.claimValidationCondition.exp.required | Boolean | 필수 | false | true, false | exp 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.exp.validate | Boolean | 필수 | true | true | exp 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.iat | Object | 필수 |  |  | iat 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.iat.value | String | 필수 | "" | 없음 | iat 클레임은 허용할 검증 값 설정을 요구하지 않으므로 빈 문자열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.iat.dataType | NumericDate | 필수 | String | NumericDate | iat 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/> [JWT > 클레임 데이터 타입]() 참고 |
| pluginConfigJson.claimValidationCondition.iat.required | Boolean | 필수 | false | true, false | iat 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.iat.validate | Boolean | 필수 | true | true | iat 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.nbf | Object | 필수 | 없음 |  | nbf 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.nbf.value | String | 필수 | "" | 없음 | nbf 클레임은 허용할 검증 값 설정을 요구하지 않으므로 빈 문자열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.nbf.dataType | NumericDate | 필수 | String | NumericDate | nbf 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/> [JWT > 클레임 데이터 타입]() 참고|
| pluginConfigJson.claimValidationCondition.nbf.required | Boolean | 필수 | false | true, false | nbf 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.nbf.validate | Boolean | 필수 | true | true | nbf 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |

* **암호화 알고리즘 RS256: (PEM 형식의 공개키 설정 방식)** 

``` json
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
      ...생략
    }
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [플러그인 타입]() 중 JWT 참고 |
| pluginConfigJson | Object | 필수 |  |  | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | RS256 | RS256 | [JWT > 암호화 알고리즘]() 참고  |
| pluginConfigJson.rs256.publicKeyType | String | 필수 | 없음 | RSA_PUBLIC_KEY | PEM 형식의 공개키 설정 [JWT > RS256 암호화 알고리즘 > Public Key Type]() 참고 |
| pluginConfigJson.rs256.rsaPublicKey | String | 필수 | 없음 | 없음 | PEM 형식의 공개키 값을 설정합니다.  개행 문자(\n)를 포함하여 입력해야합니다. |
| pluginConfigJson.clockSkew | Integer | 필수 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition | Object | 필수 |  |  | 클레임 검증 조건 영역 (암호화 알고리즘: HS256의 claimValidationCondition 필드 설명과 동일합니다.) |


* **암호화 알고리즘 RS256: (Json Web Key Sets URI 공개키 설정 방식)** 

* 암호화 알고리즘: RS256 (JSON Web Key URL)

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
        ...생략
    }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [플러그인 타입]() 중 JWT 참고 |
| pluginConfigJson | Object | 필수 |  |  | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | RS256 | RS256 | [JWT > 암호화 알고리즘]() 참고  |
| pluginConfigJson.rs256.publicKeyType | String | 필수 | 없음 | JWKS_URI | JWKS(Json Web Key Sets) URI 형식으로 공개키를 설정합니다. [JWT > RS256 암호화 알고리즘 > Public Key Type]() 참고 |
| pluginConfigJson.rs256.rsaPublicKey | String | 필수 | 없음 | 없음 | Json Web Key Set URI를 설정합니다. |
| pluginConfigJson.clockSkew | Integer | 필수 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition | Object | 필수 |  |  | 클레임 검증 조건 영역 (암호화 알고리즘: HS256의 claimValidationCondition 필드 설명과 동일합니다.) |


#### 사전 호출 API 
* 사전 호출 API는 백엔드 엔드포인트를 호출하기 전에 사용자가 지정한 API를 호출하여 호출의 응답 코드가 200 OK인 경우에만, 백엔드 엔드포인트 호출하도록 합니다.
* 모든 리소스 경로, 메서드에 설정할 수 있습니다. 


``` json
{
  "pluginType": "PRE_API",
  "pluginConfigJson": {
    "httpMethod": "POST",
    "url": "http://auth.check.com",
    "cacheTtl": 0
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | PRE_API | [플러그인 타입]() 중 PRE_API 참고 |
| pluginConfigJson | Object | 필수 |  |  | 사전 호출 API 플러그인 설정 영역 |
| pluginConfigJson.httpMethod | Enum | 필수 | 없음 | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [사전 호출 API > HttpMethod]() 참고  |
| pluginConfigJson.url | String | 필수 | 없음 | URL형식 | 사전 호출 API의 URL을 입력합니다. |
| pluginConfigJson.cacheTtl | Integer | 필수 | 없음 | 0~86400 | 사전 호출 API의 응답 상태 코드의 캐시 시간을 설정합니다. <br/>응답 상태 코드가 200 OK인 경우에만 설정된 시간 동안 캐시되며, 캐시된 경우에는 사전 호출 API를 호출하지 않습니다. |

### 요청 수 제한 
* 초당 요청 수를 제한합니다. 
* 루트(/) 리소스 경로와 리소스 메서드에 설정할 수 있습니다. 
* 요청 제한 키를 설정하여, IP, 헤더, 경로 변수 값마다 요청 수 제한을 설정할 수 있습니다.

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | RATE_LIMIT | [플러그인 타입]() 중 RATE_LIMIT 참고 |
| pluginConfigJson | Object | 필수 |  |  | 요청 수 제한 플러그인 설정 영역 |
| pluginConfigJson.keyType | Enum | 필수 | 없음 | DEFAULT, IP, HEADER, PATH_VARIABLE | [요청 수 제한 > 제한 키]() 참고  |
| pluginConfigJson.extraKeyValue | String | 조건부 필수 | 없음 | 없음 | keyType이 HEADER인 경우, 헤더 이름을 반드시 설정해야합니다.<br/> keyType이 PATH_VARIABLE인 경우, ${request.path.variable-name} 형식의 경로 변수를 반드시 설정해야 합니다. |
| pluginConfigJson.requestPerSec | Integer | 필수 | 없음 | 1~5000 | 초당 최대 요청 가능한 수를 설정합니다. |


## API Key 검증

* API 호출시 API Key가 유효한지 검증하고, 지정된 사용량 계획의 사용량을 초과했는지 검증합니다. 
* 루트(/) 리소스 경로와 리소스 메서드에 설정할 수 있습니다. 


```json
{
  "pluginType": "API_KEY",
  "pluginConfigJson": {
    "isActive": true
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | API_KEY | [플러그인 타입]() 중 API_KEY 참고 |
| pluginConfigJson | Object | 필수 |  |  | API Key 플러그인 설정 영역 |
| pluginConfigJson.isActive | Boolean | 필수 | 없음 | true | API Key 검증 여부를 설정합니다. 반드시 true로 설정해야합니다. |