## Application Service > API Gateway > 릴리스 노트

### 2024. 10. 29.
* 한국(평촌) 리전 서비스 종료

### 2024. 08. 27.
#### 기능 개선/변경 
* 게이트웨이 응답 기능 추가
    * 게이트웨이에서 정의된 오류 응답 설정을 사용자가 재정의할 수 있습니다.
    * 자세한 내용은 [콘솔 가이드 > 게이트웨이 응답](./console-guide-gov/#_42)을 참고하세요.
* 서비스 게이트웨이 연동(한국(판교) 리전)
    * 서비스 게이트웨이를 통해 NHN Cloud 내부 네트워크 내 클라이언트가 인터넷을 경유하지 않고 API Gateway와 통신할 수 있습니다.
* 게이트웨이 <-> 백엔드 엔드포인트 구간에서 백엔드 엔드포인트가 TLS 1.2 미만만 지원하는 경우, 통신이 더 이상 지원되지 않습니다.


### 2024. 07. 23.
#### 기능 개선/변경 
* 요청 유효성 검사기 플러그인 추가 
    * 요청 유효성 검사기는 리소스의 요청 파라미터에 정의된 설정에 따라 클라이언트의 요청을 검증하는 기능입니다. 자세한 내용은 [콘솔 가이드 > 요청 유효성 검사기](./console-guide-gov/#_29)를 참고하세요.
* 컨텍스트 변수 이름에 하이픈(-)이 포함되었을 때 API 호출이 실패하는 현상을 개선하였습니다.
* 요청 헤더 삭제, 응답 헤더 삭제 기능 추가


### 2024. 04. 23.
#### 기능 개선/변경 

* 컨텍스트 변수 확장
    * 요청과 응답과 관련된 다양한 컨텍스트 변수가 추가되었습니다. 추가된 컨텍스트 변수는 리소스와 스테이지 설정에서 활용 가능합니다.
    * 자세한 내용은 [콘솔 가이드 > 컨텍스트 변수](./console-guide-gov/#_11)를 참고하세요.


### 2023. 09. 05.
#### 기능 개선/변경 
* 한국(평촌) 리전 오픈


### 2023. 08. 29.
#### 기능 개선/변경 
* 요청 제한 정책 기능 추가 
    * 요청 제한 정책은 요청의 경로 변수 또는 요청 헤더의 값별로 IP ACL과 요청 수 제한을 설정할 수 있는 기능입니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 요청 제한 정책](./console-guide-gov/#_34)을 참고하세요.
* 사용자 지정 도메인 기능 추가
    * 스테이지 도메인의 Prefix를 사용자가 지정한 값으로 설정하여 도메인을 지정할 수 있는 기능입니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 사용자 지정 도메인](./console-guide-gov/#_57)을 참고하세요.
    * API 응답에 사용자 지정 도메인 관련 필드명이 stageAliasDomainList에서 stageCustomDomainList로 변경되었습니다.
* API Key 가져오기/내보내기 기능 추가 
    * CSV 파일을 통해 API Key를 가져오거나 등록된 API Key를 내보낼 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > API Key 가져오기](./console-guide-gov/#api-key_8)와 [콘솔 사용 가이드 > API Key 내보내기](./console-guide-gov/#api-key_7)를 참고하세요.
* 사용자 지정 Primary/Secondary API Key로 API Key 생성 
    * 사용자가 지정한 Primary/Sencodary API Key로 API Key를 생성할 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > API Key 생성](./console-guide-gov/#api-key_6)을 참고하세요.
* Top 10 서비스 조회 통계 API 추가 
    * 전체 API 호출 수, 실패 API 호출 수, 평균 응답 시간을 기준으로 상위 10개의 API Gateway 서비스 목록과 누적 통계를 조회할 수 있습니다.
    * 자세한 내용은 [API v1.0 가이드 > Top 10 서비스 조회](./api-guide-v1.0-gov/#top-10)를 참고하세요.


### 2022. 08. 02.
#### 기능 개선/변경 
* 백엔드 엔드포인트에 사용 가능한 포트 범위가 변경되었습니다.
    * 기존: 80, 443, 5000~12000
    * 변경: 80, 443, 10000~12000


### 2022. 04. 05.
#### 신규 서비스 출시
* API Gateway 서비스는 손쉽게 API를 통합하여 관리할 수 있는 서비스입니다.
* 서비스의 코드 수정과 배포 없이 부가 기능을 추가할 수 있습니다.
* 대시보드에서 API 통계 지표를 확인할 수 있어 모니터링 및 API 품질 지표로 활용할 수 있습니다.
