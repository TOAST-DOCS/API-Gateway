## 스테이지 배포


### 스테이지 배포
- 현재 스테이지 리소스와 설정을 API Gateway 서비스에 배포합니다. 
- 변경된 설정 정보가 없는 경우, 스테이지 배포 요청이 실패합니다.
- 스테이지 배포가 실패된 경우, 기존 성공한 스테이지 배포 설정으로 롤백됩니다.
- 스테이지 배포 요청 후, 스테이지 배포 성공 여부는 [최근 스테이지 배포 결과 조회]()에서 확인할 수 있습니다. 

#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[Request Body]
```json
{
  "deployDescription": "deploy description"
}
```
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| deployDescription | String | 선택 | 없음 | 최대 200자 | 배포 설명 |


#### 응답

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### 최근 스테이지 배포 결과 조회 
- [스테이지 배포]()의 결과를 조회할 수있습니다. 
- 스테이지 배포 요청 이후 배포 결과가 업데이트되기 까지 최대 1분 정도까지 소요될 수 있습니다. 


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/latest |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |


#### 응답

[Response]

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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|latestStageDeployResult              |Object  | 스테이지 배포 결과 영역                                        |
|latestStageDeployResult.deployId       |String    | 배포 ID |
|latestStageDeployResult.stageId   |String  | 스테이지 ID  |
|latestStageDeployResult.deployDescription        |String  | 배포 설명  |
|latestStageDeployResult.deployStatus        |Enum  | [스테이지 배포 > 배포 상태]() 참고 |
|latestStageDeployResult.isBase         |String  | 현재 스테이지의 설정 기반 여부 |
|latestStageDeployResult.deployedAt          |DateTime  | 배포 요청 일시 |
|latestStageDeployResult.rollbackAt   |DateTime  | 스테이지 되돌리기 요청 일시 |
|latestStageDeployResult.stageResourceList      |List    |스테이지 리소스 목록 영역                             |
|latestStageDeployResult.stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|latestStageDeployResult.stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|latestStageDeployResult.stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|latestStageDeployResult.stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|latestStageDeployResult.stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|latestStageDeployResult.stageResourceList[0].methodType             |Enum    |스테이지 리소스 메서드의 HTTP Method 타입               |
|latestStageDeployResult.stageResourceList[0].methodName             |String  |메서드 이름                                     |
|latestStageDeployResult.stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|latestStageDeployResult.stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성일시                              |
|latestStageDeployResult.stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정일시                              |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[스테이지 플러그인 타입 참고]()                        |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |String  |[스테이지 플러그인 타입]()별 설정 Json의 문자열             |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성일시                         |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정일시                         |

### 스테이지 배포 이력 삭제
- 스테이지 배포 이력을 삭제합니다.
- 현재 스테이지의 기반 배포 이력 (isBase가 true인 경우)과 현재 API Gateway 서비스 배포된 이력은 삭제할 수 없습니다.

#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId}/rollback |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |
| deployId | String | 필수 | 없음 | 없음 | 삭제할 배포 ID |

#### 응답

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### 스테이지 배포 이력 조회 
- 배포 성공 상태의 스테이지 배포 이력을 조회합니다. 

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                        |
|paging.page                          |Integer | 현재 페이지                                        |
|paging.limit                         |Integer | 페이지 당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|stageDeployHistoryList        |List    | 스테이지 배포 이력 목록 영역 |
|stageDeployHistoryList[0].deployId       |String    | 배포 ID |
|stageDeployHistoryList[0].stageId   |String  | 스테이지 ID  |
|stageDeployHistoryList[0].deployDescription        |String  | 배포 설명  |
|stageDeployHistoryList[0].isBase         |String  | 현재 스테이지의 설정 기반 여부 |
|stageDeployHistoryList[0].deployedAt          |DateTime  | 배포 요청 일시 |
|stageDeployHistoryList[0].rollbackAt   |DateTime  | 스테이지 되돌리기 요청 일시 |


### 스테이지 되돌리기
- 배포된 스테이지 설정 이력으로 현재 스테이지 설정을 되돌립니다.  
- 스테이지 되돌리기를 하면 현재 스테이지 설정은 모두 삭제되므로 유의하시기 바랍니다.  
- 되돌려진 스테이지 설정을 API Gateway 서비스에 적용하려면 스테이지를 배포해야합니다.
- 배포 실패 상태의 배포 이력으로는 되돌리기를 할 수 없습니다.

#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId} |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |
| deployId | String | 필수 | 없음 | 없음 | 되돌릴 배포 ID |

#### 응답

[Response]

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