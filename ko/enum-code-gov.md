## Application Service > API Gateway > Enum 코드

## Enum 코드
API v1.0 가이드 문서에서 참조되는 Enum 코드 문서입니다.

### API Gateway 리전
- API Gateway 서버가 위치하는 리전을 의미합니다.

| 이름 | 설명 |
| --- | --- |
| KR1 | 한국(판교) 리전 |
| KR2 | 한국(평촌) 리전 |

### API Gateway 서비스 타입
- 공용(Shared) 또는 전용(Dedicated) 구분에 따른 API Gateway의 서비스 타입입니다. 
- 현재는 공용 API Gateway 서비스 타입만 지원됩니다. 

| 이름 | 설명 |
| --- | --- |
| SHARED | 공용 API Gateway 서비스 타입 |


### HTTP 메서드 타입
- 지원되는 HTTP 메서드 타입입니다.

| 이름 | 설명 |
| --- | --- |
| GET | HTTP GET 메서드 |
| POST | HTTP POST 메서드 | 
| DELETE | HTTP DELETE 메서드 | 
| PUT | HTTP PUT 메서드 | 
| OPTIONS | HTTP OPTIONS 메서드 | 
| HEAD | HTTP HEAD 메서드 | 
| PATCH | HTTP PATCH 메서드 | 


### 리소스 플러그인 타입
- 리소스에 설정 가능한 플러그인 타입입니다.

| 이름 | 설명 | 플러그인 적용 가능한 위치 |
| --- | --- | --- |
| HTTP | API Gateway로 수신된 요청을 정의된 백엔드 엔드포인트 URL 경로로 전달합니다. | 메서드 |
| MOCK | API Gateway로 수신된 요청에 대해 정의된 응답을 반환합니다. | 메서드 |
| CORS | Cross-Site 방식 내에서 XMLHttpRequest API 호출을 할 수 있게 합니다. | 리소스 경로 |
| SET_REQUEST_HEADER | 요청 헤더를 추가하거나 변경합니다. | 리소스 경로, 메서드 |
| REMOVE_REQUEST_HEADER | 요청 헤더를 삭제합니다. | 리소스 경로, 메서드 |
| SET_RESPONSE_HEADER | 백엔드 응답에 헤더를 추가하거나 변경합니다. | 리소스 경로, 메서드 |
| REMOVE_RESPONSE_HEADER | 백엔드 응답에서 헤더를 삭제합니다. | 리소스 경로, 메서드 |
| ADD_REQUEST_QUERY_PARAMETER | 백엔드 엔드포인트 요청에 쿼리 문자열 파라미터를 추가합니다. | 리소스 경로, 메서드 |


### 리소스 요청/응답 파라미터 데이터 타입
- 리소스 요청/응답 파라미터에서 설정할 수 있는 데이터 타입입니다.

| 이름 | 설명 |
| --- | --- |
| STRING | String 데이터 타입 |
| BOOLEAN | Boolean 데이터 타입 | 
| INTEGER | Integer 데이터 타입 | 
| LONG | Long 데이터 타입 | 
| FLOAT | Float 데이터 타입 | 
| DOUBLE | Double 데이터 타입 | 
| FILE | File 데이터 타입. 요청 파라미터 > 폼 데이터에서만 설정 가능. | 


### 스테이지 리소스 > 플러그인 타입
- 스테이지 리소스 경로 또는 메서드에 설정 가능한 플러그인 타입입니다. 

| 이름 | 설명 | 플러그인 적용 가능한 위치 |
| --- | --- | --- |
| IP_ACL | IP 접근 제한 플러그인 | 루트(/) 리소스 경로 |
| HMAC | HMAC 요청 검증 플러그인 | 루트(/) 리소스 경로 |
| JWT | JWT 토큰 검증 플러그인 | 루트(/) 리소스 경로 |
| API_KEY | API Key 검증 플러그인 | 리소스 경로, 메서드 |
| REQUEST_VALIDATOR | 요청 유효성 검사기 플러그인 | 리소스 경로, 메서드 |
| PRE_API | 사전 호출 API 플러그인 | 리소스 경로, 메서드 |
| RATE_LIMIT | 요청 수 제한 플러그인 | 메서드 |


### JWT > 암호화 알고리즘 
- JWT 토큰 서명에 사용하는 암호화 알고리즘입니다.

| 이름 | 설명 |
| --- | --- |
| HS256 | 대칭키 알고리즘이며, HS256(HMAC with SHA-256) 알고리즘을 사용하여 토큰을 서명합니다.  |
| RS256 | 비대칭키 알고리즘이며, 공개/개인키를 사용하여 RSA256(RSA Signature with SHA-256) 알고리즘을 사용하여 토큰을 서명합니다. | 


### JWT > 클레임 데이터 타입 
- JWT 클레임의 데이터 타입입니다.

| 이름 | 설명 |
| --- | --- |
| Array | 배열 형식의 데이터 타입입니다.  |
| String | 문자열 형식의 데이터 타입입니다. | 
| NumericDate | 밀리초를 무시하고 1970-01-01T00:00:00Z UTC부터 지정된 UTC 날짜/시간까지의 초 수를 나타내는 데이터 타입입니다. |


