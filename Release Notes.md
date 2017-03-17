## Upcoming Products > API Gateway > Release Notes

### 2017.03.23
#### 기능 개선/변경
* [Console] Domain 복제 기능 추가
	* 상세한 내용은 <a href="/ko/Upcoming%20Products/API%20Gateway/Getting%20Started/#domain_1" target="_blank">Developer`s Guide > Domain clone</a> 참고 

* [API] Target Server API Connection 오류 발생시 상세 응답코드 반환하도록 변경

### 2017.02.23
#### 기능 개선/변경
* [Console] Maintenance 플러그인 기능 추가
	* 상세한 내용은 <a href="/ko/Upcoming%20Products/API%20Gateway/Developer%60s%20Guide/#maintenance" target="_blank">Developer`s Guide > Maintenance Plugin</a> 참고 

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
