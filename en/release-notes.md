## Application Service > API Gateway > Release Notes

### Jul.23,2019

#### Feature Updates/Changes 
* API Call Volume Restricted for Each Project  
  * API calls are allowed no more than 10,000 times per second at each project. When it exceeds the restricted volume, request shall be denied, with 429 Too Many Request returned as response. 
  * If you need adjustment in the usage volume, contact Customer Center. 


### Feb.26,2019 

#### Updates/Changes 
* [Console] Suspension of Monitoring Plugin  
  * The monitoring plugin service is suspended. After service suspension, setting for monitoring plugin  gets unavailable on console.  


### April 24, 2018 

#### Updates/Changes 
* 사설 인증서가 설치된 타겟서버로 프록시가 가능하도록 개선하였습니다. Updated to allow proxy to the target server where private certificate is installed.   

### Feb. 22, 2018

#### Updates/Changes 
* [Console] 통계 고도화 Upgrade in Statistics 
  * Statistical data can be queried depending on user-configured period. (search is available up to 30 days)  사용자가 선택한 기간에 따라 통계 데이터를 조회 할 수 있습니다. (최대 검새 긱간은 30일까지 가능합니다.)
  * Statistical unit has been fragmented.  통계 검색기간에 따라 통계 단위가 세분화 되었습니다.  
    * Every 10 minutes, when search period is under 6 hours (10-minute statistics are provided for up to 30 days) 검색 기간이 6시간 미만인 경우 10분 단위 (10분 단위의 통계는 최대 30일간 제공됩니다.)
    * Every hour, when search period is below 1 day 검색 기간이 1일 미만인 경우 1시간 단위
    * Every day, when search period is over 1 day 검색 기간이 1일 초과인 경우 1일 단위
  * More types of statistical data have been added. 통계 데이터 종류가 추가 되었습니다. 
    * Find cases of response HTTP status code of each group 의 그룹별 건 수를 확인할 수 있습니다.
    * Find returned cases of response from API Gateway Plugin에서 Response가 반환된 건 수를 확인할 수 있습니다.
  * Data prior to Feb 22, 2018 can be found on the query statistics page before upgraded. 02.22 이전 통계 데이터는 고도화 이전의 통계 조회 페이지에서 확인할 수 있습니다. 

* [Console] Monitoring Plugin 모니터링 플러그인 
  * Check error in the user-targeting server through monitoring plugin. 모니터링 플러그인을 통해 사용자 타겟 서버의 장애를 감지할 수 있습니다. 
    * When 사용자 타겟 서버 또는 API Gateway로 부터 Response HTTP Status Code가 400 이상의 코드가 클라이언트에 응답될 경우, 사용자가 등록한 이메일 또는 단말기번호로 알림을 발송합니다. 
* [API] HTTP Delete 요청에 대해 Request Body를 포함하여 Proxy 할 수 있도록 변경되었습니다. 


### Oct.26, 2017

#### Bug Fixes
- UriRewrite Plugin 버그 수정 
  - [API] Fixed the error in which valid rewrite pattern is recognized as invalid  유효한 Rewrite Pattern이 잘못된 패턴으로 인식하는 오류를 수정하였습니다. 

### June 22, 2017

#### Updates/Changes
- [Console] Adding CORS Plugin  플러그인 추가
  - Added the CORS plugin which enables cross-site HTTP requests. site간 HTTP Request가 가능하도록 설정할 수 있는 CORS 플러그인을 추가하였습니다.
  - See <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#corscross-origin-resource-sharing" target="_blank">Developer`s Guide > Plugin > CORS</a> for more details. 

### May 25, 2017 

#### Updates/Changes 
- [Console] Changed to disallow the entry of domain key in the path format  입력시 path 형태 입력 불가하도록 변경
  - Since path-type domain key is not supported, it has been changed to disallow path-format domain key.   
- [Console] Support of Swagger Import & Export 지원
  - The domain setting information can be imported and exported in the swagger file. domain 설정 정보를 swagger 파일로 import & export 할 수 있습니다.  
  - For more details, see <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#swagger-import-export" target="_blank">Developer`s Guide > Swagger import & Export</a>.

#### Bug Fixes 
- [Console] Fixed the bug in which Deploy is not enabled after endpoint is deleted. endpoint 삭제 후 Deploy 버튼이 활성화되지 않는 버그 수정
  - When an endpoint is deleted, setting information is changed, so deploy must be enable. 가 삭제된 경우 설정 정보가 변경되었으므로 Deploy 버튼이 활성화되어야 하나 비활성화 상태로 남아있는 버그를 수정하였습니다.

### April 20, 2017 

#### Updates/Changes
- [Console] 오류 발생시 상세 오류 메시지를 alert로 표시
- [Console] Deploy 수행시 순단이 발생되지 않도록 수정
- [Console] Endpoint Plugin > Usage Quota 플러그인 추가
  - See <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#usage-quota" target="_blank">Developer`s Guide > Endpoint Usage Quota</a> for details

### March 23, 2017 

#### Updates/Changes
- [Console] Added Replicate Domain 복제 기능 추가
  - See <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#_5" target="_blank">Developer`s Guide > Domain clone</a> for details
- [API] Target Server API Connection 오류 발생시 상세 응답코드 반환하도록 변경

### Feb.23, 2017 

#### Updates/Changes
- [Console] Added Maintenance Plugin
  - See <a href="/ko/Application%20Service/API%20Gateway/ko/console-guide/#maintenance" target="_blank">Developer`s Guide > Maintenance Plugin</a> for more details  

#### Bug Fixes 
- [Console] Fixed error in which deployment fails in particular domains
  - Fixed the issue of failed deployment, if same domain is registered after domain is deleted, which remains some data.  

### Oct. 6, 2016

#### Updates/Changes
- [Console] Added Pre-call API plugin  
- [Console] Added the header change plugin 
- [API] Support file uploading 

#### Bug Fixes
- [API] Fixed the failure in processing some responses, including 401 error code at a target server 

### August 30, 2016 

#### Bug Fixes
- [API] Fixed authentication error in HMAC  
- [API] Fixed failed operations when usage quota was applied   

### August 18, 2016 

#### Updates/Changes
- [Console] Subnets can be added to IP ACL at  subdomains
- [Console] Deleted Usage Quota/Rate Limit plugin at subdomains 
- [Console]  Available to register multiple conditions for Usage Quota at subdomains 
- [Console] Added URL Rewrite plugin at a subdomain of endpoint 
- [Console] Available to add methods in the HEAD/PATCH type to register endpoints  

#### Bug Fixes
- [Console] Fixed an issue in which plugin setting value is not visible under particular conditions
- [Console] Fixed the missing of plugin which is added for a new domain registration 