### JWT > RS256 암호화 알고리즘 > Public Key Type 
- RS256는 공개키/개인키 기반 암호화 알고리즘을 사용합니다. 공개키 설정 방식을 설정합니다.

| 이름 | 설명 |
| --- | --- |
| RSA_PUBLIC_KEY | PEM 형식의 공개키를 설정하는 방식입니다. |
| JWKS_URI | 공개키를 조회할 수 있는 Json Web Key Sets URI로 설정하는 방식입니다.|


### 요청 수 제한 > 제한 키
- 요청 수 제한이 적용되는 키입니다.

| 이름 | 설명 |
| --- | --- |
| DEFAULT | 리소스 메서드의 요청 수 제한을 적용합니다. |
| IP | 클라이언트 IP마다 리소스 메서드의 요청 수 제한을 적용합니다. |
| HEADER | 지정된 헤더 이름의 값마다 리소스 메서드의 요청 수 제한을 적용합니다. |
| PATH_VARIABLE | 경로 변수마다 리소스 메서드의 요청 수 제한을 적용합니다. |


### 스테이지 배포 > 배포 상태
- 스테이지 배포 작업의 상태입니다.

| 이름 | 설명 |
| --- | --- |
| DEPLOYING | 배포 진행중 | 
| COMPLETE | 배포 완료(성공) | 
| FAILURE | 배포 실패 | 


### 사용량 계획 > 할당량 기간 단위
- 할당량이 초기화되는 기간 단위 입니다.

| 이름 | 설명 |
| --- | --- |
| DAY | 일 단위로 호출량 제한. 매일 UTC 00:00:00에 초기화.| 
| MONTH | 월 단위로 호출량 제한. 매월 1일 UTC 00:00:00에 초기화. | 


### API Key 상태
- API Key의 상태입니다.
- 비활성화된 API Key는 API Key 인증에 실패하여 API 호출이 불가합니다. 

| 이름 | 설명 |
| --- | --- |
| ACTIVE | 활성화 상태 | 
| INACTIVE | 비활성화 상태 |


### API Key 타입
- 발급된 API Key의 Primary API Key와 Secondary API Key의 타입입니다. 

| 이름 | 설명 |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |


### API Key 구독 상태
- API Key의 구독 상태입니다.

| 이름 | 설명 |
| --- | --- |
| APPROVAL | 승인 상태 | 

### 통계 데이터 시간 단위
- 통계 데이터가 수집되는 시간 단위

| 이름 | 설명 |
| --- | --- |
| ONE_MINUTES | 1분 간격으로 통계 데이터 수집  | 
| TEN_MINUTES | 10분 간격으로 통계 데이터 수집 | 
| ONE_HOURS | 1시간 간격으로 통계 데이터 수집 | 
| ONE_DAYS | 하루 간격으로 통계 데이터 수집 | 


### 통계 > Top10 서비스 정렬 기준 
| 이름 | 설명 |
| --- | --- |
| CALL_COUNT | 전체 API 호출 수 기준 내림차순 정렬 | 
| FAIL_CALL_COUNT | 실패 API 호출 수 기준 내림차순 정렬 | 
| AVG_RESPONSE_TIME | 평균 응답 시간 기준 내림차순 정렬 | 


### 게이트웨이 응답 유형
| 게이트웨이 응답 유형 | 기본 상태 코드 | 설명 |
| ----------- | -------- | --- |
| UpstreamServiceUnavailable | 503 | 백엔드 엔드포인트 서비스가 응답을 하지 않거나 응답 지연(60초 이상)이 지속적으로 발생하는 경우의 응답입니다. |
| Unauthorized | 401 | 인증에 필요한 요청 정보가 없거나 인증에 실패하는 경우 발생하는 응답입니다. |
| JwksError | 500 | JWT의 JWKS가 잘못된 설정된 경우 발생하는 응답입니다. |
| PreApiFailed | 502 | 사전 호출 API가 API Gateway의 요청에 응답하지 않을 경우 발생하는 응답입니다. 사전 호출 API의 응답 상태 코드가 200이 아닌 경우에는 사전 호출 API의 응답이 클라이언트에 그대로 전달됩니다. |
| Forbidden | 403 | 접근이 허가되지 않은 요청을 거부할 때 발생하는 응답입니다. |
| RateLimited | 429 | 제한된 요청 수를 초과하는 요청을 거부할 때 발생하는 응답입니다. |
| UsageQuotaExceeded | 429 | 제한된 요청 할당량을 초과하는 요청을 거부할 때 발생하는 응답입니다. |
| InvalidUri | 400 | 백엔드 엔드포인트의 URI 구성이 올바르지 않을 때 발생하는 응답입니다. |
| NotFound | 404 | 등록되지 않은 경로 및 메서드로 요청한 경우 발생하는 응답입니다. |
| BadGateway | 502 | 백엔드 엔드포인트가 응답하지 않거나 응답을 거부하는 경우 발생하는 응답입니다. |
| InvalidContextVariable | 500 | 잘못된 컨텍스트 변수 설정으로 인해 발생하는 응답입니다. |
| BadRequest | 400 | 잘못된 클라이언트 요청으로 인해 발생하는 응답입니다. |
| InternalServerError | 500 | 예상치 못한 오류가 발생한 경우 응답입니다. |
