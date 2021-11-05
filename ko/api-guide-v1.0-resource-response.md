## 리소스 응답 API

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
| responseList[0].headerList[0].dataType    | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
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

| 이름                                        | 타입      | 필수 여부 | 기본값          | 유효 범위                                         | 설명                                                   |
| ----------------------------------------- | ------- | ----- | ------------ | --------------------------------------------- | ---------------------------------------------------- |
| responseList                              | List    | 선택    | Empty List   | 없음                                            | HTTP 응답 상태 코드별 응답 정보 목록 영역                           |
| responseList[0].responseStatusCode        | Integer | 필수    | 없음           | 100~599                                       | HTTP 응답 상태 코드                                        |
| responseList[0].description               | String  | 선택    | 없음         | 최대 200자                                       | HTTP 응답 상태 코드 설명                                     |
| responseList[0].headerList                | List    | 선택    | Empty List   | 최대 50개                                        | HTTP 응답 헤더 목록 영역                                     |
| responseList[0].headerList[0].name        | String  | 필수    | 없음           | 최대 50자                                        | 응답 헤더 이름                                             |
| responseList[0].headerList[0].description | String  | 선택    | 없음         | 최대 200자                                       | 응답 헤더 설명                                             |
| responseList[0].headerList[0].dataType    | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
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