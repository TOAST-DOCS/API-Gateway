## Application Service > API Gateway > API v1.0 가이드

NHN Cloud API Gateway에서 제공하는 Public API v1.0을 설명합니다.

## API 공통 정보

### 도메인

| 이름      | 리전 | 도메인                                            |
|---------|-----|------------------------------------------------|
| API 도메인 | 한국(판교) 리전 | https://kr1-apigateway.api.gov-nhncloudservice.com |
| API 도메인 | 한국(평촌) 리전 | https://kr2-apigateway.api.gov-nhncloudservice.com |

### 사전 준비

API를 사용하려면 앱 키(Appkey)가 필요합니다.
앱 키는 콘솔 오른쪽 위의 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

### 요청 공통 정보

#### Path Parameter

모든 API는 앱 키를 Path Parameter로 지정해야 합니다.
* 예) /v1.0/appkeys/**{appKey}**/**

| 이름     | 설명                    |
| ------ | --------------------- |
| appKey | 콘솔에서 발급받은 앱 키(Appkey) |

### 응답 공통 정보

#### 헤더
모든 API 요청에 대해서 **200 OK**로 응답합니다. 자세한 응답 결과는 다음의 예와 같이 응답 본문의 헤더를 참고합니다.

[성공: Response Body]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header               | Object  | 헤더 영역  |
| header.isSuccessful  | Boolean | 성공 여부  |
| header.resultCode    | Integer | 결과 코드  |
| header.resultMessage | String  | 결과 메시지 |

[실패: Response Body]

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

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| errorList            | List  | 오류 목록 영역  |
| errorList[0].resultCode  | Integer | 오류 코드  |
| errorList[0].errorProperty | String | 오류 프로퍼티(모델) |
| errorList[0].errorField | String  | 오류 상세 필드 |
| errorList[0].errorMessage | String  | 오류 메시지 |

* 잘못된 API 요청을 한 경우, errorList 필드에 자세한 오류 원인과 필드 정보가 응답됩니다.


## API Gateway 서비스

