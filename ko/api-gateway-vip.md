## Application Service > API Gateway > API Gateway 클라이언트 방화벽 정책 설정 

### API Gateway 클라이언트 방화벽 정책 설정 

클라이언트가 API Gateway를 통해 API를 호출할 때 방화벽(Network ACL)을 사용한다면, API Gateway의 VIP에 대해 방화벽 정책을 설정해야 합니다.
그렇지 않을 경우, 도메인 질의 결과에 따라 API 호출이 실패할 수 있습니다.
클라이언트가 방화벽을 별도로 관리하지 않는다면 추가적인 설정 없이 API를 사용할 수 있습니다.

#### API Gateway VIP 정보

| VIP | 포트 |
| --- | --- |
| 180.210.64.24<br>180.210.65.24<br>180.210.64.224<br>180.210.65.224<br>117.52.123.41 | 80, 443 |

API Gateway VIP 정보를 참고하여 다음의 방화벽(Network ACL)을 설정하세요.

* 출발지: API Gateway를 통해 제공되는 API를 호출하는 클라이언트 IP
* 도착지: API Gateway VIP 목록 전체 
* 포트: 80, 443
* 통신 정책: 허용(Allow) 

> **[참고]** API Gateway VIP 변경
> * API Gateway VIP 목록은 사전 공지 후 변경될 수 있습니다. 
> * 변경 시 공지 내용을 확인한 뒤 변경된 VIP에 대한 방화벽 정책을 설정해야 합니다.