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