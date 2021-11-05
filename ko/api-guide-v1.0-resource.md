## 리소스 API

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
| resourceList[0].createdAt                              | DateTime | 리소스 생성일시                                       |
| resourceList[0].updatedAt                              | DateTime | 리소스 수정일시                                       |
| resourceList[2].methodType                             | Enum     | [HTTP 메서드 타입 Enum 코드](./enum-code/#???) 참고 |
| resourceList[2].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[2].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[2].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[2].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[2].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[2].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드](./enum-code/#???) 참고    |
| resourceList[2].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값]()                    |
| resourceList[2].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성일시                                  |
| resourceList[2].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정일시                                  |


### 리소스 삭제
- 리소스를 삭제합니다.
- 루트("/") 경로 리소스는 삭제가 불가합니다.
- CORS플러그인에 의해 생성된 OPTIONS 메서드는 삭제할 수 없습니다. 
CORS플러그인에 의해 생성된 OPTIONS 메서드는 CORS플러그인이 설정된 리소스에서 플러그인을 제거하면 일괄 삭제됩니다.
- 경로 리소스를 삭제하면 하위 경로와 메서드 리소스가 모두 삭제 됩니다.
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
- Swagger paths > path > operation에서 유효하지 않은 operation의 데이터는 무시되고 등록되지 않으므로 주의해주세요.

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
| swaggerData | Object  | 필수    | 없음 | Swagger Json 형식 | [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) |
| swaggerData.info | Object | 필수 | 없음 | 없음 | API의 메타 데이터 영역. [Info Object](https://swagger.io/specification/v2/#swagger-object) 참고 |
| swaggerData.info.title | String | 선택 | 없음 | 없음 | API의 제목. [Info Object](https://swagger.io/specification/v2/#info-object) 참고 |
| swaggerData.info.version | String  | 선택 | 없음 | 없음 | API의 버전 정보. [Info Object](https://swagger.io/specification/v2/#info-object) 참고 |
| swaggerData.paths | Object | 필수 | 없음 | 없음 | API Gateway 경로를 설정하는 API의 경로 정보들을 갖는 객체 영역. [Paths Object](https://swagger.io/specification/v2/#paths-object) 참고 |
| swaggerData.paths.{path} | Object | 필수 | 없음 | {path} 최대 255자 | API Gateway 경로인 {path}와 {path} 내 메서드들 정보를 갖는 객체 영역. [Paths Item Object](https://swagger.io/specification/v2/#path-item-object) 참고 |
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
| swaggerData.paths.{path}.{operation}.responses | Object | 선택 | 없음 | 없음 | API Gateway 리소스 응답 > 응답 HTTP 상태 코드 정보들을 갖는 객체 영역. [Responses Object](https://swagger.io/specification/v2/#response-object) 참고 |
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
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins.{pluginCode} | Object | 필수 | 없음 | {pluginCode} HTTP, MOCK, CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | [리소스 플러그인 타입 Enum 코드](./enum-code/#???) 참고. [리소스 플러그인 타입별 JSON 설정값](???) 참고. |
| swaggerData.definitions | Object | 선택 | 없음 | 없음 | API Gateway 리소스 요청 파라미터, 응답에서 사용되는 본문 객체들 정의 영역. [Definitions Object](https://swagger.io/specification/v2/#definitionsObject) 참고 |




## 리소스 플러그인

### HTTP
- API Gateway애서 요청을 수신할 리소스 경로에 대해 요청을 전달할 백엔드 엔드포인트 경로를 설정합니다.
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
| frontendEndpointPath | String | 필수 | 없음 | 최대 255자 | API Gateway애서 요청을 수신할 리소스 경로 |
| backendEndpointPath  | String | 필수 | 없음 | 최대 255자 | API Gateway애서 수신된 요청을 전달할 백엔드 엔드포인트 경로 |

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
| headers | Map | 선택 | 없음 | 없음 |사용자 정의 응답 헤더들 객체 영역                  |
| headers[{HeaderName}] | String | 필수 | 없음 | 없음 | 객체 프로퍼티 키/값이 사용자 정의 응답 헤더의 이름과 값 |
| body                  | String | 선택 | 없음 | 없음 | 사용자 정의 응답 본문                         |

### CORS
- Cross-Site 방식 내에서 XMLHttpRequest API 호출을 할 수 있게 합니다.
- 리소스 경로에만 설정할 수 있습니다.
- CORS 플러그인 설정된 경로 하위에는 OPTIONS 메서드가 자동으로 생성되며, 등록된 OPTIONS메서드가 있는 경우 대체됩니다.
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
| allowedMethods[0] | Enum | 필수 | 없음 | "GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH" | [HTTP 메서드 타입 Enum 코드](./enum-code/#???) 참고 |
| allowedHeaders | List | 필수 | 없음 | 없음 | 요청에서 사용할 수 있는 HTTP 헤더 목록 영역 |
| allowedHeaders[0] | String | 필수 | 없음 | 없음 | 요청에서 사용할 수 있는 HTTP 헤더. (예시: 와일드카드 형식: '\*' 또는 'X-NHN-HEADER, Content-Type') |
| allowedOrigins    | List | 필수 | 없음 | 없음 | 리소스에 액세스할 수 있는 원본 서버의 도메인 목록 영역 |
| allowedOrigins[0] | String | 필수 | 없음 | 없음 | 리소스에 액세스할 수 있는 원본 서버의 도메인. (예시: 와일드카드 형식: '\*' 또는 ') |
| exposedHeaders    | List | 선택 | 없음 | 없음 | 브라우저(클라이언트)가 접근할 수 있는 헤더 목록 영역 |
| exposedHeaders[0] | String | 필수 | 없음 | 없음 |브라우저(클라이언트)가 접근할 수 있는 헤더 |
| maxCredentialsAge | Integer | 선택 | 없음 | -1~86400 |사전 전달 요청(Preflight)에 대한 응답 브라우저 캐시 시간 (초 단위) |
| allowCredentials  | Boolean | 필수 | 없음 |true/false | 자격 증명으로 요청하는 여부 |



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
| headers | Map | 필수 | 없음 | 없음 | 추가/변경할 요청 헤더들 객체 영역 |
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
| headers | Map | 필수 | 없음 | 없음 | 추가/변경할 응답 헤더들 객체 영역 |
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