### API Gateway 서비스 목록 조회 
- API Gateway 서비스 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | 필수 | 없음 | KR1 | [API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고 |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

#### 응답

[Response]

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
         "apigwDomain":"api.gov-nhncloudservice.com",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                        |
|paging.page                          |Integer | 현재 페이지                                        |
|paging.limit                         |Integer | 페이지당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|apigwServiceList                     |List    | API Gateway 서비스 목록 영역                         |
|apigwServiceList[0].apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwServiceList[0].apigwServiceAlias   |String  | API Gateway 서비스 별칭               |
|apigwServiceList[0].apigwServiceId      |String  | API Gateway 서비스 ID                  |
|apigwServiceList[0].apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드](./enum-code-gov/#api-gateway_1) 참고|
|apigwServiceList[0].appKey              |String  | AppKey                                        |
|apigwServiceList[0].dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwServiceList[0].apigwServiceDescription         |String  | API Gateway 서비스 설명                                        |
|apigwServiceList[0].apigwServiceName                |String  | API Gateway 서비스 이름                                        |
|apigwServiceList[0].regionCode          |Enum    | [API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고 |
|apigwServiceList[0].serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwServiceList[0].createdAt           |DateTime| API Gateway 서비스 생성 일시                                      |
|apigwServiceList[0].updatedAt           |DateTime| API Gateway 서비스 수정 일시                                      |


### 단일 API Gateway 서비스 조회 
- API Gateway 서비스 ID로 단일 API Gateway 서비스를 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |


#### 응답

[Response]

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
    "apigwDomain": "api.gov-nhncloudservice.com",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object  | API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  | API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  | API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드](./enum-code-gov/#api-gateway_1) 참고 |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwService.apigwServiceDescription         |String  | API Gateway 서비스 설명                                        |
|apigwService.apigwServiceName                |String  | API Gateway 서비스 이름                                        |
|apigwService.regionCode          |Enum    |[API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고|
|apigwService.serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime| API Gateway 서비스 생성 일시                                      |
|apigwService.updatedAt           |DateTime| API Gateway 서비스 수정 일시                                      |



### API Gateway 서비스 생성
- API Gateway 서비스를 생성합니다.
- API Gateway 서버가 생성될 리전을 선택할 수 있습니다. 현재는 한국(판교) 리전만 지원합니다.
- API Gateway 서비스를 생성하면 API Gateway 서비스 ID가 자동 발급됩니다.


#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services |

[Request Body]

```json
{
  "regionCode": "KR1",
  "apigwServiceName": "service name",
  "apigwServiceDescription": "service description"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | 필수 | 없음 | KR1 | [API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고|
| apigwServiceName | String | 필수 | 없음 | 최대 50자  | API Gateway 서비스 이름 |
| apigwServiceDescription | String | 선택 | 없음 | 최대 200자  | API Gateway 서비스 설명 |


#### 응답

[Response]

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
    "apigwDomain": "api.gov-nhncloudservice.com",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    | API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  | API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  | API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드](./enum-code-gov/#api-gateway_1) 참고 |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwService.apigwServiceDescription         |String  | 서비스 설명                                        |
|apigwService.apigwServiceName    |String  | API Gateway 서비스 이름                                        |
|apigwService.regionCode          |Enum    | [API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고|
|apigwService.serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime| API Gateway 서비스 생성 일시                                      |
|apigwService.updatedAt           |DateTime| API Gateway 서비스 수정 일시                                      |


### API Gateway 서비스 수정
- API Gateway 서비스의 이름과 설명을 수정합니다.

#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| PUT  | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |


[Request Body]

```json
{
  "apigwServiceName": "update service name",
  "apigwServiceDescription": "test of api gateway service"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceName | String | 필수 | 없음 | 최대 50자  | API Gateway 서비스 이름 |
| apigwServiceDescription | String | 선택 | 없음 | 최대 200자  | API Gateway 서비스 설명 |


#### 응답

[Response]

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
    "apigwDomain": "api.gov-nhncloudservice.com",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    |API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  |API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  |API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  |API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    |[API Gateway 서비스 타입 Enum 코드](./enum-code-gov/#api-gateway_1) 참고|
|apigwService.appKey              |String  |AppKey                                        |
|apigwService.dedicatedId         |String  |전용 API Gateway 서비스의 ID                        |
|apigwService.apigwServiceDescription         |String  |서비스 설명                                        |
|apigwService.apigwServiceName                |String  |서비스 이름                                        |
|apigwService.regionCode          |Enum    |[API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고|
|apigwService.serverGroupId       |String  |서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime|서비스 생성 일시                                      |
|apigwService.updatedAt           |DateTime|서비스 수정 일시                                      |

### API Gateway 서비스 삭제
- API Gateway 서비스를 삭제합니다.  
- API Gateway 서비스를 삭제하면 모든 스테이지가 삭제됩니다.  
- 삭제하려는 API Gateway 서비스의 스테이지가 사용량 계획과 연결된 경우, 삭제할 수 없습니다. 삭제하려면 사용량 계획에 연결된 스테이지를 모두 연결 해제한 후 삭제해 주세요.
- 삭제된 API Gateway 서비스는 복구할 수 없으므로 주의해 주세요.

#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |

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

## 리소스

### 리소스 조회

- 리소스 목록을 조회합니다.

#### 요청

[URI]

| 메서드 | URI | 
| --- | --- | 
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |

#### 응답

[Response]

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

| 필드                                                     | 타입       | 설명                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | 리소스 목록 영역                                      |
| resourceList[0].resourceId                             | String   | 리소스 ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway 서비스 ID                             |
| resourceList[0].path                                   | String   | 리소스 경로                                         |
| resourceList[0].createdAt                              | DateTime | 리소스 생성 일시                                       |
| resourceList[0].updatedAt                              | DateTime | 리소스 수정 일시                                       |
| resourceList[2].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourceList[2].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[2].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[2].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[2].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[2].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[2].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고    |
| resourceList[2].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고                   |
| resourceList[2].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성 일시                                  |
| resourceList[2].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정 일시                                  |

### 리소스 경로와 메서드 생성
- 여러 개의 리소스 경로와 메서드를 생성하고, 생성과 동시에 플러그인을 설정할 수 있습니다.
- 리소스 메서드는 선택 입력입니다. 생성된 리소스 경로의 하위에 메서드를 추가하려면 [리소스 메서드 생성](./api-guide-v1.0-gov/#_23) API를 사용해야합니다.
- 리소스 메서드에는 HTTP 또는 MOCK 플러그인 중 반드시 하나가 설정되어야 합니다. HTTP와 MOCK 플러그인을 동시에 설정할 수 없습니다.
- 생성된 리소스 경로는 수정이 불가합니다.
- pathPluginList 필드에 정의된 리소스 경로 플러그인은 해당 경로의 하위 메서드에 적용되는 플러그인 목록입니다.

#### 요청

[URI]

| 메서드 | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |


[Request Body]

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| resourcePathList | List | 필수 | 없음 | 없음  | 리소스 경로 목록 |
| resourcePathList[0] | Object | 필수 | 없음 | 없음  | 리소스 경로 영역 |
| resourcePathList[0].path | Object | 필수 | 없음 | 영문자, 숫자, 경로 변수, 제한된 문자(. + - /)로 구성된 유효한 경로  | 리소스 경로 |
| resourcePathList[0].pathPluginList | List | 선택 | 없음 | 없음 | 리소스 경로 플러그인 목록 |
| resourcePathList[0].pathPluginList[0] | Object | 선택 | 없음 | 없음 | 리소스 경로 플러그인 영역 |
| resourcePathList[0].pathPluginList[0].pluginType | Enum | 필수 | 없음 | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 중 리소스 경로에 설정 가능한 플러그인 타입 |
| resourcePathList[0].pathPluginList[0].pluginConfigJson | Object | 필수 | 없음 | 없음 | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고.|
| resourcePathList[0].methodList | List | 선택 | 없음 | 없음 | 리소스 경로 하위의 메서드 목록 |
| resourcePathList[0].methodList[0] | Object | 선택 | 없음 | 없음 | 리소스 경로 하위의 메서드 영역 |
| resourcePathList[0].methodList[0].methodType | Enum | 필수 | 없음 | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourcePathList[0].methodList[0].methodName | String | 필수 | 없음 | 최대 50자 | 메서드 이름 |
| resourcePathList[0].methodList[0].methodDescription | String | 선택 | 없음 | 최대 200자 | 메서드 설명 |
| resourcePathList[0].methodList[0].methodPluginList | List | 필수 | 없음 | 없음 | 리소스 메서드 플러그인 목록 |
| resourcePathList[0].methodList[0].methodPluginList[0] | Object | 필수 | 없음 | 없음 | 리소스 메서드 플러그인 영역, 'HTTP' 또는 'MOCK' 중 하나의 플러그인은 필수 입력 |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginType | Enum | 필수 | 없음 | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 중 리소스 메서드에 설정 가능한 플러그인 타입 |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginConfigJson | Object | 필수 | 없음 | 없음 | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고.|

#### 응답

[Response]

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

| 필드                                                     | 타입       | 설명                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | 리소스 목록 영역                                      |
| resourceList[1].resourceId                             | String   | 리소스 ID                                         |
| resourceList[1].apigwServiceId                         | String   | API Gateway 서비스 ID                             |
| resourceList[1].path                                   | String   | 리소스 경로                                         |
| resourceList[1].parentPath                             | String   | 부모 리소스 경로                                         |
| resourceList[1].createdAt                              | DateTime | 리소스 생성 일시                                       |
| resourceList[1].updatedAt                              | DateTime | 리소스 수정 일시                                       |
| resourceList[1].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourceList[1].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[1].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[1].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[1].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[1].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[1].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고    |
| resourceList[1].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고                   |
| resourceList[1].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성 일시                                  |
| resourceList[1].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정 일시                                  |


### 리소스 메서드 생성
- 생성된 리소스 경로의 하위에 리소스 메서드를 생성합니다.
- 리소스 메서드에는 HTTP 또는 MOCK 플러그인 중 반드시 하나가 설정되어야 합니다. HTTP와 MOCK 플러그인을 동시에 설정할 수 없습니다.

#### 요청

[URI]

| 메서드 | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/methods |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId | String | 필수    | 없음  | 없음    | 리소스 경로 ID |


[Request Body]

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| methodList | List | 필수 | 없음 | 없음 | 리소스 경로 하위의 메서드 목록 |
| methodList[0] | Object | 필수 | 없음 | 없음 | 리소스 경로 하위의 메서드 영역 |
| methodList[0].methodType | Enum | 필수 | 없음 | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| methodList[0].methodName | String | 필수 | 없음 | 최대 50자 | 메서드 이름 |
| methodList[0].methodDescription | String | 선택 | 없음 | 최대 200자 | 메서드 설명 |
| methodList[0].methodPluginList | List | 필수 | 없음 | 없음 | 리소스 메서드 플러그인 목록 |
| methodList[0].methodPluginList[0] | Object | 필수 | 없음 | 없음 | 리소스 메서드 플러그인 영역, 'HTTP' 또는 'MOCK' 중 하나의 플러그인은 필수 입력 |
| methodList[0].methodPluginList[0].pluginType | Enum | 필수 | 없음 | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 중 리소스 메서드에 설정 가능한 플러그인 타입 |
| methodList[0].methodPluginList[0].pluginConfigJson | Object | 필수 | 없음 | 없음 | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고.|

#### 응답

[Response]

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

| 필드                                                     | 타입       | 설명                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | 리소스 목록 영역                                      |
| resourceList[0].resourceId                             | String   | 리소스 ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway 서비스 ID                             |
| resourceList[0].path                                   | String   | 리소스 경로                                         |
| resourceList[0].parentPath                             | String   | 부모 리소스 경로                                         |
| resourceList[0].createdAt                              | DateTime | 리소스 생성 일시                                       |
| resourceList[0].updatedAt                              | DateTime | 리소스 수정 일시                                       |
| resourceList[0].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourceList[0].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[0].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[0].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성 일시                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정 일시                                  |


### 리소스 경로 플러그인 수정/삭제
- 리소스 경로 플러그인을 추가, 수정, 삭제합니다.
- 리소스 경로에 추가되지 않은 플러그인을 설정하면 플러그인이 추가됩니다.
- 리소스 경로에 추가된 플러그인을 설정하면 요청한 플러그인 설정으로 변경됩니다.
- delete 필드를 true로 설정하면, 요청한 플러그인 타입의 플러그인이 삭제됩니다. delete 필드가 true이면 pluginConfigJson 필드는 정의하지 않아도 됩니다.
- applyChildPath 필드를 true로 설정하면 리소스 경로 하위의 모든 경로와 메서드에 플러그인이 설정됩니다.
- applyChildPath와 delete 필드 모두를 true로 설정하면 리소스 경로 하위의 모든 경로와 메서드에 플러그인이 삭제됩니다.
- CORS 플러그인을 설정하면, 하위 메서드로 OPTIONS 메서드가 자동으로 생성됩니다. 만일 기존에 존재하는 OPTIONS 메서드가 있다면 삭제되고 대체되므로 주의해주세요.
- 리소스 경로에 설정 가능한 플러그인만 설정할 수 있습니다. 자세한 내용은 [리소스 플러그인](./api-guide-v1.0-gov/#_37)을 참고합니다.

#### 요청

[URI]

| 메서드 | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-paths/{resourceId} |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId | String | 필수    | 없음  | 없음    | 리소스 경로 ID |

[Request Body]

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pathPluginList | List | 선택 | 없음 | 없음 | 리소스 경로 플러그인 목록 |
| pathPluginList[0] | Object | 선택 | 없음 | 없음 | 리소스 경로 플러그인 영역 |
| pathPluginList[0].pluginType | Enum | 필수 | 없음 | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER,ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 중 리소스 경로에 설정 가능한 플러그인 타입 |
| pathPluginList[0].pluginConfigJson | Object | 조건부 필수 | 없음 | 없음 | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고, delete 필드가 false인 경우 필수 입력|
| pathPluginList[0].applyChildPath | Boolean | 선택 | false | true, false | 하위 경로와 메서드에 덮어쓰기 여부 |
| pathPluginList[0].delete | Boolean | 선택 | false | true, false | 플러그인 삭제 여부 |

#### 응답

[Response]

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

| 필드                                                     | 타입       | 설명                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | 리소스 목록 영역                                      |
| resourceList[0].resourceId                             | String   | 리소스 ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway 서비스 ID                             |
| resourceList[0].path                                   | String   | 리소스 경로                                         |
| resourceList[0].parentPath                             | String   | 부모 리소스 경로                                         |
| resourceList[0].createdAt                              | DateTime | 리소스 생성 일시                                       |
| resourceList[0].updatedAt                              | DateTime | 리소스 수정 일시                                       |
| resourceList[0].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourceList[0].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[0].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[0].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성 일시                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정 일시                                  |


### 리소스 메서드 정보와 플러그인 수정/삭제
- 리소스 메서드의 이름, 설명을 수정할 수 있습니다.
- 리소스 메서드 플러그인을 추가, 수정, 삭제합니다.
- 리소스 메서드에 추가되지 않은 플러그인을 설정하면 플러그인이 추가됩니다.
- 리소스 메서드에 추가된 플러그인을 설정하면 요청한 플러그인 설정으로 변경됩니다.
- delete 필드를 true로 설정하면, 요청한 플러그인 타입의 플러그인이 삭제됩니다. delete 필드가 true이면 pluginConfigJson 필드는 정의하지 않아도 됩니다.
- 리소스 메서드에 설정 가능한 플러그인만 설정할 수 있습니다. 자세한 내용은 [리소스 플러그인](./api-guide-v1.0-gov/#_37)을 참고합니다.

#### 요청

[URI]

| 메서드 | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-methods/{resourceId} |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId | String | 필수    | 없음  | 없음    | 리소스 메서드 ID |

[Request Body]

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| methodName | String | 필수 | 없음 | 최대 50자 | 메서드 이름 |
| methodDescription | String | 선택 | 없음 | 최대 200자 | 메서드 설명 |
| methodPluginList | List | 선택 | 없음 | 없음 | 리소스 메서드 플러그인 목록 |
| methodPluginList[0] | Object | 필수 | 없음 | 없음 | 리소스 메서드 플러그인 영역 |
| methodPluginList[0].pluginType | Enum | 필수 | 없음 | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 중 리소스 메서드에 설정 가능한 플러그인 타입 |
| methodPluginList[0].pluginConfigJson | Object | 조건부 필수 | 없음 | 없음 | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고, delete 필드가 false인 경우 필수 입력|
| methodPluginList[0].delete | Boolean | 선택 | false | 없음 | 플러그인 삭제 여부 |

#### 응답

[Response]

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

| 필드                                                     | 타입       | 설명                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | 리소스 목록 영역                                      |
| resourceList[0].resourceId                             | String   | 리소스 ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway 서비스 ID                             |
| resourceList[0].path                                   | String   | 리소스 경로                                         |
| resourceList[0].parentPath                             | String   | 부모 리소스 경로                                         |
| resourceList[0].createdAt                              | DateTime | 리소스 생성 일시                                       |
| resourceList[0].updatedAt                              | DateTime | 리소스 수정 일시                                       |
| resourceList[0].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| resourceList[0].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[0].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[0].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성 일시                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정 일시                                  |


### 리소스 삭제
- 리소스를 삭제합니다.
- 루트("/") 경로 리소스는 삭제가 불가합니다.
- CORS 플러그인에 의해 생성된 OPTIONS 메서드는 삭제할 수 없습니다. 
- CORS 플러그인에 의해 생성된 OPTIONS 메서드는 CORS 플러그인이 설정된 리소스에서 플러그인을 제거하면 일괄 삭제됩니다.
- 경로 리소스를 삭제하면 하위 경로와 메서드 리소스가 모두 삭제됩니다.
- 삭제된 리소스는 복구가 불가합니다.

#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| resourceId | String | 필수 | 없음 | 없음 | 리소스 ID |

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

### 리소스 가져오기
- [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) 형식의 파일에서 리소스를 가져옵니다.
- 리소스를 가져오면 해당 서비스에 생성되어 있던 기존의 리소스는 모두 삭제되고 가져온 리소스로 덮어씁니다.
- 리소스를 가져오면 해당 서비스에 생성되어 있던 기존의 모델은 모두 삭제되고 가져온 모델로 덮어씁니다.
- Swagger paths > path > operation에서 유효하지 않은 operation의 데이터는 무시되고 등록되지 않으므로 주의해 주세요.

#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| POST  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/import |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |

[Request Body]
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| swaggerData | Object  | 필수    | 없음 | Swagger JSON 형식 | [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) |
| swaggerData.info | Object | 필수 | 없음 | 없음 | API의 메타데이터 영역. [Info Object](https://swagger.io/specification/v2/#swagger-object) 참고 |
| swaggerData.info.title | String | 선택 | 없음 | 없음 | API의 제목. [Info Object](https://swagger.io/specification/v2/#info-object) 참고 |
| swaggerData.info.version | String  | 선택 | 없음 | 없음 | API의 버전 정보. [Info Object](https://swagger.io/specification/v2/#info-object) 참고 |
| swaggerData.paths | Object | 필수 | 없음 | 없음 | API Gateway 경로를 설정하는 API의 경로 정보를 갖는 객체 영역. [Paths Object](https://swagger.io/specification/v2/#paths-object) 참고 |
| swaggerData.paths.{path} | Object | 필수 | 없음 | {path} 최대 255자 | API Gateway 경로인 {path}와 {path} 내 메서드 정보를 갖는 객체 영역. [Paths Item Object](https://swagger.io/specification/v2/#path-item-object) 참고 |
| swaggerData.paths.{path}.{operation} | Object | 선택 | 없음 | {operation} get, post, put, delete, head, options, patch | API Gateway 메서드인 {operation}과 메서드 정보를 갖는 객체 영역. 유효하지 않은 operation의 데이터는 무시되고 등록되지 않습니다. [Operation Object](https://swagger.io/specification/v2/#operation-object) 참고  |
| swaggerData.paths.{path}.{operation}.summary | String | 선택 | {operation} 대문자 | 최대 50자 | API Gateway 메서드 이름. |
| swaggerData.paths.{path}.{operation}.description | String | 선택 | {operation} 대문자 | 최대 200자 | API Gateway 메서드 설명. |
| swaggerData.paths.{path}.{operation}.consumes | Array | 선택 | Empty Array | 없음 | API Gateway 리소스 요청 파라미터 > 콘텐츠 타입 목록 영역. |
| swaggerData.paths.{path}.{operation}.consumes[0] | String  | 선택 | 없음 | \*/\* 형식 | API Gateway 리소스 요청 파라미터 > 콘텐츠 타입. |
| swaggerData.paths.{path}.{operation}.parameters | Array | 선택 | 없음 | 없음 | API Gateway 리소스 요청 파라미터 > 쿼리 문자열, 헤더, 폼 데이터, 요청 본문 영역. [Parameter Object](https://swagger.io/specification/v2/#parameter-object) 참고 |
| swaggerData.paths.{path}.{operation}.parameters[0].name | String | 필수 | 없음 | 최대 50자 | API Gateway 리소스 요청 파라미터 > 쿼리 문자열, 헤더, 폼 데이터, 요청 본문 이름. |
| swaggerData.paths.{path}.{operation}.parameters[0].in | String | 필수 | 없음 | query, header, formData, body | API Gateway 리소스 요청 파라미터 > 쿼리 문자열, 헤더, 폼 데이터, 요청 본문 구분. |
| swaggerData.paths.{path}.{operation}.parameters[0].description | String | 선택 | 없음 | 최대 200자 | API Gateway 리소스 요청 파라미터 > 쿼리 문자열, 헤더, 폼 데이터, 요청 본문 설명. |
| swaggerData.paths.{path}.{operation}.parameters[0].required | Boolean | 필수 | 없음 | true, false | API Gateway 리소스 요청 파라미터 > 쿼리 문자열, 헤더, 폼 데이터, 요청 본문 필수 여부. |
| swaggerData.paths.{path}.{operation}.produces | Array | 선택 | Empty Array | 없음 | API Gateway 리소스 응답 > 콘텐츠 타입 목록 영역. |
| swaggerData.paths.{path}.{operation}.produces[0] | String | 선택 | 없음 | \*/\* 형식 | API Gateway 리소스 응답 > 콘텐츠 타입. |
| swaggerData.paths.{path}.{operation}.responses | Object | 선택 | 없음 | 없음 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 정보를 갖는 객체 영역. [Responses Object](https://swagger.io/specification/v2/#response-object) 참고 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode} | Object | 선택 | 없음 | {httpStatusCode} 100~599 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 객체 영역. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.description | String | 선택 | 없음 |최대 200자 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 설명. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers | Object | 선택 | 없음 | 없음 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 헤더 객체 영역. [Header Object](https://swagger.io/specification/v2/#headers-object) 참고 |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName} | Object | 선택 | 없음 | {headerName} 최대 50자 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 헤더 영역. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.description | String | 선택 | 없음 | 최대 200자 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 헤더 > 설명. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.type | String | 필수 | 없음 | string, number, integer, boolean | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 헤더 > 데이터 타입. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema | Object | 선택 | 없음 | 없음 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 응답 본문 영역.|
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema.$ref | String | 필수 | 없음 | Swagger definitions에 선언된 객체 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 > 응답 본문 > 모델. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway | Object | 선택 | 없음 | 없음 | API Gateway 제공 기능 정의 객체 영역. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins | Object | 필수 | 없음 | 없음 | API Gateway 사용자 정의 플러그인 객체 영역. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins.{pluginCode} | Object | 필수 | 없음 | {pluginCode} HTTP, MOCK, CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1) 참고. [리소스 플러그인 타입별 JSON 설정값](./api-guide-v1.0-gov/#_37) 참고. |
| swaggerData.definitions | Object | 선택 | 없음 | 없음 | API Gateway 리소스 요청 파라미터, 응답에서 사용되는 본문 객체 정의 영역. [Definitions Object](https://swagger.io/specification/v2/#definitionsObject) 참고 |




## 리소스 플러그인

### HTTP
- API Gateway에서 요청을 수신할 리소스 경로에 대해 요청을 전달할 백엔드 엔드포인트 경로를 설정합니다.
- 리소스 메서드에만 설정 가능합니다.
- MOCK 플러그인과 동시에 설정이 불가합니다.

```json
{
  "frontendEndpointPath": "/path",
  "backendEndpointPath": "/anything"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| frontendEndpointPath | String | 필수 | 없음 | 최대 255자 | API Gateway에서 요청을 수신할 리소스 경로 |
| backendEndpointPath  | String | 필수 | 없음 | 최대 255자 | API Gateway에서 수신된 요청을 전달할 백엔드 엔드포인트 경로 |

### MOCK
- 수신된 요청에 대해 정의된 응답을 반환합니다.
- 리소스 메서드에만 설정할 수 있습니다.
- HTTP 플러그인과 동시에 설정이 불가합니다.
```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"isSuccess\":true}\"}"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| statusCode | String | 필수 | 없음 | 100~599 | 사용자 정의 응답 HTTP 상태 코드                 |
| headers | Map | 선택 | 없음 | 없음 |사용자 정의 응답 헤더 객체 영역                  |
| headers[{HeaderName}] | String | 필수 | 없음 | 없음 | 객체 프로퍼티 키/값이 사용자 정의 응답 헤더의 이름과 값 |
| body                  | String | 선택 | 없음 | 없음 | 사용자 정의 응답 본문                         |

### CORS
- Cross-Site 방식 내에서 XMLHttpRequest API 호출을 할 수 있게 합니다.
- 리소스 경로에만 설정할 수 있습니다.
- CORS 플러그인이 설정된 경로 하위에는 OPTIONS 메서드가 자동으로 생성되며, 등록된 OPTIONS 메서드가 있는 경우 대체됩니다.
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| allowedMethods | List | 필수 | 없음 | 없음 | 리소스 접근에 허용할 메서드 목록 영역 |
| allowedMethods[0] | Enum | 필수 | 없음 | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고 |
| allowedHeaders | List | 필수 | 없음 | 없음 | 요청에서 사용할 수 있는 HTTP 헤더 목록 영역 |
| allowedHeaders[0] | String | 필수 | 없음 | 없음 | 요청에서 사용할 수 있는 HTTP 헤더(예시: 와일드카드 형식: '\*' 또는 'X-NHN-HEADER, Content-Type') |
| allowedOrigins    | List | 필수 | 없음 | 없음 | 리소스에 액세스할 수 있는 원본 서버의 도메인 목록 영역 |
| allowedOrigins[0] | String | 필수 | 없음 | 없음 | 리소스에 액세스할 수 있는 원본 서버의 도메인(예시: 와일드카드 형식: '\*' 또는 'http://example.nhncloudservice.com:8080') |
| exposedHeaders    | List | 선택 | 없음 | 없음 | 브라우저(클라이언트)가 접근할 수 있는 헤더 목록 영역 |
| exposedHeaders[0] | String | 필수 | 없음 | 없음 |브라우저(클라이언트)가 접근할 수 있는 헤더 |
| maxCredentialsAge | Integer | 선택 | 없음 | -1~86400 |사전 전달 요청(Preflight)에 대한 응답 브라우저 캐시 시간(초 단위) |
| allowCredentials  | Boolean | 필수 | 없음 |true/false | 자격 증명으로 요청할지 여부 |



### SET_REQUEST_HEADER
- 요청 헤더를 추가하거나 변경합니다. 
- 리소스 경로, 메서드에 설정할 수 있습니다.
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| headers | Map | 필수 | 없음 | 없음 | 추가/변경할 요청 헤더 객체 영역 |
| headers[{HeaderName}] | String | 필수 | 없음 | 없음 | 객체 프로퍼티 키/값이 추가/변경할 요청 헤더의 이름과 값 |

### SET_RESPONSE_HEADER
- 응답 헤더 변경 플러그인은 백엔드 응답에 헤더를 추가하거나 변경합니다. 
- 리소스 경로, 메서드에 설정할 수 있습니다.
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| headers | Map | 필수 | 없음 | 없음 | 추가/변경할 응답 헤더 객체 영역 |
| headers[{HeaderName}] | String | 필수 | 없음 | 없음 | 객체 프로퍼티 키/값이 추가/변경할 응답 헤더의 이름과 값 |

### ADD_REQUEST_QUERY_PARAMETER
- 백엔드 엔드포인트 요청에 쿼리 문자열 파라미터를 추가합니다.
- 리소스 경로, 메서드에 설정할 수 있습니다.
```json
{
  "parameters": {
    "queryName1": "queryValue1"
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| parameters | Map| 필수 | 없음 | 없음 | 추가할 요청 쿼리 문자열 파라미터들 객체 영역 |
| parameters[{QueryName}] | String | 필수 | 없음 | 없음 | 객체 프로퍼티 키/값이 추가할 요청 쿼리 문자열 파라미터의 이름과 값 |

## 리소스 파라미터

### 리소스 파라미터 조회 
- 리소스 파라미터의 목록을 조회합니다.

#### 요청

[URI]
 
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId     | String | 필수    | 없음  | 없음    | API Gateway 리소스 ID |

#### 응답

[Response]

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

| 필드                             | 타입      | 설명                                                   |
| ------------------------------ | ------- | ---------------------------------------------------- |
| queryStringList                | List    | 쿼리 문자열 목록 영역                                         |
| queryStringList[0].name        | String  | 쿼리 문자열 이름                                            |
| queryStringList[0].description | String  | 쿼리 문자열 설명                                            |
| queryStringList[0].dataType    | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고|
| queryStringList[0].required    | Boolean | 쿼리 문자열 필수 여부                                         |
| queryStringList[0].isArray     | Boolean | 쿼리 문자열 Array 여부                                      |
| headerList                     | List    | 헤더 목록 영역                                             |
| headerList[0].name             | String  | 헤더 이름                                                |
| headerList[0].description      | String  | 헤더 설명                                                |
| headerList[0].dataType         | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고 |
| headerList[0].required         | Boolean | 헤더 필수 여부                                             |
| headerList[0].isArray          | null    | 해더 Array 여부 미제공                                      |
| formDataList                   | List    | 폼 데이터 목록 영역                                          |
| formDataList[0].name           | String  | 폼 데이터 이름                                             |
| formDataList[0].description    | String  | 폼 데이터 설명                                             |
| formDataList[0].dataType       | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고 |
| formDataList[0].required       | Boolean | 폼 데이터 필수 여부                                          |
| formDataList[0].isArray        | Boolean | 폼 데이터 Array 여부                                       |
| requestBody                    | Object  | 요청 본문 영역                                             |
| requestBody.name               | String  | 요청 본문 이름                                             |
| requestBody.description        | String  | 요청 본문 설명                                             |
| requestBody.modelId            | String  | 요청 본문과 연결된 모델 ID                                     |
| contentTypeList                | List    | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]             | String  | 콘텐츠 타입                                               |



### 리소스 파라미터 생성
- 리소스 메서드의 파라미터를 생성합니다.
- 기존 리소스 파라미터들은 삭제되고, 요청된 리소스 파라미터들이 생성됩니다. 

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId     | String | 필수    | 없음  | 없음    | API Gateway 리소스 ID |

[Request Body]
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| queryStringList                | List    | 선택    | Empty List    | 최대 50개                                              | 쿼리 문자열 목록 영역                                         |
| queryStringList[0].name        | String  | 필수    | 없음           | 최대 50자                                              | 쿼리 문자열 이름                                            |
| queryStringList[0].description | String  | 선택    | 없음           | 최대 200자                                             | 쿼리 문자열 설명                                            |
| queryStringList[0].dataType    | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고|
| queryStringList[0].required    | Boolean | 필수    | 없음           | true, false                                          | 쿼리 문자열 필수 여부                                         |
| queryStringList[0].isArray     | Boolean | 필수    | 없음           | true, false                                          | 쿼리 문자열 Array 여부                                      |
| headerList                     | List    | 선택    | Empty List    | 최대 50개                                              | 헤더 목록 영역                                             |
| headerList[0].name             | String  | 필수    | 없음           | 최대 50자                                              | 헤더 이름                                                |
| headerList[0].description      | String  | 선택    | 없음           | 최대 200자                                             | 헤더 설명                                                |
| headerList[0].dataType         | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고|
| headerList[0].required         | Boolean | 필수    | 없음           | true, false                                          | 헤더 필수 여부                                             |
| formDataList                   | List    | 선택    | Empty List    | 최대 50개                                              | 폼 데이터 목록 영역                                          |
| formDataList[0].name           | String  | 필수    | 없음           | 최대 50자                                              | 폼 데이터 이름                                             |
| formDataList[0].description    | String  | 선택    | 없음           | 최대 200자                                             | 폼 데이터 설명                                             |
| formDataList[0].dataType       | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE, FILE  | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고|
| formDataList[0].required       | Boolean | 필수    | 없음           | true, false                                          | 폼 데이터 필수 여부                                          |
| formDataList[0].isArray        | Boolean | 필수    | 없음           | true, false                                          | 폼 데이터 Array 여부. dataType이 FILE인 경우 false.            |
| requestBody                    | Object  | 선택    | Empty Object  | 없음                                                  | 요청 본문 객체 영역                                          |
| requestBody.name               | String  | 필수    | 없음           | 최대 50자                                              | 요청 본문 이름                                             |
| requestBody.description        | String  | 선택    | 없음           | 최대 200자                                             | 요청 본문 설명                                             |
| requestBody.modelId            | String  | 필수    | 없음           | 없음                                                  | 요청 본문과 연결되는 모델 ID                                    |
| contentTypeList                | List    | 선택    | Empty List    | 최대 10개                                              | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]             | String  | 필수    | 없음           | \*/\* 형식                                             | 콘텐츠 타입                                               |

#### 응답

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

## 리소스 응답

### 리소스 응답 조회 
- HTTP 응답 상태 코드별 헤더와 요청 본문 항목과 콘텐츠 타입을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId     | String | 필수    | 없음  | 없음    | API Gateway 리소스 ID |

#### 응답

[Response]

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

| 필드                                        | 타입      | 설명                                                   |
| ----------------------------------------- | ------- | ---------------------------------------------------- |
| responseList                              | List    | HTTP 응답 상태 코드별 응답 정보 목록 영역                           |
| responseList[0].responseStatusCode        | Integer | HTTP 응답 상태 코드                                        |
| responseList[0].description               | String  | HTTP 응답 상태 코드 설명                                     |
| responseList[0].headerList                | List    | HTTP 응답 헤더 목록 영역                                     |
| responseList[0].headerList[0].name        | String  | 응답 헤더 이름                                             |
| responseList[0].headerList[0].description | String  | 응답 헤더 설명                                             |
| responseList[0].headerList[0].dataType    | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고|
| responseList[0].responseBody              | Object  | HTTP 응답 본문 객체 영역                                     |
| responseList[0].responseBody.name         | String  | 응답 본문 이름                                             |
| responseList[0].responseBody.description  | String  | 응답 본문 설명                                             |
| responseList[0].responseBody.modelId      | String  | 응답 본문과 연결된 모델 ID                                     |
| contentTypeList                           | List    | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]                        | String  | 콘텐츠 타입                                               |


### 리소스 응답 생성
- 기존 리소스 응답들은 삭제되고, 요청한 HTTP 응답 상태 코드별 헤더와 요청 본문 항목과 콘텐츠 타입을 생성합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| 이름             | 타입     | 필수 여부 | 기본값 | 유효 범위 | 설명                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | 필수    | 없음  | 없음    | API Gateway 서비스 ID |
| resourceId     | String | 필수    | 없음  | 없음    | API Gateway 리소스 ID |

[Request Body]
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
          "dataType": "STRING"
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

| 이름                                        | 타입      | 필수 여부 | 기본값          | 유효 범위                                         | 설명                                                   |
| ----------------------------------------- | ------- | ----- | ------------ | --------------------------------------------- | ---------------------------------------------------- |
| responseList                              | List    | 선택    | Empty List   | 없음                                            | HTTP 응답 상태 코드별 응답 정보 목록 영역                           |
| responseList[0].responseStatusCode        | Integer | 필수    | 없음           | 100~599                                       | HTTP 응답 상태 코드                                        |
| responseList[0].description               | String  | 선택    | 없음         | 최대 200자                                       | HTTP 응답 상태 코드 설명                                     |
| responseList[0].headerList                | List    | 선택    | Empty List   | 최대 50개                                        | HTTP 응답 헤더 목록 영역                                     |
| responseList[0].headerList[0].name        | String  | 필수    | 없음           | 최대 50자                                        | 응답 헤더 이름                                             |
| responseList[0].headerList[0].description | String  | 선택    | 없음         | 최대 200자                                       | 응답 헤더 설명                                             |
| responseList[0].headerList[0].dataType    | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드](./enum-code-gov/#_2) 참고 |
| responseList[0].responseBody              | Object  | 선택    | Empty Object | 없음                                            | HTTP 응답 본문 객체 영역                                     |
| responseList[0].responseBody.name         | String  | 필수    | 없음           | 최대 50자                                        | 응답 본문 이름                                             |
| responseList[0].responseBody.description  | String  | 선택    | 없음         | 최대 200자                                       | 응답 본문 설명                                             |
| responseList[0].responseBody.modelId      | String  | 필수    | 없음           | 없음                                           | 응답 본문과 연결된 모델 ID                                     |
| contentTypeList                           | List    | 선택    | Empty List   | 최대 10개                                        | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]                        | String  | 필수    | 없음           | \*/\* 형식                                        | 콘텐츠 타입                                               |


#### 응답

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

## 모델

### 모델 목록 조회 
- 모델 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |
| modelName | String | 선택 | 없음 | 최대 50자  | 모델 이름 필터 조건. 모델 이름의 문자열을 포함해야 합니다.|

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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                        |
|paging.page                          |Integer | 현재 페이지                                        |
|paging.limit                         |Integer | 페이지당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|modelList                     |List    | 모델 목록 영역                         |
|modelList[0].apigwServiceId  |String  |API Gateway 서비스 ID |
|modelList[0].modelId         |String  |모델 ID              |
|modelList[0].modelName       |String  |모델 이름              |
|modelList[0].modelDescription|String  |모델 설명              |
|modelList[0].modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|modelList[0].createdAt       |DateTime|모델 생성 일시            |
|modelList[0].updatedAt       |DateTime|모델 수정 일시            |



### 모델 생성
- 모델을 JSON Schema 형식으로 생성합니다.
- 모델 이름은 중복될 수 없습니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |


[Request Body]

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

| 이름               | 타입     | 필수 여부 | 기본값 | 유효 범위   | 설명                                                           |
| ---------------- | ------ | ----- | --- | ------- | ------------------------------------------------------------ |
| modelName        | String | 필수    | 없음  | 최대 50자  | 모델 이름                                                        |
| modelDescription | String | 선택    | 없음  | 최대 200자 | 모델 설명                                                        |
| modelSchema      | Object | 필수    | 없음  | 최대 65535자| 모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |

#### 응답

[Response]

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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | 모델 영역                         |
|model.apigwServiceId  |String  |API Gateway 서비스 ID |
|model.modelId         |String  |모델 ID              |
|model.modelName       |String  |모델 이름              |
|model.modelDescription|String  |모델 설명              |
|model.modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|model.createdAt       |DateTime|모델 생성 일시            |
|model.updatedAt       |DateTime|모델 수정 일시            |


### 모델 수정 
- 모델의 설명과 스키마를 수정합니다. 
- 모델 이름은 변경할 수 없습니다. 

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| modelId | String | 필수 | 없음 | 없음 | 모델 ID |

[Request Body]

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| modelDescription | String | 선택    | 없음  | 최대 200자 | 모델 설명                                                        |
| modelSchema      | Object | 필수    | 없음  | 최대 65535자| 모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |


#### 응답

[Response]

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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | 모델 영역                         |
|model.apigwServiceId  |String  |API Gateway 서비스 ID |
|model.modelId         |String  |모델 ID              |
|model.modelName       |String  |모델 이름              |
|model.modelDescription|String  |모델 설명              |
|model.modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|model.createdAt       |DateTime|모델 생성 일시            |
|model.updatedAt       |DateTime|모델 수정 일시            |


### 모델 삭제
- 모델을 삭제합니다.
- 모델이 리소스의 요청 파라미터 또는 응답에서 참조된 경우에는 모델 삭제가 불가합니다. 모델을 삭제하려면 참조를 해제한 후 모델을 삭제해 주세요.

#### 요청

[URI]

| 메서드  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| modelId | String | 필수 | 없음 | 없음 | 모델 ID |

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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

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
      "stageDescription": "alpha environment stage",
      "stageUrl": "kr1-{apigwServiceId}-alpha.api.gov-nhncloudservice.com",
      "stageCustomDomainList": [],
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
|paging.limit                         |Integer | 페이지당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|stageList        |List    | 스테이지 목록 영역 |
|stageList[0].regionCode       |Enum    |[API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고                |
|stageList[0].apigwServiceId   |String  |API Gateway 서비스 ID  |
|stageList[0].stageId          |String  |스테이지 ID             |
|stageList[0].stageName        |String  |스테이지 이름             |
|stageList[0].stageUrl         |String  |스테이지 URL            |
|stageList[0].stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
|stageList[0].stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
|stageList[0].stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
|stageList[0].stageDescription |String  |스테이지 설명             |
|stageList[0].backendEndpointUrl|String  |백엔드 엔드포인트 URL       |
|stageList[0].resourceUpdatedAt|DateTime|최근 스테이지에 리소스를 가져온 일시 |
|stageList[0].createdAt        |DateTime|스테이지 생성 일시           |
|stageList[0].updatedAt        |DateTime|스테이지 수정 일시           |


### Swagger Export
- Swagger 문서를 조회합니다. 
- Swagger 문서는 API Gateway에 배포된 설정이 아닌 현재 스테이지 설정을 기준으로 추출됩니다.

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

|필드                                  |타입     |설명                                           |
|-------------------------------------|--------|----------------------------------------------|
|swaggerData        |Object    | 현재 스테이지 기준 Swagger JSON 객체. [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) 참고. |


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
  "stageName": "alpha",
  "stageDescription": "alpha environment stage",
  "backendEndpointUrl": "https://backend.com"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| stageName | String | 조건부 필수 | 없음 | 최대 30자, 영소문자와 숫자만 | 스테이지 이름<br/>기본 스테이지가 아닌 경우 필수 값입니다.  |
| stageDescription | String | 선택 | 없음 | 최대 200자  | 스테이지 설명 |
| backendEndpointUrl | String | 필수 | 없음 | 최대 150자, URL 형식  | 백엔드 엔드포인트 URL |

- stageName 필드 값은 유일해야 합니다. 
- stageName(스테이지 이름) 필드를 null로 설정하면 기본 스테이지로 생성됩니다. 기본 스테이지는 하나만 생성할 수 있습니다. 
- stageName 필드 값에 따라 스테이지 URL이 변경됩니다.
    - 스테이지 URL 포맷: {regionCode}-{apigwServiceId}-{stageName}.api.gov-nhncloudservice.com



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
    "stageDescription": "alpha environment stage",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.gov-nhncloudservice.com",
    "stageCustomDomainList": [],
    "backendEndpointUrl": "https://backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createdAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | 스테이지 영역 |
|stage.regionCode       |Enum    |[API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고                |
|stage.apigwServiceId   |String  |API Gateway 서비스 ID  |
|stage.stageId          |String  |스테이지 ID             |
|stage.stageName        |String  |스테이지 이름             |
|stage.stageUrl         |String  |스테이지 URL            |
|stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
|stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
|stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
|stage.stageDescription |String  |스테이지 설명             |
|stage.backendEndpointUrl      |String  |백엔드 엔드포인트 URL       |
|stage.resourceUpdatedAt|DateTime|최근 스테이지에 리소스를 가져온 일시 |
|stage.createdAt        |DateTime|스테이지 생성 일시           |
|stage.updatedAt        |DateTime|스테이지 수정 일시           |

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
```json
{
  "backendEndpointUrl": "https://v2.backend.com",
  "stageDescription": "alpha v2 environment stage"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| backendEndpointUrl | String | 필수 | 없음 | 최대 150자, URL 형식  | 백엔드 엔드포인트 URL |
| stageDescription | String | 선택 | 없음 | 최대 200자  | 스테이지 설명 |


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
    "stageDescription": "alpha v2 environment stage",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.gov-nhncloudservice.com",
    "stageCustomDomainList": [],
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
|stage.regionCode       |Enum    |[API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고                |
|stage.apigwServiceId   |String  |API Gateway 서비스 ID  |
|stage.stageId          |String  |스테이지 ID             |
|stage.stageName        |String  |스테이지 이름             |
|stage.stageUrl         |String  |스테이지 URL            |
|stage.stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
|stage.stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
|stage.stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
|stage.stageDescription |String  |스테이지 설명             |
|stage.backendEndpointUrl      |String  |백엔드 엔드포인트 URL       |
|stage.resourceUpdatedAt|DateTime|최근 스테이지에 리소스를 가져온 일시 |
|stage.createdAt        |DateTime|스테이지 생성 일시           |
|stage.updatedAt        |DateTime|스테이지 수정 일시           |


### 스테이지 삭제
- 스테이지를 삭제합니다.
- 삭제하려는 스테이지가 사용량 계획에 연결된 경우 삭제가 불가합니다. 사용량 계획에서 스테이지 연결 해제 후 삭제하시기 바랍니다.
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


### 스테이지 리소스 목록 조회 
* 스테이지에 등록된 리소스 목록을 가져옵니다. 각 리소스에 설정된 스테이지 리소스 플러그인 정보가 포함됩니다.
* 스테이지 리소스 플러그인에 대한 자세한 내용은 [스테이지 리소스 플러그인](./api-guide-v1.0-gov/#_89)을 참고합니다.


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
            "defaultKey": "kr1-{apigwServiceId}.api.gov-nhncloudservice.com/:",
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
|stageResourceList[0]      |Object    |스테이지 리소스 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고  |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성 일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정 일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |스테이지 리소스의 플러그인 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1), [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[리소스 플러그인 타입](./api-guide-v1.0-gov/#_37), [스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89)별 설정 JSON 참고            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성 일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정 일시                         |



### 스테이지에 리소스 가져오기
* API Gateway 서비스 > 리소스를 스테이지에 가져옵니다. 
* 리소스를 가져오면 스테이지 리소스, 스테이지 리소스 플러그인은 모두 새로 생성됩니다. 
* 기존 리소스 경로, 메서드에 설정된 스테이지 리소스 플러그인의 설정값은 그대로 유지됩니다. 
* 리소스에 변경된 사항이 없는 경우, 수행되지 않습니다.

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
            "defaultKey": "kr1-{apigwServiceId}.api.gov-nhncloudservice.com/:",
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
|stageResourceList[0]      |Object    |스테이지 리소스 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성 일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정 일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |스테이지 리소스의 플러그인 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1), [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[리소스 플러그인 타입](./api-guide-v1.0-gov/#_37), [스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89)별 설정 JSON 참고            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성 일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정 일시                         |



### 스테이지 리소스 수정
* 리소스 경로 또는 리소스 메서드에 설정된 백엔드 엔드포인트 URL 재정의와 스테이지 리소스 플러그인을 수정합니다.
* 스테이지 리소스를 수정하면 등록된 스테이지 리소스 플러그인은 모두 삭제되고, 요청한 리소스 플러그인만 새로 등록됩니다.
* 스테이지 리소스 플러그인에 대한 자세한 정보는 [스테이지 리소스 플러그인](./api-guide-v1.0-gov/#_89)을 참고합니다.

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| customBackendEndpointUrl | String | 선택 | 없음 | 최대 150자, URL 형식 | 백엔드 엔드포인트 재정의 URL |
| stageResourcePluginList | List | 필수 | 없음 | 없음 | 스테이지 리소스 플러그인 목록 영역 |
| stageResourcePluginList[0] | Object | 필수 | 없음 | 없음 | 스테이지 리소스의 플러그인 영역 |
| stageResourcePluginList[0].pluginType  | Enum | 필수 | 없음 | IP_ACL, HMAC, JWT, API_KEY, PRE_API, RATE_LIMIT | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고|
| stageResourcePluginList[0].pluginConfigJson | Object | 필수 | 없음 | 없음 | 스테이지 리소스 플러그인 별 JSON 형식의 객체<br>[스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89) 참고|

* customBackendEndpointUrl 필드는 루트(/) 리소스 경로에는 설정할 수 없습니다.


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
            "defaultKey": "kr1-{apigwServiceId}.api.gov-nhncloudservice.com/:",
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
|stageResourceList[0]      |Object    |스테이지 리소스 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성 일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정 일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |스테이지 리소스의 플러그인 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1), [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[리소스 플러그인 타입](./api-guide-v1.0-gov/#_37), [스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89)별 설정 JSON 참고            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성 일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정 일시                         |


## 스테이지 리소스 플러그인
* 스테이지의 리소스에는 접근 제한, 인증, 사용량 제어 등의 기능을 플러그인 형태로 설정할 수 있습니다. 
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
        2. POST 리소스 메서드에 요청 수 제한을 초당 10개로 제한 (재정의)
    * 동작 결과 
        - GET /members는 루트(/)에 설정된 요청 수 제한의 초당 100개로 제한이 적용됩니다.
        - POST /members는 루트(/)에 설정된 요청 수 제한의 초당 100개 제한이 무시되고, 초당 10개로 제한으로 적용됩니다.

* 리소스에 따라 설정 가능한 플러그인

| 리소스 타입 | 설정 가능한 플러그인 목록 |
| --- | --- |
| 루트(/) 리소스 경로 |IP ACL, 인증(JWT 또는 HMAC 중 하나), 사전 호출 API, 요청 수 제한, API Key |
| 리소스 경로 |백엔드 엔드포인트 URL 재정의, 사전 호출 API, API Key |
| 리소스 메서드  |백엔드 엔드포인트 URL 재정의, 사전 호출 API, 요청 수 제한, API Key |


### IP ACL 
* IP ACL을 통해 지정된 클라이언트 IP에 대해 API Gateway 요청을 허용/거부할 수 있습니다.
* 루트(/) 리소스 경로에만 설정할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | IP_ACL | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 IP_ACL 참고 |
| pluginConfigJson | Object | 필수 | 없음 | 없음 | IP ACL 플러그인 설정 영역 |
| pluginConfigJson.isPermit | Boolean | 필수 | 없음 | true, false | false로 설정하면 설정된 IP/CIDR에 대해 요청을 거부하고, true로 설정하면 설정된 IP/CIDR만 요청을 허용합니다.  |
| pluginConfigJson.ipAclList | List | 필수 | 없음 | 1~100개 | 요청을 허용/거부할 IP 또는 CIDR 목록 영역 |
| pluginConfigJson.ipAclList[0].ipCidrAddress | String | 필수 | 없음 | IP 또는 CIDR 형식 | IP 또는 CIDR을 설정합니다. |
| pluginConfigJson.ipAclList[0].description | String | 선택 | 없음 | 최대 200자 | 설명을 설정합니다. |


### HMAC
* HMAC 서명 검증을 통해 클라이언트 요청의 변조를 검증하기 위한 설정입니다. 
* 루트(/) 리소스 경로에만 설정할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.
* HMAC 인증은 JWT 인증과 동시에 설정이 불가합니다. 
* 서명에 사용하는 비밀키를 설정합니다.
* 시간 차로 발생하는 검증 실패를 방지하기 위한 검증 유효 시간을 설정합니다.
* 요청에 필수로 포함되어야 하는 헤더 목록을 설정합니다.

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | HMAC | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 HMAC 참고 |
| pluginConfigJson | Object | 필수 | 없음 | 없음 | HMAC 플러그인 설정 영역 |
| pluginConfigJson.secretKey | String | 필수 | 없음 | 없음 | 서명에 사용되는 비밀키를 설정합니다. 최소 32바이트 이상 문자열로 설정하는 것을 권장합니다.|
| pluginConfigJson.clockSkewSeconds | Integer | 선택 | 0 | 0~86400 | 요청 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.enforceHeaders | Array | 선택 | Empty List | 없음 | 필수 검증 헤더의 문자열 배열을 입력합니다. |
| pluginConfigJson.enforceHeaders[0] | String | 필수 | 없음 | 없음| 필수 검증 헤더의 문자열 |


### JWT 
* JWT 토큰의 서명과 요청 클레임을 검증하기 위한 설정입니다.
* 루트(/) 리소스 경로에만 설정할 수 있습니다. 설정 내용은 하위 모든 리소스에 적용됩니다.
* JWT 인증은 HMAC 인증과 동시에 설정이 불가합니다.
* 서명 검증을 위한 토큰 암호화 알고리즘과 암호화 알고리즘 방식에 따른 비밀키 혹은 공개키를 설정합니다.
* 요청 클레임의 값, 필수 여부 검증을 위한 클레임 검증 조건을 설정합니다. 
* 시간 차로 발생하는 검증 실패를 방지하기 위한 검증 유효 시간을 설정합니다.
* **암호화 알고리즘 HS256** 
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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 JWT 참고 |
| pluginConfigJson | Object | 필수 | 없음  | 없음 | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | HS256 | HS256 | [JWT > 암호화 알고리즘 Enum 코드](./enum-code-gov/#jwt) 참고  |
| pluginConfigJson.hs256 | Object | 필수 | 없음 | 없음 | HS256 설정 영역 |
| pluginConfigJson.hs256.secretKey | String | 필수 | 없음 | 없음 | 서명에 사용되는 비밀키를 설정합니다. 최소 32바이트 이상 문자열로 설정하는 것을 권장합니다.|
| pluginConfigJson.clockSkew | Integer | 선택 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition | Object | 선택 | Default Object | 없음 | 클레임 검증 조건 영역 |
| pluginConfigJson.claimValidationCondition.iss | Object | 선택 | Default Object | 없음 | iss 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.iss.value | Array | 필수 | Empty Array | 없음 |  iss 요청 클레임의 값 중 허용할 클레임 값을 문자열 배열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.value[0] | String | 선택 | 없음 | 없음 |  iss 요청 클레임의 값 중 허용할 문자열을 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.dataType | Enum | 선택 | Array | Array | iss 클레임의 데이터 타입을 설정합니다. Array만 유효합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고 |
| pluginConfigJson.claimValidationCondition.iss.required | Boolean | 필수 | false | true, false | iss 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.iss.validate | Boolean | 필수 | false | true, false | iss 요청 클레임 값의 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud | Object | 선택 | Default Object | 없음 | aud 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다.  |
| pluginConfigJson.claimValidationCondition.aud.value | Array | 필수 | Empty Array | 없음 |  aud 요청 클레임의 값 중 허용할 클레임 값을 문자열 배열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.value[0] | String | 선택 | 없음 | 없음 |  aud 요청 클레임의 값 중 허용할 문자열을 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.dataType | Enum | 선택 | Array | Array | aud 클레임의 데이터 타입을 설정합니다. Array만 유효합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고 |
| pluginConfigJson.claimValidationCondition.aud.required | Boolean | 필수 | false | true, false | aud 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.aud.validate | Boolean | 필수 | true | true | aud 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.sub | Object | 선택 | Default Object | 없음 | sub 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.sub.value | String | 필수 | Empty String | 없음 |  sub 요청 클레임의 값 중 허용할 클레임 문자열 값을 설정합니다. |
| pluginConfigJson.claimValidationCondition.sub.dataType | Enum | 선택 | String | String | sub 클레임의 데이터 타입을 설정합니다. String만 유효합니다.<br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고|
| pluginConfigJson.claimValidationCondition.sub.required | Boolean | 필수 | false | true, false | sub 요청 클레임 값의 필수 검증 여부를 설정합니다. <br/> validate 필드값이 true인 경우, required는 반드시 true로 설정되어야 합니다.  |
| pluginConfigJson.claimValidationCondition.sub.validate | Boolean | 필수 | false | true, false | sub 요청 클레임 값의 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti | Object | 선택 | Default Object | 없음 | jti 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.jti.value | String | 필수 | Empty String | 없음 | jti 클레임은 허용할 검증 값 설정을 요구하지 않으므로 빈 문자열로 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti.dataType | Enum | 선택 | String | String | jti 클레임의 데이터 타입을 설정합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고|
| pluginConfigJson.claimValidationCondition.jti.required | Boolean | 필수 | false | true, false | jti 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.jti.validate | Boolean | 필수 | false | false | jti 요청 클레임 값의 검증 여부를 설정합니다. false만 유효합니다.|
| pluginConfigJson.claimValidationCondition.exp | Object | 선택 | Default Object | 없음 | exp 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.exp.dataType | Enum | 선택 | NumericDate | NumericDate | exp 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고 |
| pluginConfigJson.claimValidationCondition.exp.required | Boolean | 필수 | false | true, false | exp 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.exp.validate | Boolean | 선택 | true | true | exp 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.iat | Object | 선택 | Default Object | 없음 | iat 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.iat.dataType | Enum | 선택 | NumericDate | NumericDate | iat 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고 |
| pluginConfigJson.claimValidationCondition.iat.required | Boolean | 필수 | false | true, false | iat 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.iat.validate | Boolean | 선택 | true | true | iat 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |
| pluginConfigJson.claimValidationCondition.nbf | Object | 선택 | Default Object | 없음 | nbf 클레임 검증 조건 영역. 요청하지 않는 경우 각 필드의 기본값으로 저장됩니다. |
| pluginConfigJson.claimValidationCondition.nbf.dataType | Enum | 선택 | NumericDate | NumericDate | nbf 클레임의 데이터 타입을 설정합니다. NumericDate만 유효합니다. <br/>[JWT > 클레임 데이터 타입 Enum 코드](./enum-code-gov/#jwt_1) 참고|
| pluginConfigJson.claimValidationCondition.nbf.required | Boolean | 필수 | false | true, false | nbf 요청 클레임 값의 필수 검증 여부를 설정합니다. |
| pluginConfigJson.claimValidationCondition.nbf.validate | Boolean | 선택 | true | true | nbf 요청 클레임 값의 검증 여부를 설정합니다. true만 유효합니다. |


* **암호화 알고리즘 RS256: (PEM 형식의 공개키 설정 방식)** 

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 JWT 참고 |
| pluginConfigJson | Object | 필수 | 없음  | 없음 | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | RS256 | RS256 | [JWT > 암호화 알고리즘 Enum 코드](./enum-code-gov/#jwt) 참고  |
| pluginConfigJson.rs256 | Object | 필수 | 없음 | 없음 | RS256 설정 영역 |
| pluginConfigJson.rs256.publicKeyType | Enum | 필수 | 없음 | RSA_PUBLIC_KEY | PEM 형식의 공개키 설정 [JWT > RS256 암호화 알고리즘 > Public Key Type Enum 코드](./enum-code-gov/#jwt-rs256-public-key-type) 참고 |
| pluginConfigJson.rs256.rsaPublicKey | String | 필수 | 없음 | PEM 형식의 공개키 | PEM 형식의 공개키 값을 설정합니다.  개행 문자(\n)를 포함하여 입력해야 합니다. |
| pluginConfigJson.clockSkew | Integer | 선택 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition | Object | 선택 | Default Object | 없음 | 클레임 검증 조건 영역 (암호화 알고리즘: HS256의 claimValidationCondition 필드 설명과 동일합니다.) |


* **암호화 알고리즘 RS256: (JSON Web Key Sets URI 공개키 설정 방식)** 

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | JWT | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 JWT 참고 |
| pluginConfigJson | Object | 필수 | 없음  | 없음 | JWT 플러그인 설정 영역 |
| pluginConfigJson.encryptAlgorithm | Enum | 필수 | RS256 | RS256 |[JWT > 암호화 알고리즘 Enum 코드](./enum-code-gov/#jwt) 참고  |
| pluginConfigJson.rs256 | Object | 필수 | 없음 | 없음 | RS256 설정 영역 |
| pluginConfigJson.rs256.publicKeyType | String | 필수 | 없음 | JWKS_URI | JWKS(JSON Web Key Sets) URI 형식으로 공개키를 설정합니다. [JWT > RS256 암호화 알고리즘 > Public Key Type Enum 코드](./enum-code-gov/#jwt-rs256-public-key-type) 참고 |
| pluginConfigJson.rs256.rsaPublicKey | String | 필수 | 없음 | 없음 | JSON Web Key Set URI를 설정합니다. |
| pluginConfigJson.clockSkew | Integer | 선택 | 0 | 0~86400 | exp, nbf 클레임의 검증 유효 시간(단위: 초)을 지정합니다. |
| pluginConfigJson.claimValidationCondition | Object | 선택 | Default Object | 없음 | 클레임 검증 조건 영역 (암호화 알고리즘: HS256의 claimValidationCondition 필드 설명과 동일합니다.) |


### 사전 호출 API 
* 사전 호출 API는 백엔드 엔드포인트를 호출하기 전에 사용자가 지정한 API를 호출하여 호출의 응답 코드가 200 OK인 경우에만 백엔드 엔드포인트 호출하도록 합니다.
* 모든 리소스 경로, 메서드에 설정할 수 있습니다. 

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

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | 필수 | 없음 | PRE_API | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 PRE_API 참고 |
| pluginConfigJson | Object | 필수 | 없음 | 없음 | 사전 호출 API 플러그인 설정 영역 |
| pluginConfigJson.httpMethod | Enum | 필수 | 없음 | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고  |
| pluginConfigJson.url | String | 필수 | 없음 | URL 형식 | 사전 호출 API의 URL을 입력합니다. |
| pluginConfigJson.cacheTtl | Integer | 선택 | 0 | 0~86400 | 사전 호출 API의 응답 상태 코드의 캐시 시간을 설정합니다. <br/>응답 상태 코드가 200 OK인 경우에만 설정된 시간 동안 캐시되며, 캐시된 경우에는 사전 호출 API를 호출하지 않습니다. |


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
| pluginType | Enum | 필수 | 없음 | RATE_LIMIT | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 RATE_LIMIT 참고 |
| pluginConfigJson | Object | 필수 | 없음 | 없음 | 요청 수 제한 플러그인 설정 영역 |
| pluginConfigJson.keyType | Enum | 필수 | 없음 | DEFAULT, IP, HEADER, PATH_VARIABLE | [요청 수 제한 > 제한 키 Enum 코드](./enum-code-gov/#_4) 참고  |
| pluginConfigJson.extraKeyValue | String | 조건부 필수 | 없음 | 없음 | keyType이 HEADER인 경우, 헤더 이름을 반드시 설정해야 합니다.<br/> keyType이 PATH_VARIABLE인 경우, ${request.path.variable-name} 형식의 경로 변수를 반드시 설정해야 합니다. |
| pluginConfigJson.requestPerSec | Integer | 필수 | 없음 | 1~5000 | 초당 최대 요청 가능한 수를 설정합니다. |


### API Key

* API 호출 시 API Key가 유효한지 검증하고, 지정된 사용량 계획의 사용량을 초과했는지 검증합니다. 
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
| pluginType | Enum | 필수 | 없음 | API_KEY | [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 중 API_KEY 참고 |
| pluginConfigJson | Object | 필수 | 없음 | 없음 | API Key 플러그인 설정 영역 |
| pluginConfigJson.isActive | Boolean | 필수 | 없음 | true | API Key 검증 여부를 설정합니다. 반드시 true로 설정해야 합니다. |

## 스테이지 배포


### 스테이지 배포
- 현재 스테이지 리소스와 설정을 API Gateway 서비스에 배포합니다. 
- 변경된 설정 정보가 없는 경우, 스테이지 배포 요청이 실패합니다.
- 스테이지 배포가 실패한 경우, 기존의 성공한 스테이지 배포 설정으로 되돌려집니다.
- 스테이지 배포 요청 후, 스테이지 배포 성공 여부는 [최근 스테이지 배포 결과 조회](./api-guide-v1.0-gov/#_95)에서 확인할 수 있습니다. 

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
- [스테이지 배포](./api-guide-v1.0-gov/#_91)의 결과를 조회할 수 있습니다. 
- 스테이지 배포 요청 이후 배포 결과가 업데이트되기까지 최대 1분 정도까지 소요될 수 있습니다. 


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
                "defaultKey": "kr1-{apigwServiceId}.api.gov-nhncloudservice.com/:",
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
|latestStageDeployResult.deployStatus        |Enum  | [스테이지 배포 > 배포 상태 Enum 코드](./enum-code-gov/#_5) 참고 |
|latestStageDeployResult.isBase         |String  | 현재 스테이지 설정의 기반이 되는 배포 이력 여부 |
|latestStageDeployResult.deployedAt          |DateTime  | 배포 요청 일시 |
|latestStageDeployResult.rollbackAt   |DateTime  | 스테이지 되돌리기 요청 일시 |
|latestStageDeployResult.stageResourceList      |List    |스테이지 리소스 목록 영역                             |
|latestStageDeployResult.stageResourceList[0]      |Object    |스테이지 리소스 영역                             |
|latestStageDeployResult.stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|latestStageDeployResult.stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|latestStageDeployResult.stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|latestStageDeployResult.stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|latestStageDeployResult.stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|latestStageDeployResult.stageResourceList[0].methodType             |Enum    |[HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고               |
|latestStageDeployResult.stageResourceList[0].methodName             |String  |메서드 이름                                     |
|latestStageDeployResult.stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|latestStageDeployResult.stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성 일시                              |
|latestStageDeployResult.stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정 일시                              |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0]|Object    |스테이지 리소스의 플러그인 영역                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1), [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[리소스 플러그인 타입](./api-guide-v1.0-gov/#_37), [스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89)별 설정 JSON 참고          |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성 일시                         |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정 일시                         |

### 스테이지 배포 이력 삭제
- 스테이지 배포 이력을 삭제합니다.
- 현재 스테이지의 기반 배포 이력(isBase가 true인 경우)과 현재 API Gateway 서비스의 배포 이력은 삭제할 수 없습니다.

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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

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
|paging.limit                         |Integer | 페이지당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|stageDeployHistoryList        |List    | 스테이지 배포 이력 목록 영역 |
|stageDeployHistoryList[0]        |Object    | 스테이지 배포 이력 영역 |
|stageDeployHistoryList[0].deployId       |String    | 배포 ID |
|stageDeployHistoryList[0].stageId   |String  | 스테이지 ID  |
|stageDeployHistoryList[0].deployDescription        |String  | 배포 설명  |
|stageDeployHistoryList[0].isBase         |Boolean  | 현재 스테이지 설정의 기반이 되는 배포 이력 여부 |
|stageDeployHistoryList[0].deployedAt          |DateTime  | 배포 요청 일시 |
|stageDeployHistoryList[0].rollbackAt   |DateTime  | 스테이지 되돌리기 요청 일시 |


### 스테이지 되돌리기
- 배포된 스테이지 설정 이력으로 현재 스테이지 설정을 되돌립니다.  
- 스테이지 되돌리기를 하면 현재 스테이지 설정은 모두 삭제되므로 유의하시기 바랍니다.  
- 되돌려진 스테이지 설정을 API Gateway 서비스에 적용하려면 스테이지를 배포해야 합니다.
- 배포 실패 상태의 배포 이력으로는 되돌리기를 할 수 없습니다.

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
|stageResourceList[0]      |Object    |스테이지 리소스 영역                             |
|stageResourceList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].path                   |String  |스테이지 리소스 경로                                |
|stageResourceList[0].parentPath             |String  |스테이지 상위 리소스 경로 (루트(/) 경로의 parentPath는 null)|
|stageResourceList[0].stageId                |String  |스테이지 ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |백엔드 엔드포인트 재정의 URL                          |
|stageResourceList[0].methodType             |Enum    |[HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고               |
|stageResourceList[0].methodName             |String  |메서드 이름                                     |
|stageResourceList[0].methodDescription      |String  |메서드 설명                                     |
|stageResourceList[0].createdAt              |DateTime|스테이지 리소스 생성 일시                              |
|stageResourceList[0].updatedAt              |DateTime|스테이지 리소스 수정 일시                              |
|stageResourceList[0].stageResourcePluginList|List    |스테이지 리소스의 플러그인 목록 영역                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |스테이지 리소스의 플러그인 영역                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |스테이지 리소스 플러그인 ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |스테이지 리소스 ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |[리소스 플러그인 타입 Enum 코드](./enum-code-gov/#_1), [스테이지 리소스 > 플러그인 타입 Enum 코드](./enum-code-gov/#_3) 참고                       |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |[리소스 플러그인 타입](./api-guide-v1.0-gov/#_37), [스테이지 플러그인 타입](./api-guide-v1.0-gov/#_89)별 설정 JSON 참고         |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|스테이지 리소스 플러그인 생성 일시                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|스테이지 리소스 플러그인 수정 일시                         |


## API 설명서

### API 설명서 조회
- 배포된 스테이지 설정 기준으로 API 설명서를 조회합니다. 
- API 설명서는 [Swagger v2.0](https://swagger.io/specification/v2/)사양의 JSON 객체로 응답됩니다.
- 배포되지 않은 스테이지에 대해서는 API 설명서를 조회할 수 없으며, 404 Not Found가 응답됩니다.


#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/documents/swagger |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

#### 응답

[Response]

```json
{
  "swagger": "2.0",
  "info": {
    "version": "2021-10-26T15:21:22.163+09:00",
    "title": "alpha"
  },
  "host": "kr1-{apigwServiceId}-alpha.api.gov-nhncloudservice.com",
  "schemes": [
    "https",
    "http"
  ],
  "paths": {
    "/members/{proxy+}": {
      "get": {
        "summary": "Member API",
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
            "description": "Request ID",
            "required": false,
            "type": "string"
          },
          {
            "in": "body",
            "name": "Member",
            "description": "Member object",
            "required": false,
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Query success response",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "Response ID"
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
            "description": "Unavailable member",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "Response ID"
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
        "summary": "Member API",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|swagger                     |String    | Swagger 사양의 버전. [Swagger Object](https://swagger.io/specification/v2/#swagger-object) 참고|
|info         | Object   | API의 메타데이터 영역입니다. [Info Object](https://swagger.io/specification/v2/#swagger-object) 참고|
|info.version   |String  | API의 버전 정보이며, 스테이지 배포 요청 일시가 설정됩니다. [Info Object](https://swagger.io/specification/v2/#info-object) 참고|
|info.title      |String  | API의 제목이며, 스테이지 이름이 설정됩니다. [Info Object](https://swagger.io/specification/v2/#info-object) 참고|
|host|String    |API를 제공하는 호스트이며, 스테이지 URL이 설정됩니다. [Swagger Object](https://swagger.io/specification/v2/#swagger-object) 참고|
|schemes              |Array  | API의 지원 전송 프로토콜이며, [http, https]이 설정됩니다. [Swagger Object > schemes](https://swagger.io/specification/v2/#swagger-object) 참고|
|paths         | Object  | API의 경로들이며, 리소스 메서드의 경로들이 설정됩니다. [Paths Object](https://swagger.io/specification/v2/#pathsObject) 참고|
|paths.{path} | Object | {path}는 API의 경로이며, 리소스 메서드의 경로가 설정됩니다. [Paths Object](https://swagger.io/specification/v2/#pathsObject) 참고|
|paths.{path}.{operation}         |Object  | {operation}는 API 경로의 오퍼레이션이며, 리소스 메서드로 설정됩니다. [Path Item Object](https://swagger.io/specification/v2/#path-item-object) 참고|
|paths.{path}.{operation}.consumes         | Array  | API 경로의 오퍼레이션이 사용할 수 있는 MIME 유형 목록입니다. |
|paths.{path}.{operation}.consumes[0]         | String  | API 경로의 오퍼레이션이 사용할 수 있는 MIME 유형입니다. |
|paths.{path}.{operation}.produces         | Array  | API 경로의 오퍼레이션이 생성할 수 있는 MIME 유형 목록입니다. |
|paths.{path}.{operation}.produces[0]         | String  | API 경로의 오퍼레이션이 생성할 수 있는 MIME 유형입니다. |
|paths.{path}.{operation}.summary                |String  | API 요약이며, 리소스의 이름이 설정됩니다. [Operation Object](https://swagger.io/specification/v2/#operation-object) 참고|
|paths.{path}.{operation}.description                |String  |API 설명이며, 리소스의 설명이 설정됩니다. [Operation Object](https://swagger.io/specification/v2/#operation-object) 참고|
|paths.{path}.{operation}.parameters                | Object  | API 파라미터이며, 리소스의 경로 변수와 요청 파라미터가 설정됩니다. [Parameter Object](https://swagger.io/specification/v2/#parameter-object) 참고|
|paths.{path}.{operation}.responses                | Object  | API 응답이며, 리소스 응답이 설정됩니다. [Responses Object](https://swagger.io/specification/v2/#responses-object) 참고|
|paths.{path}.{operation}.security     | Array  | API 오퍼레이션의 작업에 사용되는 보안 정의입니다. API Key, 인증(HMAC, JWT) 설정 시 API Gateway의 사용자 정의 설정이 포함됩니다. |
|paths.{path}.{operation}.x-nhncloud-apigateway     | Object  | NHN Cloud API Gateway 정의 설정 영역 |
|paths.{path}.{operation}.x-nhncloud-apigateway.plugins     | Object  | API Gateway의 사용자 정의 플러그인 정보 영역입니다. 리소스 > 플러그인 설정과 리소스와 매핑된 백엔드 엔드포인트 경로의 설정이 포함됩니다. |
|securityDefinitions          |Object    | 보안 정의 객체입니다. API Key, 인증(HMAC, JWT) 설정 시 API Gateway의 사용자 정의 설정이 포함됩니다. [Security Definitions Object](https://swagger.io/specification/v2/#securityDefinitionsObject) 참고|
|definitions | Object | 요청 및 응답에서 사용되는 데이터 유형에 대한 영역. 요청 파라미터/응답에서 참조된 모델이 정의가 설정됩니다. [Definitions Object](https://swagger.io/specification/v2/#definitionsObject) 참고| 

## API Key

### API Key 목록 조회 
- API Key 목록을 조회합니다.
- 여러 요청 쿼리 파라미터들이 있는 경우 모든 조건을 만족하는 목록을 반환합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | Primary 또는 Secondary API Key 필터 조건 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID 필터 조건 |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름  필터 조건. API Key 이름의 시작 문자열은 일치해야 합니다. |
| apiKeyStatus | Enum | 선택 | 없음 | ACTIVE, INACTIVE | API Key 상태 필터 조건. [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |

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

| 필드                              | 타입       | 설명                                                |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | 페이징 영역                                            |
| paging.page                     | Integer  | 현재 페이지                                            |
| paging.limit                    | Integer  | 페이지당 건 수                                         |
| paging.totalCount               | Integer  | 전체 건 수                                            |
| apiKeyList                      | List     | API Key 목록 영역                                     |
| apiKeyList[0]                   | Object   | API Key 영역                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key 이름                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key 설명                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key 값                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |
| apiKeyList[0].createdAt         | DateTime | API Key 생성 일시                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key 수정 일시                                      |

### API Key 생성
- API Key를 생성합니다. 

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/apikeys |

[Request Body]
```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE"
}
```

| 이름                | 타입     | 필수 여부 | 기본값 | 유효 범위            | 설명                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | 필수    | 없음  | 최대 50자           | API Key 이름                                        |
| apiKeyDescription | String | 선택    | 없음  | 최대 200자          | API Key 설명                                        |
| apiKeyStatus      | Enum   | 필수    | 없음  | ACTIVE, INACTIVE | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |

#### 응답

[Response]

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

| 필드                       | 타입       | 설명                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key 영역                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key 이름                                        |
| apiKey.apiKeyDescription | String   | API Key 설명                                        |
| apiKey.primaryApiKey     | String   | Primary API Key 값                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |
| apiKey.createdAt         | DateTime | API Key 생성 일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정 일시                                      |


### API Key 수정
- API Key의 이름, 설명, 상태를 수정합니다.
- API Key 상태를 INACTIVE로 변경하면, API Key가 비활성화되며 API호출이 불가해집니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

[Request Body]
```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE"
}
```

| 이름                | 타입     | 필수 여부 | 기본값 | 유효 범위            | 설명                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | 필수    | 없음  | 최대 50자           | API Key 이름                                        |
| apiKeyDescription | String | 선택    | 없음  | 최대 200자          | API Key 설명                                        |
| apiKeyStatus      | Enum   | 필수    | 없음  | ACTIVE, INACTIVE | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |

#### 응답

[Response]

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

| 필드                       | 타입       | 설명                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key 영역                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key 이름                                        |
| apiKey.apiKeyDescription | String   | API Key 설명                                        |
| apiKey.primaryApiKey     | String   | Primary API Key 값                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |
| apiKey.createdAt         | DateTime | API Key 생성 일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정 일시                                      |


### API Key 삭제
- API Key를 삭제합니다. 삭제된 API Key는 복구할 수 없습니다.
- 사용량 계획의 스테이지에 연결된 API Key가 있는 경우, API Key를 삭제할 수 없습니다. 삭제하려면 API Key를 연결 해제해야 합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

#### 응답

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### API Key 재발급
- API Key 값으로 사용되는 Primary API Key, Secondary API Key는 각각 재발급할 수 있습니다.
- 재발급할 경우 이전 API Key로는 API 호출이 불가합니다. 재발급 이전 API Key로 복구는 불가합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/regenerate |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

[Request Body]
```json
{
  "apiKeyType": "PRIMARY"
}
```

| 이름                | 타입     | 필수 여부 | 기본값 | 유효 범위            | 설명                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyType      | Enum   | 필수    | 없음  | PRIMARY, SECONDARY | 변경하려는 API Key 타입. [API Key 타입 Enum 코드](./enum-code-gov/#api-key_1) 참고 |

#### 응답

[Response]

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

| 필드                       | 타입       | 설명                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key 영역                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key 이름                                        |
| apiKey.apiKeyDescription | String   | API Key 설명                                        |
| apiKey.primaryApiKey     | String   | Primary API Key 값                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |
| apiKey.createdAt         | DateTime | API Key 생성 일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정 일시                                      |

### 스테이지에 연결 가능한 API Key 목록 조회
- 스테이지에 연결 가능한 API Key 목록을 조회합니다.
- 여러 요청 쿼리 파라미터들이 있는 경우 모든 조건을 만족하는 목록을 반환합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/stages/{stageId}/apikeys/connectable |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| stageId | String | 필수 | 없음 | 없음 | Stage ID |


[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | primary 또는 secondary API Key 값 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름 시작 문자열 |
| apiKeyStatus | Enum | 선택 | 없음 | ACTIVE, INACTIVE | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |

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

| 필드                              | 타입       | 설명                                                |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | 페이징 영역                                            |
| paging.page                     | Integer  | 현재 페이지                                            |
| paging.limit                    | Integer  | 페이지당 건 수                                         |
| paging.totalCount               | Integer  | 전체 건 수                                            |
| apiKeyList                      | List     | API Key 목록 영역                                     |
| apiKeyList[0]                   | Object   | API Key 영역                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key 이름                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key 설명                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key 값                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code-gov/#api-key) 참고 |
| apiKeyList[0].createdAt         | DateTime | API Key 생성 일시                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key 수정 일시                                      |


## 사용량 계획

### 사용량 계획 목록 조회 
- 사용량 계획 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

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

| 필드                                         | 타입       | 설명                                                |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | 페이징 영역                                            |
| paging.page                                | Integer  | 현재 페이지                                            |
| paging.limit                               | Integer  | 페이지당 건 수                                         |
| paging.totalCount                          | Integer  | 전체 건 수                                            |
| usagePlanList                              | List     | 사용량 계획 목록 영역                                      |
| usagePlanList[0]                           | Object   | 사용량 계획 영역                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlanList[0].usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlanList[0].usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| usagePlanList[0].quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlanList[0].createdAt                 | DateTime | 사용량 계획 생성 일시                                       |
| usagePlanList[0].updatedAt                 | DateTime | 사용량 계획 수정 일시                                       |



### 단일 사용량 계획 조회
- 단일 사용량 계획을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |

#### 응답

[Response]

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

| 필드                                  | 타입       | 설명                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 사용량 계획 영역                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlan.usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlan.usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성 일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정 일시                                       |

### 사용량 계획 생성
- 사용량 계획을 생성합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans |

[Request Body]
```json
{
  "usagePlanName": "string",
  "usagePlanDescription": "string",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

| 이름                        | 타입      | 필수 여부 | 기본값 | 유효 범위        | 설명                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | 필수    | 없음  | 최대 50자       | 사용량 계획 이름                                         |
| usagePlanDescription      | String  | 선택    | 없음  | 최대 200자      | 사용량 계획 설명                                         |
| rateLimitRequestPerSecond | Integer | 선택    | 없음  | 1~5000       | 초당 요청 수 제한                                        |
| quotaLimitPeriodUnitCode  | Enum    | 선택    | 없음  | DAY, MONTH   | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| quotaLimit                | Integer | 조건부 필수 | 없음  | 1~2147483647 | quotaLimitPeriodUnitCode가 설정된 경우 필수. 할당량 기간 단위 별 요청 할당량                                |

#### 응답

[Response]

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

| 필드                                  | 타입       | 설명                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 사용량 계획 영역                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlan.usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlan.usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성 일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정 일시                                       |


### 사용량 계획 수정
- 사용량 계획을 수정합니다. 
- 할당량 기간 단위를 '없음'으로 수정하면 연결된 API Key들의 요청 할당량 사용량은 초기화됩니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |

[Request Body]
```json
{
  "usagePlanName": "Basic",
  "usagePlanDescription": "It's for Basic User",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

| 이름                        | 타입      | 필수 여부 | 기본값 | 유효 범위        | 설명                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | 필수    | 없음  | 최대 50자       | 사용량 계획 이름                                         |
| usagePlanName             | String  | 선택    | 없음  | 최대 200자      | 사용량 계획 설명                                         |
| rateLimitRequestPerSecond | Integer | 선택    | 없음  | 1~5000       | 초당 요청 수 제한                                        |
| quotaLimitPeriodUnitCode  | Enum    | 선택    | 없음  | DAY, MONTH   | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| quotaLimit                | Integer | 조건부 필수 | 없음  | 1~2147483647 | quotaLimitPeriodUnitCode가 설정된 경우 필수. 할당량 기간 단위 별 요청 할당량                                |

#### 응답

[Response]

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

| 필드                                  | 타입       | 설명                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | 사용량 계획 영역                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlan.usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlan.usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성 일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정 일시                                       |


### 사용량 계획 삭제
- 사용량 계획을 삭제합니다.
- 사용량 계획에 연결된 스테이지들을 모두 해제한 후 사용량 계획을 삭제할 수 있습니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |

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


### 사용량 계획에 연결된 스테이지 목록 조회
- 사용량 계획에 연결된 스테이지 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |

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
  "usagePlanStageList": [
    {
      "regionCode": "KR1",
      "apigwServiceId": "{apigwServiceId}",
      "apigwServiceName": "APIGW Example",
      "stageId": "{stageId}",
      "stageName": "custom",
      "stageUrl": "kr1-example-custom.api.gov-nhncloudservice.com",
      "stageCustomDomainList": [],
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic"
    }
  ]
}
```

| 필드                                    | 타입      | 설명                     |
| ------------------------------------- | ------- | ---------------------- |
| paging                                | Object  | 페이징 영역                 |
| paging.page                           | Integer | 현재 페이지                 |
| paging.limit                          | Integer | 페이지당 건 수              |
| paging.totalCount                     | Integer | 전체 건 수                 |
| usagePlanStageList                    | List    | 사용량 계획과 연결된 스테이지 목록 영역 |
| usagePlanStageList[0]                | Object  | 사용량 계획과 연결된 스테이지 영역    |
| usagePlanStageList[0].regionCode | Enum    | [API Gateway 리전 Enum 코드](./enum-code-gov/#api-gateway) 참고 |
| usagePlanStageList[0].apigwServiceId | String  | API Gateway 서비스 ID     |
| usagePlanStageList[0].apigwServiceName      | String  | API Gateway 서비스 이름     |
| usagePlanStageList[0].stageId        | String  | 스테이지 ID                |
| usagePlanStageList[0].stageName      | String  | 스테이지 이름                |
| usagePlanStageList[0].stageUrl       | String  | 스테이지 URL               |
| usagePlanStageList[0].stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
| usagePlanStageList[0].stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
| usagePlanStageList[0].stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
| usagePlanStageList[0].usagePlanId    | String  | 사용량 계획 ID              |
| usagePlanStageList[0].usagePlanName  | String  | 사용량 계획 이름              |


### 사용량 계획에 스테이지 연결
- 사용량 계획에 스테이지를 연결합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

#### 응답

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### 사용량 계획에 연결된 스테이지 해제
- 사용량 계획에 연결된 스테이지를 연결 해제합니다.
- 스테이지에 연결된 API Key가 존재하면 연결을 해제할 수 없습니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

#### 응답

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### 스테이지가 연결된 사용량 계획 목록 조회
- 스테이지가 연결된 사용량 계획 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/stages/{stageId} |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

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

| 필드                                         | 타입       | 설명                                                |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | 페이징 영역                                            |
| paging.page                                | Integer  | 현재 페이지                                            |
| paging.limit                               | Integer  | 페이지당 건 수                                         |
| paging.totalCount                          | Integer  | 전체 건 수                                            |
| usagePlanList                              | List     | 사용량 계획 목록 영역                                      |
| usagePlanList[0]                           | Object   | 사용량 계획 영역                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlanList[0].usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlanList[0].usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| usagePlanList[0].quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlanList[0].createdAt                 | DateTime | 사용량 계획 생성 일시                                       |
| usagePlanList[0].updatedAt                 | DateTime | 사용량 계획 수정 일시                                       |

## API Key 구독

### API Key 구독 목록 조회
- API Key가 연결된 스테이지와 사용량 계획 정보의 목록을 조회합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/subscriptions |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |
| stageUrl | String | 선택 | 없음 | 없음 | Stage Url 필터 조건 |

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
    "subscribedStageAndUsagePlanList": [
        {
            "subscriptionId": "{subscriptionId}",
            "subscriptionStatus": "APPROVAL",
            "apiKeyId": "{apiKeyId}",
            "apigwServiceName": "test api gateway",
            "stageId": "{stageId}",
            "stageName": null,
            "stageUrl": "kr1-example.api.gov-nhncloudservice.com",
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

| 필드                                                           | 타입      | 설명                                                |
| ------------------------------------------------------------ | ------- | ------------------------------------------------- |
| paging                                                       | Object  | 페이징 영역                                            |
| paging.page                                                  | Integer | 현재 페이지                                            |
| paging.limit                                                 | Integer | 페이지당 건 수                                         |
| paging.totalCount                                            | Integer | 전체 건 수                                            |
| subscribedStageAndUsagePlanList                              | List    | API Key가 연결된 스테이지와 사용량 계획 목록 영역                |
| subscribedStageAndUsagePlanList[0]                           | Object    | API Key가 연결된 스테이지와 사용량 계획 영역                |
| subscribedStageAndUsagePlanList[0].subscriptionId            | String  | 구독 ID                                     |
| subscribedStageAndUsagePlanList[0].subscriptionStatus        | Enum    | [API Key 구독 상태 Enum 코드](./enum-code-gov/#api-key_2) 참고              |
| subscribedStageAndUsagePlanList[0].apiKeyId                  | String  | API Key ID                                        |
| subscribedStageAndUsagePlanList[0].apigwServiceName          | String  | API Gateway 서비스 이름                                |
| subscribedStageAndUsagePlanList[0].stageId                   | String  | 스테이지 ID                                           |
| subscribedStageAndUsagePlanList[0].stageName                 | String  | 스테이지 이름                                           |
| subscribedStageAndUsagePlanList[0].stageUrl                  | String  | 스테이지 URL                                          |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
| subscribedStageAndUsagePlanList[0].usagePlanId               | String  | 사용량 계획 ID                                         |
| subscribedStageAndUsagePlanList[0].usagePlanName             | String  | 사용량 계획 이름                                         |
| subscribedStageAndUsagePlanList[0].usagePlanDescription      | String  | 사용량 계획 설명                                         |
| subscribedStageAndUsagePlanList[0].rateLimitRequestPerSecond | Integer | 초당 요청 수 제한                                        |
| subscribedStageAndUsagePlanList[0].quotaLimitPeriodUnitCode  | Enum    | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code-gov/#_6) 참고 |
| subscribedStageAndUsagePlanList[0].quotaLimit                | Integer | 할당량 기간 단위 별 요청 할당량                                |


### 사용량 계획의 스테이지를 구독 중인 API Key 목록 조회
- 사용량 계획의 스테이지에 연결된 API Key 목록을 조회합니다.
- 여러 요청 쿼리 파라미터들이 있는 경우 모든 조건을 만족하는 목록을 반환합니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | Primary 또는 Secondary API Key 필터 조건 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID 필터 조건 |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름  필터 조건. API Key 이름의 시작 문자열은 일치해야 합니다.  |
| apiSubscriptionStatus | Enum | 선택 | 없음 | APPROVAL | [API Key 구독 상태 Enum 코드](./enum-code-gov/#api-key_2) 참고 |

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

| 필드                                             | 타입       | 설명                                   |
| ---------------------------------------------- | -------- | ------------------------------------ |
| paging                                         | Object   | 페이징 영역                               |
| paging.page                                    | Integer  | 현재 페이지                               |
| paging.limit                                   | Integer  | 페이지당 건 수                            |
| paging.totalCount                              | Integer  | 전체 건 수                               |
| apiSubscriptionList                            | List     | 구독 정보 목록 영역      |
| apiSubscriptionList[0]                         | Object   | 구독 정보 영역      |
| apiSubscriptionList[0].subscriptionId          | String   | 구독 ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Key 구독 상태 Enum 코드](./enum-code-gov/#api-key_2) 참고 |
| apiSubscriptionList[0].subscriptionDescription | String   | 구독 설명                                |
| apiSubscriptionList[0].stageId                 | String   | 스테이지 ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 사용량 계획 ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key 이름                           |
| apiSubscriptionList[0].createdAt               | DateTime | 구독 생성 일시                              |
| apiSubscriptionList[0].updatedAt               | DateTime | 구독 수정 일시                              |


### API Key 구독 (API Key 연결)
- 사용량 계획의 스테이지에 요청한 API Key 목록을 연결합니다.
- 연결된 API Key만 API Key 인증에 성공하고, 사용량 계획의 사용량 제한이 적용됩니다.
- 다른 사용량 계획의 동일 스테이지에 연결된 API Key는 연결할 수 없습니다.

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[Request Body]
```json
{
  "apiKeyIdList": [
    "{apiKeyId}"
  ]
}
```

| 이름                        | 타입      | 필수 여부 | 기본값 | 유효 범위        | 설명                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiKeyIdList              | List  | 필수    | 없음  | 최대 100개       | API Key ID 목록 영역                                        |
| apiKeyIdList[0]           | String  | 필수    | 없음  | 없음       | API Key ID                                        |

#### 응답

[Response]

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

| 필드                                             | 타입       | 설명                                   |
| ---------------------------------------------- | -------- | ------------------------------------ |
| apiSubscriptionList                            | List     | 구독 정보 목록 영역                          |
| apiSubscriptionList[0]                         | Object   | 구독 정보 영역                        |
| apiSubscriptionList[0].subscriptionId          | String   | 구독 ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Key 구독 상태 Enum 코드](./enum-code-gov/#api-key_2) 참고 |
| apiSubscriptionList[0].subscriptionDescription | String   | 구독 설명                                |
| apiSubscriptionList[0].stageId                 | String   | 스테이지 ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 사용량 계획 ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key 이름                           |
| apiSubscriptionList[0].createdAt               | DateTime | 구독 생성 일시                              |
| apiSubscriptionList[0].updatedAt               | DateTime | 구독 수정 일시                              |


### API Key 구독 취소 (API Key 연결 해제)
- 사용량 계획의 스테이지에서 요청한 API Key 목록을 연결 해제합니다.
- 연결 해제된 API Key는 API Key 인증에 실패하여 API 호출이 실패합니다. 

#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| DELETE | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[Request Body]
```json
{
  "apiSubscriptionIdList": [
    "{apiKeyId}"
  ]
}
```

| 이름                        | 타입      | 필수 여부 | 기본값 | 유효 범위        | 설명                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiSubscriptionIdList             | List  | 필수    | 없음  | 최대 100개       | 구독 ID 목록 영역                                        |
| apiSubscriptionIdList[0]             | String  | 필수    | 없음  | 없음       | 구독 ID                                        |

#### 응답

[Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```


### API Key의 사용량 계획 변경
- 선택한 스테이지가 연결된 다른 사용량 계획으로만 변경할 수 있습니다.
- 사용량 계획 변경 시 API Key 요청 할당량의 사용량은 초기화됩니다.
    - 할당량 기간 단위가 '일' 또는 '월'인 사용량 계획으로 변경하면, 연결된 API Key 요청 할당량의 사용량은 유지됩니다. 요청 할당량 한도가 낮은 사용량 계획으로 변경 시 사용량이 초과될 수 있습니다. 
    - 할당량 기간 단위가 '없음'인 사용량 계획으로 변경하면, 연결된 API Key 요청 할당량의 사용량은 초기화됩니다.
  
#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions/{subscriptionId}/change-usage-plan |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | 필수 | 없음 | 없음 | 사용량 계획 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |
| subscriptionId | String | 필수 | 없음 | 없음 | 구독 ID |

[Request Body]
```json
{
  "changeUsagePlanId": "{usagePlanId}"
}
```

| 이름                        | 타입      | 필수 여부 | 기본값 | 유효 범위        | 설명                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| changeUsagePlanId            | String  | 필수    | 없음  | 없음       | 변경할 사용량 계획 ID                                        |

#### 응답

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

## 통계

### 스테이지 리소스별 조회
- 조회 기간 동안의 리소스별 통계 데이터를 조회합니다.


#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/metrics |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | 필수 | 없음 | 없음 | 통계 조회 시작 일시 |
| endTime | DateTime | 필수 | 없음 | 없음 | 통계 조회 종료 일시 |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지당 건 수 |

* startTime, endTime 필드의 조회 기간은 최근 90일까지 조회할 수 있습니다.
* stageTime, endTime 필드는 ISO8601형식의 날짜 문자열 형식으로 입력합니다. 
    * UTC 표기: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC 기준 타임 오프셋 표기: yyyy-MM-dd'T'HH:mm:ss±hh:mm


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

|필드                                   |타입      |설명                                         |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                     |
|paging.page                          |Integer | 현재 페이지                                    |
|paging.limit                         |Integer | 페이지당 건 수                                 |
|paging.totalCount                    |Integer | 전체 건 수                                     |
|data                                 |List    | 리소스별 통계 데이터 목록 영역                      |
|data[0]                              |Object    | 리소스별 통계 데이터 영역                      |
|data[0].uriPattern                   |String  | 리소스 경로 또는 경로 패턴                         |
|data[0].httpMethodType               |Enum  | [HTTP 메서드 타입 Enum 코드](./enum-code-gov/#http) 참고                             |
|data[0].successCount                 |Long    | API 성공 수(응답 HTTP 상태 코드가 2xx, 3xx인 경우) |
|data[0].failCount               |Long    | API 실패 수(응답 HTTP 상태 코드가 4xx, 5xx인 경우) |
|data[0].status2xxCount               |Long    | 응답 HTTP 상태 코드가 2xx인 API 호출 수 |
|data[0].status3xxCount               |Long    | 응답 HTTP 상태 코드가 3xx인 API 호출 수 |
|data[0].status4xxCount               |Long    | 응답 HTTP 상태 코드가 4xx인 API 호출 수 |
|data[0].status5xxCount               |Long    | 응답 HTTP 상태 코드가 5xx인 API 호출 수 |
|data[0].statusEtcCount               |Long    | 2xx, 3xx, 4xx, 5xx 외 응답 HTTP 상태 코드 API 호출 수 |
|data[0].avgResponseTimeMs            |Long    | 평균 API 응답 시간(ms) |
|data[0].networkOutboundByte          |Long    | 아웃바운드 네트워크 바이트 합계(bytes) |
|metricsLatestUpdatedAt         | DateTime | 통계 데이터 최신 갱신 일시                             |


### API Key별 조회
- API Key별 일 단위 통계를 조회합니다.


#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/metrics |

[Path Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | 필수 | 없음 | 없음 | 통계 조회 시작 일시 |
| endTime | DateTime | 필수 | 없음 | 없음 | 통계 조회 종료 일시 |

* startTime, endTime 필드의 조회 기간은 최근 90일까지 조회할 수 있습니다.
* stageTime, endTime 필드는 ISO8601형식의 날짜 문자열 형식으로 입력합니다.
    * UTC 표기: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC 기준 타임 오프셋 표기: yyyy-MM-dd'T'HH:mm:ss±hh:mm

#### 응답

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "data": {
    "kr1-{apigwServiceId}-member.api.gov-nhncloudservice.com": {
      "stageName": "member",
      "stageUrl": "kr1-{apigwServiceId1}-member.api.gov-nhncloudservice.com",
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
    "kr1-{apigwServiceId}-billing.api.gov-nhncloudservice.com": {
      "stageName": "billing",
      "stageUrl": "kr1-{apigwServiceId}-billing.api.gov-nhncloudservice.com",
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

|필드                                   |타입      |설명                                         |
|-------------------------------------|--------|----------------------------------------------|
|data                                 |Object  | API Key 통계 데이터 영역                         |
|data.{requestApigwEndpoint}          |Object  | API 호출 엔드포인트별 통계 영역                |
|data.{requestApigwEndpoint}.stageName                    |String    | 스테이지 이름            |
|data.{requestApigwEndpoint}.stageUrl                     |String    | 스테이지 URL |
|data.{requestApigwEndpoint}.stageCustomDomainList   |List  |스테이지 사용자 지정 도메인 목록 영역   |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].customDomain   |String  |사용자 지정 도메인   |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].createdAt   |DateTime  |사용자 지정 도메인 연결 일시    |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries      |Object    | 집계 시간 단위별 API Key 통계 영역|
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount               |List    | API 호출 수 통계 목록 영역 |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0]               |Object    | API 호출 수 통계 영역 |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].dateTime   |Long    | 통계 시간(Unix time 형식) |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].count      |Long    | 통계 시간 동안의 총 API 호출 수 |
|metricsLatestUpdatedAt         | DateTime | 통계 데이터 최신 갱신 일시                             |
|timeUnit          |Enum    | [통계 데이터 시간 단위 Enum 코드](./enum-code-gov/#_7) ONE_DAYS 참고 |


* 일 단위 통계 데이터는 각 일의 00:00:00의 시간 데이터에 집계됩니다.


### Top 10 서비스 조회
- 전체 API 호출 수, 실패 API 호출 수, 평균 응답 시간을 기준으로 상위 10개의 API Gateway 서비스 목록과 누적 통계를 조회할 수 있습니다.


#### 요청

[URI]

| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/metrics/top-services |


[QueryString Parameter]

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| lastDays | Integer | 선택 | 7 | 1~30 | 조회 기간의 일 수(당일 포함)  |
| order | Enum | 선택 | CALL_COUNT | CALL_COUNT,FAIL_CALL_COUNT,AVG_RESPONSE_TIME | [통계 > Top10 서비스 정렬 기준](./enum-code-gov/#top10)|


#### 응답

[Response]

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

| 필드 | 타입 | 설명 |
| --- | --- | --- |
|data | Object | Top 10 서비스 통계 데이터 영역 |
|data[0].rank | Integer  | 순위 번호 |
|data[0].apigwServiceId | String | API Gateway 서비스 ID |
|data[0].apigwServiceName | String | API Gateway 서비스 이름 |
|data[0].successCount | Long | API 성공 수(응답 HTTP 상태 코드가 2xx, 3xx인 경우) |
|data[0].failCount | Long | API 실패 수(응답 HTTP 상태 코드가 4xx, 5xx인 경우) |
|data[0].status2xxCount | Long | 응답 HTTP 상태 코드가 2xx인 API 호출 수 |
|data[0].status3xxCount | Long | 응답 HTTP 상태 코드가 3xx인 API 호출 수 |
|data[0].status4xxCount | Long | 응답 HTTP 상태 코드가 4xx인 API 호출 수 |
|data[0].status5xxCount | Long | 응답 HTTP 상태 코드가 5xx인 API 호출 수 |
|data[0].statusEtcCount | Long | 2xx, 3xx, 4xx, 5xx 외 응답 HTTP 상태 코드 API 호출 수 |
|data[0].avgResponseTimeMs | Long | 평균 API 응답 시간(ms) |
|data[0].networkOutboundByte | Long | 아웃바운드 네트워크 바이트 합계(bytes) |
|metricsLatestUpdatedAt | DateTime | 통계 데이터 최신 갱신 일시 |