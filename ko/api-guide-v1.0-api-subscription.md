## API Key 구독 

### API Key 구독 목록 조회
- API Key가 연결된 스테이지와 사용량 계획 정보가 있는 구독 목록을 조회합니다.

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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |
| stageUrl | String | 선택 | 없음 | 없음 | Stage Url |

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
            "apigwName": "test api gateway",
            "stageId": "{stageId}",
            "stageName": null,
            "stageUrl": "kr1-example.api.nhncloudservice.com",
            "stageCustomUrl": null,
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
| paging.limit                                                 | Integer | 페이지 당 건 수                                         |
| paging.totalCount                                            | Integer | 전체 건 수                                            |
| subscribedStageAndUsagePlanList                              | List    | API Key가 연결된 스테이지와 사용량 계획 목록 영역                |
| subscribeStageAndUsagePlanList[0].subscriptionId            | String  | 구독 ID                                     |
| subscribedStageAndUsagePlanList[0].subscriptionStatus        | Enum    | [API Key 구독 상태](./enum-code/#???) 참조              |
| subscribedStageAndUsagePlanList[0].apiKeyId                  | String  | API Key ID                                        |
| subscribedStageAndUsagePlanList[0].apigwName                 | String  | API Gateway 서비스 이름                                |
| subscribedStageAndUsagePlanList[0].stageId                   | String  | 스테이지 ID                                           |
| subscribedStageAndUsagePlanList[0].stageName                 | String  | 스테이지 이름                                           |
| subscribedStageAndUsagePlanList[0].stageUrl                  | String  | 스테이지 URL                                          |
| subscribedStageAndUsagePlanList[0].stageCustomUrl            | String  | 스테이지 사용자 정의 URL                                   |
| subscribedStageAndUsagePlanList[0].usagePlanId               | String  | 사용량 계획 ID                                         |
| subscribedStageAndUsagePlanList[0].usagePlanName             | String  | 사용량 계획 이름                                         |
| subscribedStageAndUsagePlanList[0].usagePlanDescription      | String  | 사용량 계획 설명                                         |
| subscribedStageAndUsagePlanList[0].rateLimitRequestPerSecond | Integer | 초당 요청 수 제한                                        |
| subscribedStageAndUsagePlanList[0].quotaLimitPeriodUnitCode  | Enum    | [사용량 계획 > 할당량 기간 단위 Enum 코드](./enum-code/#???) 참조 |
| subscribedStageAndUsagePlanList[0].quotaLimit                | Integer | 할당량 기간 단위 별 요청 할당량                                |


### 스테이지와 사용량 계획 구독하는 목록 조회
- 스테이지와 사용량 계획를 구독하고 있는 목록을 조회합니다.
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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | primary 또는 secondary API Key 값 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름 시작 문자열 |
| apiSubscriptionStatus | Enum | 선택 | 없음 | APPROVAL | [API Key 구독 상태](./enum-code/#???) 참조 |

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
      "subscriptionId": "a4294d79-cf3f-42a2-a3c2-7d5573913007",
      "subscriptionStatus": "APPROVAL",
      "subscriptionDescription": null,
      "stageId": "976a9050-9a68-417f-807a-6cb7badda379",
      "usagePlanId": "5f90b859-8320-4404-9557-713378f9ef8e",
      "apiKeyId": "7bd6c8c4-7e11-44ef-a86a-86316b4a91fe",
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
| paging.limit                                   | Integer  | 페이지 당 건 수                            |
| paging.totalCount                              | Integer  | 전체 건 수                               |
| apiSubscriptionList                            | List     | 구독 정보 목록 영역      |
| apiSubscriptionList[0].subscriptionId          | String   | 구독 ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Key 구독 상태](./enum-code/#???) 참조 |
| apiSubscriptionList[0].subscriptionDescription | String   | 구독 설명                                |
| apiSubscriptionList[0].stageId                 | String   | 스테이지 ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 사용량 계획 ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key 이름                           |
| apiSubscriptionList[0].createdAt               | DateTime | 구독 생성일시                              |
| apiSubscriptionList[0].updatedAt               | DateTime | 구독 수정일시                              |


### 스테이지와 사용량 계획에 API Key 목록 연결
- 스테이지와 사용량 계획에 연결될 API Key ID 목록을 보내 구독 요청합니다.

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
| apiKeyIdList             | List  | 필수    | 없음  | 최대 100개       | API Key ID 목록 영역                                        |
| apiKeyIdList[0]             | String  | 필수    | 없음  | 없음       | API Key ID                                        |

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
| apiSubscriptionList[0].subscriptionId          | String   | 구독 ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | [API Key 구독 상태](./enum-code/#???) 참조 |
| apiSubscriptionList[0].subscriptionDescription | String   | 구독 설명                                |
| apiSubscriptionList[0].stageId                 | String   | 스테이지 ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | 사용량 계획 ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key 이름                           |
| apiSubscriptionList[0].createdAt               | DateTime | 구독 생성일시                              |
| apiSubscriptionList[0].updatedAt               | DateTime | 구독 수정일시                              |


### 스테이지와 사용량 계획에 구독 해제

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


### API Key와 연결된 사용량 계획 변경
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
| changeUsagePlanId            | String  | 필수    | 없음  | 없음       | 변경할 시용량 계획 ID                                        |

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
