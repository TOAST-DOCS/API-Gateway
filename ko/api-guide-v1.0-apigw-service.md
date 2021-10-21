## Application Service > API Gateway > API v1.0 가이드

NHN Cloud API Gateway에서 제공하는 Public API v1.0을 설명합니다.

## API 공통 정보

### 도메인

| 이름              | 도메인                                   |
| --------------- | ------------------------------------- |
| API 도메인 | https://apigw.api.nhncloudservice.com |

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

[필드]
| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header               | Object  | 헤더 영역  |
| header.isSuccessful  | Boolean | 성공 여부  |
| header.resultCode    | Integer | 결과 코드  |
| header.resultMessage | String  | 결과 메시지 |

[실패: Response Body]  
잘못된 API 요청을 한 경우, errorList 필드에 자세한 오류 원인과 필드 정보가 응답됩니다.  

``` json
{
  "header": {
    "isSuccessful": false,
    "resultCode": 400,
    "resultMessage": "Bad Request"
  },
  "errorList": [
    {
      "resultCode": 400,
      "errorProperty": "putResourceAndPluginRequest",
      "errorField": "deleteResourcePluginList[0]",
      "errorMessage": "리소스 플러그인 중 잘못된 값이 존재합니다."
    }
  ]
}
```

[필드]
| 필드 | 타입 | 설명 |
| --- | --- | --- |
| errorList            | List  | 오류 영역  |
| errorList[0].resultCode  | Integer | 오류 코드  |
| errorList[0].errorProperty | String | 오류 프로퍼티(모델) |
| errorList[0].errorField | String  | 오류 상세 필드 |
| errorList[0].errorMessage | String  | 오류 메시지 |

## API Gateway 서비스

### 서비스 목록 조회 
- API Gateway 서비스 목록을 조회합니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services |

[QueryString Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| regionCode | String | 필수 | 없음 | KR1 | [API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType) |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |

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
         "name":"test api gateway",
         "description":"description of test api gateway service",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                        |
|paging.page                          |Integer | 현재 페이지                                        |
|paging.limit                         |Integer | 페이지 당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|apigwServiceList                     |List    | API Gateway 서비스 목록 영역                         |
|apigwServiceList[0].apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwServiceList[0].apigwServiceAlias   |String  | API Gateway 서비스 별칭               |
|apigwServiceList[0].apigwServiceId      |String  | API Gateway 서비스 ID                  |
|apigwServiceList[0].apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType)|
|apigwServiceList[0].appKey              |String  | AppKey                                        |
|apigwServiceList[0].dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwServiceList[0].description         |String  | API Gateway  서비스 설명                                        |
|apigwServiceList[0].name                |String  | API Gateway 서비스 이름                                        |
|apigwServiceList[0].regionCode          |Enum    | [API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode) |
|apigwServiceList[0].serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwServiceList[0].createdAt           |DateTime| API Gateway 서비스 생성일시                                      |
|apigwServiceList[0].updatedAt           |DateTime| API Gateway 서비스 수정일시                                      |


### 단일 서비스 조회 
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

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwServiceBean": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "name": "test api gateway",
    "description": "description of test api gateway",
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

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object  | API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  | API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  | API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType) |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwService.description         |String  | API Gateway 서비스 설명                                        |
|apigwService.name                |String  | API Gateway 서비스 이름                                        |
|apigwService.regionCode          |Enum    |[API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode) |
|apigwService.serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime| API Gateway 서비스 생성일시                                      |
|apigwService.updatedAt           |DateTime| API Gateway 서비스 수정일시                                      |



### API Gateway 서비스 생성
- API Gateway 서비스를 생성합니다.
- API Gateway 서버가 생성될 리전을 선택할 수 있습니다. 현재는 한국(판교)리전만 지원합니다.
- API Gateway 서비스를 생성하면 API Gateway 서비스 ID가 자동 발급됩니다.


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services |

[Request Body]
``` json
{
  "regionCode": "KR1",
  "serviceName": "service name",
  "description": "service description"
}
```
[필드]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | 필수 | 없음 | KR1 | [API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType) |
| serviceName | String | 필수 | 없음 | 최대 50자  | API Gateway 서비스 이름 |
| description | String | 선택 | 없음 | 최대 200자  | API Gateway 서비스 설명 |


#### 응답

[Response Body]

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
    "name": "test api gateway",
    "description": "description of test api gateway",
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

[필드]
|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    | API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  | API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  | API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  | API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    | [API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType) |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | 전용 API Gateway 서비스의 ID                        |
|apigwService.description         |String  | 서비스 설명                                        |
|apigwService.name                |String  | API Gateway 서비스 이름                                        |
|apigwService.regionCode          |Enum    | [API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode) |
|apigwService.serverGroupId       |String  | API Gateway 서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime| API Gateway 서비스 생성일시                                      |
|apigwService.updatedAt           |DateTime| API Gateway 서비스 수정일시                                      |


### 서비스 수정
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
  "serviceName": "update service name",
  "description": "test of api gateway service"
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| serviceName | String | 필수 | 없음 | 최대 50자  | API Gateway 서비스 이름 |
| description | String | 선택 | 없음 | 최대 200자  | API Gateway 서비스 설명 |


#### 응답

[Response Body]

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
    "name": "test api gateway",
    "description": "description of test api gateway",
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

[필드]
|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    |API Gateway 서비스 영역                         |
|apigwService.apigwDomain         |String  |API Gateway 서비스 도메인                  |
|apigwService.apigwServiceAlias   |String  |API Gateway 서비스 별칭                            |
|apigwService.apigwServiceId      |String  |API Gateway 서비스 ID                            |
|apigwService.apigwServiceTypeCode|Enum    |[API Gateway 서비스 타입 Enum 코드 참조](./enum-code/#apigwServiceType)|
|apigwService.appKey              |String  |AppKey                                        |
|apigwService.dedicatedId         |String  |전용 API Gateway 서비스의 ID                        |
|apigwService.description         |String  |서비스 설명                                        |
|apigwService.name                |String  |서비스 이름                                        |
|apigwService.regionCode          |Enum    |[API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode)|
|apigwService.serverGroupId       |String  |서비스가 속한 서버 그룹 ID                              |
|apigwService.createdAt           |DateTime|서비스 생성일시                                      |
|apigwService.updatedAt           |DateTime|서비스 수정일시                                      |

### 서비스 삭제
- API Gateway 서비스를 삭제합니다.  
- API Gateway 서비스를 삭제하면 모든 스테이지가 삭제됩니다.  
- 삭제하려는 API Gateway 서비스의 스테이지가 사용량 계획과 연결된 경우, 삭제할 수 없습니다. 삭제하려면 사용량 계획에서 연결된 스테이지를 모두 연결 해제후 삭제해주세요.
- 삭제된 API Gateway 서비스는 복구할 수 없으므로 주의해주세요.

#### 요청

[URI]

| 메서드    | URI                                  |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services |

[Query Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | 필수 | 없음 | KR1 | [API Gateway 리전 Enum 코드 참조](./enum-code/#regionCode) |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |

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