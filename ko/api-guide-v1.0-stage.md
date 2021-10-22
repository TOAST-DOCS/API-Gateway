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
      "stageId": "73e9b399-6db7-4bc5-9c9f-6873c37fa4ec",
      "apigwServiceId": "o3jamslvip",
      "regionCode": "KR1",
      "stageName": "alpha",
      "stageDescription": "alpha 환경 스테이지",
      "stageUrl": "kr1-o3jamslvip-alpha.api.nhncloudservice.com",
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
- Swagger문서는 스테이지에 배포된 설정 기준이 아닌 현재 스테이지 설정을 기준으로 추출됩니다. 

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
    "stageId": "b17b5fc6-5d7a-4d7c-9fee-da709673dc96",
    "apigwServiceId": "o3jamslvip",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alpha환경 스테이지",
    "stageUrl": "kr1-o3jamslvip-alpha.api.nhncloudservice.com",
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
    "stageId": "b17b5fc6-5d7a-4d7c-9fee-da709673dc96",
    "apigwServiceId": "o3jamslvip",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alpha 스테이지 v2",
    "stageUrl": "kr1-o3jamslvip-alpha.api.nhncloudservice.com",
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
      "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
      "stageId": "d4e3c87d-fd2f-491f-90ee-8d56e1cdc09d",
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
          "stageResourcePluginId": "a1051eb4-525c-4108-9f92-781399859fae",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
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
          "stageResourcePluginId": "fb7dee06-1c76-41d8-ba3e-0d322bcbd036",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-xd06ax3zta.alpha-api.nhncloudservice.com/:",
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



### 스테이지에 리소스 가져오기
* API Gateway 서비스 > 리소스에 등록된 리소스를 스테이지 리소스로 가져옵니다. 
* 리소스를 가져오면 스테이지 리소스 ID, 스테이지 리소스 플러그인 ID가 모두 새로 생성됩니다. 
* 리소스 가져오기 후 기존 리소스 경로/메서드가 유지된 경우, 기존 리소스 플러그인 설정은 그대로 유지됩니다.


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
      "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
      "stageId": "d4e3c87d-fd2f-491f-90ee-8d56e1cdc09d",
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
          "stageResourcePluginId": "a1051eb4-525c-4108-9f92-781399859fae",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
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
          "stageResourcePluginId": "fb7dee06-1c76-41d8-ba3e-0d322bcbd036",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-xd06ax3zta.alpha-api.nhncloudservice.com/:",
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
  "customEndpointUrl": "http://custom.backendpoint.com",
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
      "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
      "stageId": "d4e3c87d-fd2f-491f-90ee-8d56e1cdc09d",
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
          "stageResourcePluginId": "a1051eb4-525c-4108-9f92-781399859fae",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
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
          "stageResourcePluginId": "fb7dee06-1c76-41d8-ba3e-0d322bcbd036",
          "stageResourceId": "5a02d433-caa6-411f-9e8f-4d5f99470d0c",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-xd06ax3zta.alpha-api.nhncloudservice.com/:",
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
* 스테이지의 리소스마다 접근 제한, 인증, 사용량 제어와 같은 설정을 플러그인 형태로 설정할 수 있습니다. 
* 플러그인은 상위에서 설정하면 하위 모든 메서드에 일괄 적용되며, 하위 경로/메서드에서 재정의할 수 있습니다. 
  * 재정의는 상위에서 설정한 값은 무시하고, 하위에서 
  재정의한 값으로 동작됨을 의미합니다.
* [예시] 
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
    - POST /members는 루트(/)에 설정된 초당 100개 제한이 무시되고, 초당 10개로 제한으로 적용됩니다.

* 리소스에 따라 설정 가능한 플러그인

| 리소스 타입 | 설정 가능한 플러그인 목록 | 
| --- | --- |
| 루트(/) 리소스 경로 |IP ACL, 인증(JWT 또는 HMAC 중 하나), 사전 호출 API, 요청 수 제한, API Key |
| 리소스 경로 |백엔드 엔드포인트 URL 재정의, 사전 호출 API, API Key |
| 리소스 메서드  |백엔드 엔드포인트 URL 재정의, 사전 호출 API, 요청 수 제한, API Key |