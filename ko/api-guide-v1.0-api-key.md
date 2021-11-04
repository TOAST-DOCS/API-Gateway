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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | primary 또는 secondary API Key 값 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름 시작 문자열 |
| apiKeyStatus | Enum | 선택 | 없음 | ACTIVE, INACTIVE | [API Key 상태](./enum-code/#???) 참조 |

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
| paging.limit                    | Integer  | 페이지 당 건 수                                         |
| paging.totalCount               | Integer  | 전체 건 수                                            |
| apiKeyList                      | List     | API Key 목록 영역                                     |
| apiKeyList[0]                   | Object   | API Key 영역                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key 이름                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key 설명                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key 값                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |
| apiKeyList[0].createdAt         | DateTime | API Key 생성일시                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key 수정일시                                      |

### API Key 생성

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
| apiKeyStatus      | Enum   | 필수    | 없음  | ACTIVE, INACTIVE | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |

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
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |
| apiKey.createdAt         | DateTime | API Key 생성일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정일시                                      |


### API Key 수정
- API Key 상태를 INACTIVE로 변경하면 해당 API Key를 사용할 수 없습니다.

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
| apiKeyStatus      | Enum   | 필수    | 없음  | ACTIVE, INACTIVE | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |

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
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |
| apiKey.createdAt         | DateTime | API Key 생성일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정일시                                      |


### API Key 삭제
- 연결된 사용량 계획, 스테이지가 있는 경우 API Key를 삭제할 수 없습니다.

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
- 재발급할 경우 이전 API Key 값은 더 이상 유효하지 않게 됩니다.

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
| apiKeyType      | Enum   | 필수    | 없음  | PRIMARY, SECONDARY | [API Key 타입 Enum 코드](./enum-code/#???) 참조 |

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
| apiKey.apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |
| apiKey.createdAt         | DateTime | API Key 생성일시                                      |
| apiKey.updatedAt         | DateTime | API Key 수정일시                                      |

### 스테이지에 연결 가능한 API Key 목록 조회
- 스테이지에 연결 가능한 api key API Key 목록을 조회합니다.
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
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |
| apiKey | String | 선택 | 없음 | 없음 | primary 또는 secondary API Key 값 |
| apiKeyId | String | 선택 | 없음 | 없음 | API Key ID |
| apiKeyName | String | 선택 | 없음 | 없음 | API Key 이름 시작 문자열 |
| apiKeyStatus | Enum | 선택 | 없음 | ACTIVE, INACTIVE | [API Key 상태](./enum-code/#???) 참조 |

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
| paging.limit                    | Integer  | 페이지 당 건 수                                         |
| paging.totalCount               | Integer  | 전체 건 수                                            |
| apiKeyList                      | List     | API Key 목록 영역                                     |
| apiKeyList[0]                   | Object   | API Key 영역                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key 이름                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key 설명                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key 값                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key 값                               |
| apiKeyList[0].apiKeyStatus      | Enum     | [API Key 상태 Enum 코드](./enum-code/#???) 참조 |
| apiKeyList[0].createdAt         | DateTime | API Key 생성일시                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key 수정일시                                      |
