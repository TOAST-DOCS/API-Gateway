## 리소스 API

### 리소스 조회

- 리소스 목록을 조회합니다.

#### 요청

[URI]
| 메서드 | URI | | --- | --- | | GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

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
| resourceList[2].methodType                             | Enum     | [리소스 HTTP 메서드 타입 Enum 코드 참조](./enum-code/#???) |
| resourceList[2].methodName                             | String   | 메서드 리소스 이름                                     |
| resourceList[2].methodDescription                      | String   | 메서드 리소스 설명                                     |
| resourceList[2].resourcePluginList                     | List     | 리소스 플러그인 목록 영역                                 |
| resourceList[2].resourcePluginList[0].resourcePluginId | String   | 리소스 플러그인 ID                                    |
| resourceList[2].resourcePluginList[0].resourceId       | String   | 리소스 ID                                         |
| resourceList[2].resourcePluginList[0].pluginType       | Enum     | [리소스 플러그인 타입 Enum 코드 참조](./enum-code/#???)     |
| resourceList[2].resourcePluginList[0].pluginConfigJson | Object   | [리소스 플러그인 타입별 JSON 설정값]()                    |
| resourceList[2].resourcePluginList[0].createdAt        | DateTime | 리소스 플러그인 생성일시                                  |
| resourceList[2].resourcePluginList[0].updatedAt        | DateTime | 리소스 플러그인 수정일시                                  |


### 리소스 삭제
- 리소스를 삭제합니다.
- 루트("/") 경로 리소스는 삭제가 불가합니다.
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
- Swagger v2.0 [OpenAPI Specification](https://swagger.io/specification/v2/) 형식의 파일에서 리소스를 가져옵니다.
- 리소스를 가져오면 해당 서비스에 생성되어 있던 기존의 모델은 모두 삭제되고 가져온 모델로 덮어씁니다.

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
    "info": {},
    "paths": {
      "/bytes/{n}": {
        "get": {
          "summary": "Get Bytes"
        }
      }
    }
  }
}
```

| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |

@TODO


## 리소스 플러그인

### HTTP

```json
{
  "frontendEndpointPath": "/path",
  "backendEndpointPath": "/anything"
}
```

| 필드                   | 타입     | 설명                                     |
| -------------------- | ------ | -------------------------------------- |
| frontendEndpointPath | String | API Gateway애서 요청을 수신할 리소스 경로           |
| backendEndpointPath  | String | API Gateway애서 수신된 요청을 전달할 백엔드 엔드포인트 경로 |

### MOCK
```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"isSuccess\":true}\"}"
}
```

| 필드                    | 타입     | 설명                                   |
| --------------------- | ------ | ------------------------------------ |
| statusCode            | String | 사용자 정의 응답 HTTP 상태 코드                 |
| headers               | Map    | 사용자 정의 응답 헤더들 객체 영역                  |
| headers[{HeaderName}] | String | 객체 프로퍼티 키/값이 사용자 정의 응답 헤더의 이름과 값 |
| body                  | String | 사용자 정의 응답 본문                         |

### CORS
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

| 필드                | 타입      | 설명                                                                                             |
| ----------------- | ------- | ---------------------------------------------------------------------------------------------- |
| allowedMethods    | List    | 리소스 접근에 허용할 메서드 목록 영역                                                                          |
| allowedMethods[0] | Enum    | [리소스 HTTP 메서드 타입 Enum 코드 참조](./enum-code/#???)                                                 |
| allowedHeaders    | List    | 요청에서 사용할 수 있는 HTTP 헤더 목록 영역                                                                    |
| allowedHeaders[0] | String  | 요청에서 사용할 수 있는 HTTP 헤더. (예시: 와일드카드 형식: '\*' 또는 'X-NHN-HEADER, Content-Type')                    |
| allowedOrigins    | List    | 리소스에 액세스할 수 있는 원본 서버의 도메인 목록 영역                                                                |
| allowedOrigins[0] | String  | 리소스에 액세스할 수 있는 원본 서버의 도메인. (예시: 와일드카드 형식: '\*' 또는 ') |
| exposedHeaders    | List    | 브라우저(클라이언트)가 접근할 수 있는 헤더 목록 영역                                                                 |
| exposedHeaders[0] | String  | 브라우저(클라이언트)가 접근할 수 있는 헤더                                                                       |
| maxCredentialsAge | Integer | 사전 전달 요청(Preflight)에 대한 응답 브라우저 캐시 시간 (초 단위)                                                   |
| allowCredentials  | Boolean | 자격 증명으로 요청하는 여부                                                                                |

### SET_REQUEST_HEADER
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 필드                    | 타입     | 설명                               |
| --------------------- | ------ | -------------------------------- |
| headers               | Map    | 추가/변경할 요청 헤더들 객체 영역              |
| headers[{HeaderName}] | String | 객체 프로퍼티 키/값이 추가/변경할 요청 헤더의 이름과 값 |

### SET_RESPONSE_HEADER
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| 필드                    | 타입     | 설명                               |
| --------------------- | ------ | -------------------------------- |
| headers               | Map    | 추가/변경할 응답 헤더들 객체 영역              |
| headers[{HeaderName}] | String | 객체 프로퍼티 키/값이 추가/변경할 응답 헤더의 이름과 값 |

### ADD_REQUEST_QUERY_PARAMETER
```json
{
  "parameters": {
    "queryName1": "queryValue1"
  }
}
```

| 필드                      | 타입     | 설명                                     |
| ----------------------- | ------ | -------------------------------------- |
| parameters              | Map    | 추가할 요청 쿼리 문자열 파라미터들 객체 영역              |
| parameters[{QueryName}] | String | 객체 프로퍼티 키/값이 추가할 요청 쿼리 문자열 파라미터의 이름과 값 |
