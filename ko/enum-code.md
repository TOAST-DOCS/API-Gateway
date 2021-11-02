## Application Service > API Gateway > Enum 코드

## Enum 코드
API v1.0 가이드 문서에서 참조되는 Enum 코드 문서입니다.

### API Gateway 리전
- API Gateway 서버가 위치할 리전 코드 입니다. 

| 이름 | 설명 |
| --- | --- |
| KR1 | 한국(판교) 리전 |


### API Gateway 서비스 타입
- 공용 또는 전용 구분에 따른 API Gateway의 서비스 타입입니다. 
- 현재는 공용 API Gateway 서비스 타입만 지원됩니다. 

| 이름 | 설명 |
| --- | --- |
| SHARED | 공용 API Gateway 서비스 타입 |


### 리소스 HTTP 메서드 타입
- 리소스 HTTP 메서드 타입입니다.

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
| 이름 | 설명 |
| --- | --- |
| HTTP | API Gateway로 수신된 요청을 정의된 백엔드 엔드포인트 URL 경로로 전달합니다. |
| MOCK | API Gateway로 수신된 요청에 대해 정의된 응답을 반환합니다. | 
| CORS | Cross-Site 방식 내에서 XMLHttpRequest API 호출을 할 수 있게 합니다. | 
| SET_REQUEST_HEADER | 요청 헤더를 추가하거나 변경합니다.  | 
| SET_RESPONSE_HEADER | 응답 헤더 변경 플러그인은 백엔드 응답에 헤더를 추가하거나 변경합니다. | 
| ADD_REQUEST_QUERY_PARAMETER | 백엔드 엔드포인트 요청에 쿼리 문자열 파라미터를 추가합니다.   | 

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

| 이름 | 설명 |
| --- | --- |
| IP_ACL | IP 접근 제한 플러그인 | 
| HMAC | HMAC 요청 검증 플러그인 |
| JWT | JWT 토큰 검증 플러그인 | 
| API_KEY | API Key 검증 플러그인 | 
| PRE_API | 사전 호출 API 플러그인  | 
| RATE_LIMIT | 요청 수 제한 플러그인 타입 | 


### JWT > 암호화 알고리즘 
- JWT토큰을 서명하는데 사용하는 알고리즘입니다. 

| 이름 | 설명 |
| --- | --- |
| HS256 | 대칭키 알고리즘이며, HS256(HMAC with SHA-256)알고리즘을 사용하여 토큰을 서명합니다.  |
| RS256 | 비대칭키 알고리즘이며, 공개/개인키를 사용하여 RSA256(RSA Signature with SHA-256)알고리즘을 사용하여 토큰을 서명합니다. | 


### JWT > 클레임 데이터 타입 
- 클레임의 데이터 형식입니다.

| 이름 | 설명 |
| --- | --- |
| Array | 배열 형식의 데이터 타입입니다.  |
| String | 문자열 형식의 데이터 타입입니다. | 
| NumericDate | 밀리초를 무시하고 1970-01-01T00:00:00Z UTC부터 지정된 UTC 날짜/시간까지의 초 수를 나타내는 데이터 타입니다. |


### JWT > RS256 암호화 알고리즘 > Public Key Type 
- RS256는 공개키/개인키 기반 암호화 알고리즘을 사용합니다. 공개키 설정 방식을 설정합니다.
| 이름 | 설명 |
| --- | --- |
| RSA_PUBLIC_KEY | PEM 형식의 공개키를 설정하는 방식입니다. |
| JWKS_URI | 공개키를 조회할 수 있는 Json Web Key Sets URI로 설정하는 방식입니다.|


### 사전 호출 API > HttpMethod
- 지정된 사전 호출 API의 HttpMethod를 설정합니다.
| 이름 | 설명 |
| --- | --- |
| GET | GET 메서드 |
| POST | POST 메서드 |
| PUT | PUT 메서드 |
| DELETE | DELETE 메서드 |
| HEAD | HEAD 메서드 |
| OPTIONS | OPTIONS 메서드 |
| PATCH | PATCH 메서드 |


### 요청 수 제한 > 제한 키

| 이름 | 설명 |
| --- | --- |
| DEFAULT | 리소스 메서드의 요청 수 제한을 적용합니다. |
| IP | 클라이언트 IP마다 리소스 메서드의 요청 수 제한을 적용합니다. |
| HEADER | 지정된 헤더 이름의 값마다 리소스 메서드의 요청 수 제한을 적용합니다. |
| PATH_VARIABLE | 경로 변수마다  리소스 메서드의 요청 수 제한을 적용합니다. |

### 스테이지 배포 > 배포 상태
- 요청된 스테이지 배포 작업의 상태입니다.

| 이름 | 설명 |
| --- | --- |
| DEPLOYING | 배포 진행중 | 
| COMPLETE | 배포 완료(성공) | 
| FAILURE | 배포 실패 | 

### 사용량 계획 > 할당량 기간 단위

| 이름 | 설명 |
| --- | --- |
| DAY | 일 단위로 호출량 제한. 매일 UTC 00:00:00에 초기화.| 
| MONTH | 월 단위로 호출량 제한. 매월 1일 UTC 00:00:00에 초기화. | 


### API Key 상태

| 이름 | 설명 |
| --- | --- |
| ACTIVE | 활성화 상태 | 
| INACTIVE | 비활성화 상태 |

### API Key 타입

| 이름 | 설명 |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |