<a id="application-service-api-gateway-release-note"></a>
## Application Service > API Gateway > 릴리스 노트 { #application-service-api-gateway-release-note }

<a id="july-28-2026"></a>
### 2026. 07. 28. { #july-28-2026 }
<a id="july-28-2026-added-features"></a>
#### 기능 추가 { #july-28-2026-added-features }
*  API v2.0 추가
    * User Access Key 토큰을 지원합니다.

<a id="november-11-2025"></a>
### 2025. 11. 11. { #november-11-2025 }
<a id="november-11-2025-feature-updates"></a>
#### 기능 개선/변경 { #november-11-2025-feature-updates }
* 사용자 콘솔 UI/UX 개선
   * 사용 편의성 향상을 위해 사용자 인터페이스를 개선했습니다.

<a id="october-29-2024"></a>
### 2024. 10. 29. { #october-29-2024 }
<a id="october-29-2024-feature-updates"></a>
#### 기능 개선/변경 { #october-29-2024-feature-updates }
* 한국(평촌) 리전 서비스 종료

<a id="august-27-2024"></a>
### 2024. 08. 27. { #august-27-2024 }
<a id="august-27-2024-feature-updates"></a>
#### 기능 개선/변경 { #august-27-2024-feature-updates }
* 게이트웨이 응답 기능 추가
    * 게이트웨이에서 정의된 오류 응답 설정을 사용자가 재정의할 수 있습니다.
    * 자세한 내용은 [콘솔 가이드 > 게이트웨이 응답](./console-guide-gov/#gateway-response)을 참고하세요.
* 서비스 게이트웨이 연동(한국(판교) 리전)
    * 서비스 게이트웨이를 통해 NHN Cloud 내부 네트워크 내 클라이언트가 인터넷을 경유하지 않고 API Gateway와 통신할 수 있습니다.
* 게이트웨이 <-> 백엔드 엔드포인트 구간에서 백엔드 엔드포인트가 TLS 1.2 미만만 지원하는 경우, 통신이 더 이상 지원되지 않습니다.


<a id="july-23-2024"></a>
### 2024. 07. 23. { #july-23-2024 }
<a id="july-23-2024-feature-updates"></a>
#### 기능 개선/변경 { #july-23-2024-feature-updates }
* 요청 유효성 검사기 플러그인 추가 
    * 요청 유효성 검사기는 리소스의 요청 파라미터에 정의된 설정에 따라 클라이언트의 요청을 검증하는 기능입니다. 자세한 내용은 [콘솔 가이드 > 요청 유효성 검사기](./console-guide-gov/#validate-requests)를 참고하세요.
* 컨텍스트 변수 이름에 하이픈(-)이 포함되었을 때 API 호출이 실패하는 현상을 개선하였습니다.
* 요청 헤더 삭제, 응답 헤더 삭제 기능 추가


<a id="april-23-2024"></a>
### 2024. 04. 23. { #april-23-2024 }
<a id="april-23-2024-feature-updates"></a>
#### 기능 개선/변경 { #april-23-2024-feature-updates }

* 컨텍스트 변수 확장
    * 요청과 응답과 관련된 다양한 컨텍스트 변수가 추가되었습니다. 추가된 컨텍스트 변수는 리소스와 스테이지 설정에서 활용 가능합니다.
    * 자세한 내용은 [콘솔 가이드 > 컨텍스트 변수](./console-guide-gov/#context-variables)를 참고하세요.


<a id="september-5-2023"></a>
### 2023. 09. 05. { #september-5-2023 }
<a id="september-5-2023-feature-updates"></a>
#### 기능 개선/변경 { #september-5-2023-feature-updates }
* 한국(평촌) 리전 오픈


<a id="august-29-2023"></a>
### 2023. 08. 29. { #august-29-2023 }
<a id="august-29-2023-feature-updates"></a>
#### 기능 개선/변경 { #august-29-2023-feature-updates }
* 요청 제한 정책 기능 추가 
    * 요청 제한 정책은 요청의 경로 변수 또는 요청 헤더의 값별로 IP ACL과 요청 수 제한을 설정할 수 있는 기능입니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 요청 제한 정책](./console-guide-gov/#request-restriction-policy)을 참고하세요.
* 사용자 지정 도메인 기능 추가
    * 스테이지 도메인의 Prefix를 사용자가 지정한 값으로 설정하여 도메인을 지정할 수 있는 기능입니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 사용자 지정 도메인](./console-guide-gov/#custom-domain)을 참고하세요.
    * API 응답에 사용자 지정 도메인 관련 필드명이 stageAliasDomainList에서 stageCustomDomainList로 변경되었습니다.
* API Key 가져오기/내보내기 기능 추가 
    * CSV 파일을 통해 API Key를 가져오거나 등록된 API Key를 내보낼 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > API Key 가져오기](./console-guide-gov/#import-api-key)와 [콘솔 사용 가이드 > API Key 내보내기](./console-guide-gov/#export-api-key)를 참고하세요.
* 사용자 지정 Primary/Secondary API Key로 API Key 생성 
    * 사용자가 지정한 Primary/Sencodary API Key로 API Key를 생성할 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > API Key 생성](./console-guide-gov/#create-api-key)을 참고하세요.
* Top 10 서비스 조회 통계 API 추가 
    * 전체 API 호출 수, 실패 API 호출 수, 평균 응답 시간을 기준으로 상위 10개의 API Gateway 서비스 목록과 누적 통계를 조회할 수 있습니다.
    * 자세한 내용은 [API v1.0 가이드 > Top 10 서비스 조회](./api-guide-v1.0-gov/#query-top-10-services)를 참고하세요.


<a id="august-2-2022"></a>
### 2022. 08. 02. { #august-2-2022 }
<a id="august-2-2022-feature-updates"></a>
#### 기능 개선/변경 { #august-2-2022-feature-updates }
* 백엔드 엔드포인트에 사용 가능한 포트 범위가 변경되었습니다.
    * 기존: 80, 443, 5000~12000
    * 변경: 80, 443, 10000~12000


<a id="april-5-2022"></a>
### 2022. 04. 05. { #april-5-2022 }
<a id="april-5-2022-new-service-release"></a>
#### 신규 서비스 출시 { #april-5-2022-new-service-release }
* API Gateway 서비스는 손쉽게 API를 통합하여 관리할 수 있는 서비스입니다.
* 서비스의 코드 수정과 배포 없이 부가 기능을 추가할 수 있습니다.
* 대시보드에서 API 통계 지표를 확인할 수 있어 모니터링 및 API 품질 지표로 활용할 수 있습니다.
