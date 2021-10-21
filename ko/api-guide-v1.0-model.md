## 모델 API

### 모델 목록 조회 
- 모델 목록을 조회합니다.

#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | ​/v1.0​/appkeys​/{appKey}​/services​/{apigwServiceId}​/models |

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
  "modelList": [
    {
      "modelId": "a56f71e9-e9f8-4028-9708-aa6b82f1186b",
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
|paging.limit                         |Integer | 페이지 당 건 수                                  |
|paging.totalCount                    |Integer | 전체 건 수                                        |
|modelList                     |List    | 모델 목록 영역                         |
|modelList[0].apigwServiceId  |String  |API Gateway 서비스 ID |
|modelList[0].modelId         |String  |모델 ID              |
|modelList[0].modelName       |String  |모델 이름              |
|modelList[0].modelDescription|String  |모델 설명              |
|modelList[0].modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|modelList[0].createdAt       |DateTime|모델 생성일시            |
|modelList[0].updatedAt       |DateTime|모델 수정일시            |



### 모델 생성
- 모델을 JSON Schema형식으로 생성합니다.
- 모델 이름은 중복될 수 없습니다.


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| POST | ​/v1.0​/appkeys​/{appKey}​/services​/{apigwServiceId}​/models |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |


[Request Body]
```json
{
  "modelName": "string",
  "modelDescription": "string",
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
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| modelName | String | 필수 | 없음 | 최대 50자  | 모델 이름 |
| modelDescription | String | 선택 | 없음 | 최대 200자  | 모델 설명 |
| modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |


#### 응답

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "a56f71e9-e9f8-4028-9708-aa6b82f1186b",
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
|model                     |List    | 모델 영역                         |
|model.apigwServiceId  |String  |API Gateway 서비스 ID |
|model.modelId         |String  |모델 ID              |
|model.modelName       |String  |모델 이름              |
|model.modelDescription|String  |모델 설명              |
|model.modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|model.createdAt       |DateTime|모델 생성일시            |
|model.updatedAt       |DateTime|모델 수정일시            |


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
``` json
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
[필드]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
|modelDescription|String  |모델 설명              |
|modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |


#### 응답

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "a56f71e9-e9f8-4028-9708-aa6b82f1186b",
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
      "updatedAt": "2021-10-11T23:51:47.000Z"
  }
}
```

|필드                                   |타입      |설명                                            |
|-------------------------------------|--------|----------------------------------------------|
|model                     |List    | 모델 영역                         |
|model.apigwServiceId  |String  |API Gateway 서비스 ID |
|model.modelId         |String  |모델 ID              |
|model.modelName       |String  |모델 이름              |
|model.modelDescription|String  |모델 설명              |
|model.modelSchema     |Object  |모델의 [JSON Schema](https://json-schema.org/) draft-04 JSON 객체 |
|model.createdAt       |DateTime|모델 생성일시            |
|model.updatedAt       |DateTime|모델 수정일시            |


### 모델 삭제
- 모델을 삭제합니다.
- 모델이 리소스의 요청 파라미터 또는 응답에서 참조된 경우에는 모델 삭제가 불가합니다. 모델을 삭제하려면 참조를 해제한 후 모델을 삭제해주세요.

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