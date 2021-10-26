## API 설명서

### API 설명서 조회
- 배포된 스테이지 설정 기준으로 API 설명서를 조회합니다. 
- API 설명서는 [Swagger v2.0](https://swagger.io/specification/v2/)사양의 Json객체로 응답됩니다.
- 배포되지 않은 스테이지는 API 설명서를 조회할 수 없으며, 404 Not Found가 응답됩니다.


#### 요청

[URI]

| 메서드    | URI                                 |
| ------ | ------------------------------------ |
| GET | ​/v1.0​/appkeys​/{appKey}​/services​/{apigwServiceId}​/stages​/{stageId}​/documents​/swagger |

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
  "host": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
  "schemes": [
    "https",
    "http"
  ],
  "paths": {
    "/members/{proxy+}": {
      "get": {
        "summary": "회원 API",
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
            "description": "요청 ID",
            "required": false,
            "type": "string"
          },
          {
            "in": "body",
            "name": "Member",
            "description": "회원 객체",
            "required": false,
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "조회 성공 응답",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "응답 ID"
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
            "description": "존재하지 않는 회원",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "응답 ID"
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
            "HTTP": "{\"frontendEndpointPath\":\"/members/{proxy+}\",\"backendEndpointPath\":\"/anything/${request.path.proxy+}\"}"
          }
        }
      },
      "post": {
        "summary": "회원 API",
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
            "HTTP": "{\"frontendEndpointPath\":\"/members/{proxy+}\",\"backendEndpointPath\":\"/api/${request.path.proxy+}\"}"
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
|info         | Object   | API의 메타 데이터 영역입니다. [Info Object](https://swagger.io/specification/v2/#swagger-object) 참고|
|info.version   |String  | API의 버전 정보이며, 스테이지 배포 요청 일시가 설정됩니다. [Info Object](https://swagger.io/specification/v2/#info-object) 참고|
|info.title      |String  | API의 제목이며, 스테이지 이름이 설정됩니다. [Info Object](https://swagger.io/specification/v2/#info-object) 참고|
|host|String    |API의 제공하는 호스트이며, 스테이지 URL이 설정됩니다. [Swagger Object](https://swagger.io/specification/v2/#swagger-object) 참고|
|schemes              |String[]  | API의 지원 전송 프로토콜이며, [http, https]이 설정됩니다. [Swagger Object > schemes](https://swagger.io/specification/v2/#swagger-object) 참고|
|paths         | Object  | API의 경로 이며, 리소스 메서드의 경로가 설정됩니다. [Paths Object](https://swagger.io/specification/v2/#pathsObject) 참고|
|paths.{operation}         |String  | API 경로의 오퍼레이션이며, 리소스 메서드로 설정됩니다. [Path Item Object](https://swagger.io/specification/v2/#path-item-object) 참고|
|paths.{operation}.consumes         | String[]  | API 경로의 오퍼레이션이 사용할 수 있는 MIME 유형 목록입니다. |
|paths.{operation}.produces         | String[]  | API 경로의 오퍼레이션이 생성할 수 있는 MIME 유형 목록입니다. |
|paths.{operation}.summary                |String  | API 요약이며, 리소스의 이름이 설정됩니다.  [Operation Object](https://swagger.io/specification/v2/#operation-object) 참고|
|paths.{operation}.description                |String  |API 설명이며, 리소스의 설명이 설정됩니다.  [Operation Object](https://swagger.io/specification/v2/#operation-object) 참고|
|paths.{operation}.parameters                | Object  | API 파라미터이며, 리소스의 경로 변수와 요청 파라미터가 설정됩니다.[Parameter Object](https://swagger.io/specification/v2/#parameter-object) 참고|
|paths.{operation}.responses                | Object  | API 응답이며, 리소스 응답이 설정됩니다. [Responses Object](https://swagger.io/specification/v2/#responses-object) 참고|
|paths.{operation}.security     | Object[]  | API 오퍼레이션의 작업에 사용되는 보안 정의입니다. API Key, 인증(HMAC, JWT)설정시 API Gateway의 사용자 정의 설정이 포함됩니다. |
|paths.{operation}.x-nhncloud-apigateway     | Object  | API Gateway의 사용자 정의 플러그인입니다. 리소스 > 플러그인 설정과 리소스와 매핑된 백엔드 엔드포인트 경로의 설정이 포함됩니다. |
|securityDefinitions          |Object    | 보안 정의 객체입니다. API Key, 인증(HMAC, JWT)설정시 API Gateway의 사용자 정의 설정이 포함됩니다. [Security Definitions Object](https://swagger.io/specification/v2/#securityDefinitionsObject) 참고|
|definitions | Object | 요청 및 응답에서 사용되는 데이터 유형에 대한 영역. 요청 파라미터/응답에서 참조된 모델이 정의가 설정됩니다. [Definitions Object](https://swagger.io/specification/v2/#definitionsObject) 참고| 