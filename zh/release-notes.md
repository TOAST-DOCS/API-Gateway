## Application Service > API Gateway > Release Notes

### 2019.02.26

#### 기능 개선/변경
* [Console] 모니터링 플러그인 서비스 중단 
  * 모니터링 플러그인 서비스가 중단됩니다. 서비스 중단 이후에는 콘솔 화면에서 모니터링 플러그인 기능 설정이 불가합니다. 

### 2018.04.24

#### 기능 개선/변경 
* 사설 인증서가 설치된 타겟서버로 프록시가 가능하도록 개선하였습니다. 

### 2018.02.22

#### 기능 개선/변경
* [Console] 통계 고도화 
  * 사용자가 선택한 기간에 따라 통계 데이터를 조회 할 수 있습니다. (최대 검새 긱간은 30일까지 가능합니다.)
  * 통계 검색기간에 따라 통계 단위가 세분화 되었습니다.  
    * 검색 기간이 6시간 미만인 경우 10분 단위 (10분 단위의 통계는 최대 30일간 제공됩니다.)
    * 검색 기간이 1일 미만인 경우 1시간 단위
    * 검색 기간이 1일 초과인 경우 1일 단위
  * 통계 데이터 종류가 추가 되었습니다. 
    * Response HTTP Status code의 그룹별 건 수를 확인할 수 있습니다.
    * API Gateway Plugin에서 Response가 반환된 건 수를 확인할 수 있습니다.
  * 2018.02.22 이전 통계 데이터는 고도화 이전의 통계 조회 페이지에서 확인할 수 있습니다. 

* [Console] 모니터링 플러그인 
  * 모니터링 플러그인을 통해 사용자 타겟 서버의 장애를 감지할 수 있습니다. 
    * 사용자 타겟 서버 또는 API Gateway로 부터 Response HTTP Status Code가 400 이상의 코드가 클라이언트에 응답될 경우, 사용자가 등록한 이메일 또는 단말기번호로 알림을 발송합니다. 
* [API] HTTP Delete 요청에 대해 Request Body를 포함하여 Proxy 할 수 있도록 변경되었습니다. 


### 2017.10.26

#### 버그 수정
- UriRewrite Plugin 버그 수정 
  - [API] 유효한 Rewrite Pattern이 잘못된 패턴으로 인식하는 오류를 수정하였습니다. 

### 2017.06.22

#### 기능 개선/변경
- [Console] CORS 플러그인 추가
  - Cross-site간 HTTP Request가 가능하도록 설정할 수 있는 CORS 플러그인을 추가하였습니다.
  - 상세한 내용은 <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#corscross-origin-resource-sharing" target="_blank">Developer`s Guide > Plugin > CORS</a> 참고

### 2017.05.25

#### 기능 개선/변경
- [Console] domain key 입력시 path 형태 입력 불가하도록 변경
  - path 형태의 domain key는 지원하지 않고 있으므로 path 형태의 domain key를 입력하지 못하도록 변경하였습니다.  
- [Console] Swagger import & export 지원
  - domain 설정 정보를 swagger 파일로 import & export 할 수 있습니다.  
  - 상세한 내용은 <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#swagger-import-export" target="_blank">Developer`s Guide > Swagger import & Export</a> 참고

#### 버그 수정
- [Console] endpoint 삭제 후 Deploy 버튼이 활성화되지 않는 버그 수정
  - endpoint가 삭제된 경우 설정 정보가 변경되었으므로 Deploy 버튼이 활성화되어야 하나 비활성화 상태로 남아있는 버그를 수정하였습니다.

### 2017.04.20

#### 기능 개선/변경
- [Console] 오류 발생시 상세 오류 메시지를 alert로 표시
- [Console] Deploy 수행시 순단이 발생되지 않도록 수정
- [Console] Endpoint Plugin > Usage Quota 플러그인 추가
  - 상세한 내용은 <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#usage-quota" target="_blank">Developer`s Guide > Endpoint Usage Quota</a> 참고

### 2017.03.23

#### 기능 개선/변경
- [Console] Domain 복제 기능 추가
  - 상세한 내용은 <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#_5" target="_blank">Developer`s Guide > Domain clone</a> 참고
- [API] Target Server API Connection 오류 발생시 상세 응답코드 반환하도록 변경

### 2017.02.23

#### 기능 개선/변경
- [Console] Maintenance 플러그인 기능 추가
  - 상세한 내용은 <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#maintenance" target="_blank">Developer`s Guide > Maintenance Plugin</a> 참고

#### 버그 수정
- [Console] 특정 Domain Deploy가 실패하는 오류 수정  
  - Domain 삭제시 일부 데이터가 남아 동일한 Domain 등록할 경우 Deploy가 실패하는 문제 수정

### 2016.10.06

#### 기능 개선/변경
- [Console] Pre API 플러그인 기능 추가
- [Console] Header 변경 플러그인 기능 추가
- [API] 파일 업로드 지원

#### 버그수정
- [API] 타겟서버의 401 에러코드등 일부 응답을 처리하지 못하는 문제 수정

### 2016.08.30

#### 버그 수정
- [API] HMAC 인증 오류 수정
- [API] USAGE QUATA 적용시 동작하지 않던 문제 수정

### 2016.08.18

#### 기능 개선/변경
- [Console] Domain 하위  IP ACL에 subnet 형식 추가 가능
- [Console] Domain 하위 Usage Quota/Rate Limit 플러그인 삭제
- [Console] Domain 하위 Usage Quota 조건을 다수 등록 가능
- [Console] Endpoint 하위 URL Rewrite 플러그인 추가
- [Console] Endpoint 등록시  HEAD/PATCH 타입의 메소드 추가 가능

#### 버그 수정
- [Console] 플러그인 설정값이 특정조건에서 보이지 않는 문제 수정
- [Console] 도메인 신규 등록시 추가한 플러그인이 누락되는 문제 수정