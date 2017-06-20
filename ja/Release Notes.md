## Upcoming Products > API Gateway > Release Notes

### 2017.06.22
#### 기능 개선/변경
* [Console] CORS 플러그인 추가
	* Cross-site간 HTTP Request가 가능하도록 설정할 수 있는 CORS 플러그인을 추가하였습니다.
	* 상세한 내용은 <a href="/ja/Upcoming%20Products/API%20Gateway/ja/Developer%60s%20Guide/#cors" target="_blank">Developer`s Guide > Plugin > CORS</a> 참고

### 2017.05.25
#### 기능 개선/변경
* [Console] domain key 입력시 path 형태 입력 불가하도록 변경
	* path 형태의 domain key는 지원하지 않고 있으므로 path 형태의 domain key를 입력하지 못하도록 변경하였습니다.  
* [Console] Swagger import & export 지원
	* domain 설정 정보를 swagger 파일로 import & export 할 수 있습니다.  
	* 상세한 내용은 <a href="/ja/Upcoming%20Products/API%20Gateway/ja/Getting%20Started/#swagger-import-export" target="_blank">Developer`s Guide > Swagger import & Export</a> 참고

#### 버그 수정
* [Console] endpoint 삭제 후 Deploy 버튼이 활성화되지 않는 버그 수정
	* endpoint가 삭제된 경우 설정 정보가 변경되었으므로 Deploy 버튼이 활성화되어야 하나 비활성화 상태로 남아있는 버그를 수정하였습니다.

### 2017.04.20
#### 기능 개선/변경
* [Console] 오류 발생시 상세 오류 메시지를 alert로 표시
* [Console] Deploy 수행시 순단이 발생되지 않도록 수정
* [Console] Endpoint Plugin > Usage Quota 플러그인 추가
	* 상세한 내용은 <a href="/ja/Upcoming%20Products/API%20Gateway/ja/Developer%60s%20Guide/#endpoint-usage-quota" target="_blank">Developer`s Guide > Endpoint Usage Quota</a> 참고

### 2017.03.23
#### 기능 개선/변경
* [Console] Domain 복제 기능 추가
	* 상세한 내용은 <a href="/ja/Upcoming%20Products/API%20Gateway/ja/Getting%20Started/#domain_1" target="_blank">Developer`s Guide > Domain clone</a> 참고

* [API] Target Server API Connection 오류 발생시 상세 응답코드 반환하도록 변경

### 2017.02.23
#### 기능 개선/변경
* [Console] Maintenance 플러그인 기능 추가
	* 상세한 내용은 <a href="/ja/Upcoming%20Products/API%20Gateway/ja/Developer%60s%20Guide/#maintenance" target="_blank">Developer`s Guide > Maintenance Plugin</a> 참고

#### 버그 수정
* [Console] 특정 Domain Deploy가 실패하는 오류 수정  
	* Domain 삭제시 일부 데이터가 남아 동일한 Domain 등록할 경우 Deploy가 실패하는 문제 수정

### 2016.10.06
#### 기능 개선/변경
* [Console] Pre API 플러그인 기능 추가
* [Console] Header 변경 플러그인 기능 추가
* [API] 파일 업로드 지원

#### 버그수정
* [API] 타겟서버의 401 에러코드등 일부 응답을 처리하지 못하는 문제 수정


### 2016.08.30
#### 버그 수정
* [API] HMAC 인증 오류 수정
* [API] USAGE QUATA 적용시 동작하지 않던 문제 수정


### 2016.08.18
#### 기능 개선/변경
* [Console] Domain 하위  IP ACL에 subnet 형식 추가 가능
* [Console] Domain 하위 Usage Quota/Rate Limit 플러그인 삭제
* [Console] Domain 하위 Usage Quota 조건을 다수 등록 가능
* [Console] Endpoint 하위 URL Rewrite 플러그인 추가
* [Console] Endpoint 등록시  HEAD/PATCH 타입의 메소드 추가 가능

#### 버그 수정
* [Console] 플러그인 설정값이 특정조건에서 보이지 않는 문제 수정
* [Console] 도메인 신규 등록시 추가한 플러그인이 누락되는 문제 수정
