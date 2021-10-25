## 리소스 파라미터 API

### 리소스 파라미터 조회 
- 리소스 파라미터의 목록들을 조회합니다.

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
      "name": "q1",
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
    "modelId": "e316b1db-a41a-41c7-a81f-b62b924ec711"
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
| queryStringList[0].dataType    | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| queryStringList[0].required    | Boolean | 쿼리 문자열 필수 여부                                         |
| queryStringList[0].isArray     | Boolean | 쿼리 문자열 Array 여부                                      |
| headerList                     | List    | 헤더 목록 영역                                             |
| headerList[0].name             | String  | 헤더 이름                                                |
| headerList[0].description      | String  | 헤더 설명                                                |
| headerList[0].dataType         | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| headerList[0].required         | Boolean | 헤더 필수 여부                                             |
| headerList[0].isArray          | null    | 해더 Array 여부 미제공                                      |
| formDataList                   | List    | 폼 데이터 목록 영역                                          |
| formDataList[0].name           | String  | 폼 데이터 이름                                             |
| formDataList[0].description    | String  | 폼 데이터 설명                                             |
| formDataList[0].dataType       | Enum    | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| formDataList[0].required       | Boolean | 폼 데이터 필수 여부                                          |
| formDataList[0].isArray        | Boolean | 폼 데이터 Array 여부                                       |
| requestBody                    | Object  | 요청 본문 영역                                             |
| requestBody.name               | String  | 요청 본문 이름                                             |
| requestBody.description        | String  | 요청 본문 설명                                             |
| requestBody.modelId            | String  | 요청 본문과 연결된 모델 ID                                     |
| contentTypeList                | List    | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]             | String  | 콘텐츠 타입                                               |



### 리소스 파라미터 생성
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
      "name": "string",
      "description": "string",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "headerList": [
    {
      "name": "string",
      "description": "string",
      "dataType": "BOOLEAN",
      "required": true
    }
  ],
  "formDataList": [
    {
      "name": "string",
      "description": "string",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "requestBody": {
    "name": "string",
    "description": "string",
    "modelId": "string"
  },
  "contentTypeList": [
    "application/json"
  ]
}
```

| 이름                             | 타입      | 필수 여부 | 기본값          | 유효 범위                                               | 설명                                                   |
| ------------------------------ | ------- | ----- | ------------ | --------------------------------------------------- | ---------------------------------------------------- |
| queryStringList                | List    | 선택    | Empty List   | 최대 50개                                              | 쿼리 문자열 목록 영역                                         |
| queryStringList[0].name        | String  | 필수    | 없음           | 최대 50자                                              | 쿼리 문자열 이름                                            |
| queryStringList[0].description | String  | 선택    | null         | 최대 200자                                             | 쿼리 문자열 설명                                            |
| queryStringList[0].dataType    | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE       | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| queryStringList[0].required    | Boolean | 필수    | 없음           | true, false                                         | 쿼리 문자열 필수 여부                                         |
| queryStringList[0].isArray     | Boolean | 필수    | 없음           | true, false                                         | 쿼리 문자열 Array 여부                                      |
| headerList                     | List    | 선택    | Empty List   | 최대 50개                                              | 헤더 목록 영역                                             |
| headerList[0].name             | String  | 필수    | 없음           | 최대 50자                                              | 헤더 이름                                                |
| headerList[0].description      | String  | 선택    | null         | 최대 200자                                             | 헤더 설명                                                |
| headerList[0].dataType         | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE       | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| headerList[0].required         | Boolean | 필수    | 없음           | true, false                                         | 헤더 필수 여부                                             |
| formDataList                   | List    | 선택    | Empty List   | 최대 50개                                              | 폼 데이터 목록 영역                                          |
| formDataList[0].name           | String  | 필수    | 없음           | 최대 50자                                              | 폼 데이터 이름                                             |
| formDataList[0].description    | String  | 선택    | null         | 최대 200자                                             | 폼 데이터 설명                                             |
| formDataList[0].dataType       | Enum    | 필수    | 없음           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE, FILE | [리소스 요청/응답 파라미터 데이터 타입 Enum 코드 참조](./enum-code/#???) |
| formDataList[0].required       | Boolean | 필수    | 없음           | true, false                                         | 폼 데이터 필수 여부                                          |
| formDataList[0].isArray        | Boolean | 필수    | 없음           | true, false                                         | 폼 데이터 Array 여부. dataType이 FILE인 경우 false.            |
| requestBody                    | Object  | 선택    | Empty Object | 없음                                                  | 폼 데이터 목록 영역                                          |
| requestBody.name               | String  | 필수    | 없음           | 최대 50자                                              | 폼 데이터 이름                                             |
| requestBody.description        | String  | 선택    | null         | 최대 200자                                             | 폼 데이터 설명                                             |
| requestBody.modelId            | String  | 필수    | 없음           | 존재하는 modelId                                        | 폼 데이터 설명                                             |
| contentTypeList                | List    | 선택    | Empty List   | 최대 10개                                              | 콘텐츠 타입 목록 영역                                         |
| contentTypeList[0]             | String  | 필수    | 없음           | */* 형태                                              | 콘텐츠 타입                                               |

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