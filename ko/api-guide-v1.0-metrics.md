## 통계

### 스테이지 리소스별 조회
- 조회 기간 동안의 리소스별 통계 데이터를 조회합니다.


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/metrics |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| stageId | String | 필수 | 없음 | 없음 | 스테이지 ID |

[QueryString Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| startTime | String | 필수 | 없음 | 없음 | 통계 조회 시작 일시 |
| endTime | String | 필수 | 없음 | 없음 | 통계 조회 종료 일시 |
| page | Integer | 선택 | 1 | 없음 | 페이지 |
| limit | Integer | 선택 | 10 | 최대 1000 | 페이지 당 건 수 |

* startTime, endTime 필드의 조회 기간은 최대 3개월까지 조회할 수 있습니다.
* stageTime, endTime 필드는 ISO8601형식의 날짜 문자열 형식으로 입력합니다. 
    * UTC 표기: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC 기준 타임 오프셋 표기: yyyy-MM-dd'T'HH:mm:ss±hh:mm


#### 응답

[Response]


``` json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 2
  },
  "data": [
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "GET",
      "successCount": 31,
      "failCount": 18,
      "status2xxCount": 29,
      "status3xxCount": 2,
      "status4xxCount": 18,
      "status5xxCount": 0,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 35,
      "networkOutboundByte": 26059
    },
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "POST",
      "successCount": 20,
      "failCount": 2,
      "status2xxCount": 18,
      "status3xxCount": 0,
      "status4xxCount": 0,
      "status5xxCount": 2,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 129,
      "networkOutboundByte": 3032
    }
  ]
}
```

|필드                                   |타입      |설명                                         |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                     |
|paging.page                          |Integer | 현재 페이지                                    |
|paging.limit                         |Integer | 페이지 당 건 수                                 |
|paging.totalCount                    |Integer | 전체 건 수                                     |
|data                                 |List    | 리소스별 통계 데이터 목록 영역                      |
|data[0].uriPattern                   |String  | 리소스 경로 또는 경로 패턴                         |
|data[0].httpMethodType               |String  | 리소스 경로의 메서드                              |
|data[0].successCount                 |Long    | API 성공 수 (응답 HTTP 상태 코드가 2xx, 3xx인 경우) |
|data[0].failCount|Long               |Long    | API 실패 수 (응답 HTTP 상태 코드가 4xx, 5xx인 경우) |
|data[0].status2xxCount               |Long    | 응답 HTTP 상태코드가 2xx인 API 호출 수 |
|data[0].status3xxCount               |Long    | 응답 HTTP 상태코드가 3xx인 API 호출 수 |
|data[0].status4xxCount               |Long    | 응답 HTTP 상태코드가 4xx인 API 호출 수 |
|data[0].status5xxCount               |Long    | 응답 HTTP 상태코드가 5xx인 API 호출 수 |
|data[0].statusEtcCount               |Long    | 2xx, 3xx, 4xx, 5xx 외 응답 HTTP 상태코드 API 호출 수 |
|data[0].avgResponseTimeMs            |Long    | 평균 API 응답 시간(ms) |
|data[0].networkOutboundByte          |Long    | 아웃바운드 네트워크 바이트 합계 (bytes) |


### API Key별 조회
- API Key별 일 단위 통계를 조회합니다.


#### 요청

[URI]
| 메서드  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/metrics |

[Path Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | 필수 | 없음 | 없음 | API Gateway 서비스 ID |
| apiKeyId | String | 필수 | 없음 | 없음 | API Key ID |

[QueryString Parameter]
| 이름 | 타입 | 필수 여부 | 기본값 | 유효 범위 | 설명 |
| --- | --- | --- | --- | --- | --- |
| startTime | String | 필수 | 없음 | 없음 | 통계 조회 시작 일시 |
| endTime | String | 필수 | 없음 | 없음 | 통계 조회 종료 일시 |

* startTime, endTime 필드의 조회 기간은 최대 3개월까지 조회할 수 있습니다.
* stageTime, endTime 필드는 ISO8601형식의 날짜 문자열 형식으로 입력합니다.
    * UTC 표기: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC 기준 타임 오프셋 표기: yyyy-MM-dd'T'HH:mm:ss±hh:mm

#### 응답

[Response]

``` json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "data": {
    "kr1-{apigwServiceId}-member.api.nhncloudservice.com": {
      "stageName": "member",
      "stageUrl": "kr1-{apigwServiceId1}.api.nhncloudservice.com",
      "stageCustomUrl": "kr1-mariadb.alpha-api.nhncloudservice.com",
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 8
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    },
    "kr1-{apigwServiceId}-billing.api.nhncloudservice.com": {
      "stageName": "billing",
      "stageUrl": "kr1-{apigwServiceId}-billing.api.nhncloudservice.com",
      "stageCustomUrl": null,
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 13
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    }
  }
}
```

|필드                                   |타입      |설명                                         |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | 페이징 영역                                     |
|paging.page                          |Integer | 현재 페이지                                     |
|paging.limit                         |Integer | 페이지 당 건 수                                 |
|paging.totalCount                    |Integer | 전체 건 수                                     |
|data                                 |Object  | API Key 통계 데이터 영역                         |
|data[0].{requestApigwEndpoint}       |String  | API 호출 엔드포인트별 통계 영역                |
|data[0].{requestApigwEndpoint}.stageName                    |String    | 스테이지 이름            |
|data[0].{requestApigwEndpoint}.stageUrl                     |String    | 스테이지 URL |
|data[0].{requestApigwEndpoint}.stageCustomUrl               |String    | 스테이지 커스텀 URL |
|data[0].{requestApigwEndpoint}.apiKeyMetricsTimeSeries      |Object    | 집계 시간 단위별 API Key 통계 영역|
|data[0].{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount               |List    | API 호출 수 통계 목록 영역 |
|data[0].{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].dateTime   |Long    | 통계 시간(Unix time 형식) |
|data[0].{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].count      |Long    | 통계 시간 동안의 총 API 호출 수 |
* 일 단위 통계 데이터는 각 일의 00:00:00의 시간 데이터에 집계됩니다.
