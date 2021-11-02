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
    "totalCount": 5
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
| paging.limit                               | Integer  | 페이지 당 건 수                                         |
| paging.totalCount                          | Integer  | 전체 건 수                                            |
| usagePlanList                              | List     | 사용량 계획 목록 영역                                      |
| usagePlanList[0]                           | Object   | 사용량 계획 영역                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlanList[0].usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlanList[0].usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| usagePlanList[0].quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlanList[0].createdAt                 | DateTime | 사용량 계획 생성일시                                       |
| usagePlanList[0].updatedAt                 | DateTime | 사용량 계획 수정일시                                       |


### 사용량 계획 생성

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans |

[Request Body]
``` json
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
| usagePlanName             | String  | 선택    | 없음  | 최대 200자      | 사용량 계획 설명                                         |
| rateLimitRequestPerSecond | Integer | 선택    | 없음  | 1~5000       | 초당 요청 수 제한                                        |
| quotaLimitPeriodUnitCode  | Enum    | 선택    | 없음  | DAY, MONTH   | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| quotaLimit                | Integer | 선택    | 없음  | 1~2147483647 | 할당량 기간 단위 별 요청 할당량                                |

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
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정일시                                       |



### 단일 사용량 계획 조회
- 사용량 계획을 조회합니다.

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
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정일시                                       |


### 사용량 계획 수정

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
``` json
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
| quotaLimitPeriodUnitCode  | Enum    | 선택    | 없음  | DAY, MONTH   | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| quotaLimit                | Integer | 선택    | 없음  | 1~2147483647 | 할당량 기간 단위 별 요청 할당량                                |

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
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| usagePlan.quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlan.createdAt                 | DateTime | 사용량 계획 생성일시                                       |
| usagePlan.updatedAt                 | DateTime | 사용량 계획 수정일시                                       |


### 사용량 계획 삭제
- 사용량 계획과 연결된 스테이지들을 모두 해제한 후 사용량 계획을 삭제할 수 있습니다.

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
      "apigwServiceId": "{apigwServiceId}",
      "apigwName": "APIGW Example",
      "stageId": "{stageId}",
      "stageName": "custom",
      "stageUrl": "kr1-example-custom.api.nhncloudservice.com",
      "stageCustomUrl": "custom.api.nhncloudservice.com",
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
| paging.limit                          | Integer | 페이지 당 건 수              |
| paging.totalCount                     | Integer | 전체 건 수                 |
| usagePlanStageList                    | List    | 사용량 계획과 연결된 스테이지 목록 영역 |
| usagePlanStageList.[0]                | Object  | 사용량 계획과 연결된 스테이지 영역    |
| usagePlanStageList.[0].apigwServiceId | String  | API Gateway 서비스 ID     |
| usagePlanStageList.[0].apigwName      | String  | API Gateway 서비스 이름     |
| usagePlanStageList.[0].stageId        | String  | 스테이지 ID                |
| usagePlanStageList.[0].stageName      | String  | 스테이지 이름                |
| usagePlanStageList.[0].stageUrl       | String  | 스테이지 URL               |
| usagePlanStageList.[0].stageCustomUrl | String  | 스테이지 사용자 정의 URL        |
| usagePlanStageList.[0].usagePlanId    | String  | 사용량 계획 ID              |
| usagePlanStageList.[0].usagePlanName  | String  | 사용량 계획 이름              |


### 사용량 계획에 스테이지 연결

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

### 스테이지에 연결된 사용량 계획 목록 조회

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/stages/{stageId} |


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
| paging.limit                               | Integer  | 페이지 당 건 수                                         |
| paging.totalCount                          | Integer  | 전체 건 수                                            |
| usagePlanList                              | List     | 사용량 계획 목록 영역                                      |
| usagePlanList[0]                           | Object   | 사용량 계획 영역                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | 사용량 계획 ID                                         |
| usagePlanList[0].usagePlanName             | String   | 사용량 계획 이름                                         |
| usagePlanList[0].usagePlanDescription      | String   | 사용량 계획 설명                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | 초당 요청 수 제한                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| usagePlanList[0].quotaLimit                | Integer  | 할당량 기간 단위 별 요청 할당량                                |
| usagePlanList[0].createdAt                 | DateTime | 사용량 계획 생성일시                                       |
| usagePlanList[0].updatedAt                 | DateTime | 사용량 계획 수정일시                                       |