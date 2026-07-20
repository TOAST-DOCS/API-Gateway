<!-- pre-align:aligned sig=4c627ec8f307 -->

<a id="application-service-api-gateway-enum-code"></a>
## Application Service > API Gateway > Enum Code { #application-service-api-gateway-enum-code }

<a id="enum-code"></a>
## Enum Code { #enum-code }
This document describes Enum codes referenced in the API v1.0 guide.

<a id="api-gateway-region"></a>
### API Gateway Region { #api-gateway-region }
- Indicates the region where the API Gateway server is located.

| Name | Description |
| --- | --- |
| KR1 | Korea (Pangyo) Region |
| KR2 | Korea (Pyeongchon) Region |


<a id="api-gateway-service-type"></a>
### API Gateway Service Type { #api-gateway-service-type }
- The service type of API Gateway according to the Shared or Dedicated type. 
- Currently, only Shared API Gateway service type is supported. 

| Name | Description |
| --- | --- |
| SHARED | Shared API Gateway service type |


<a id="http-method-type"></a>
### HTTP Method Type { #http-method-type }
- Supported HTTP method types.

| Name | Description |
| --- | --- |
| GET | HTTP GET method |
| POST | HTTP POST method | 
| DELETE | HTTP DELETE method | 
| PUT | HTTP PUT method | 
| OPTIONS | HTTP OPTIONS method | 
| HEAD | HTTP HEAD method | 
| PATCH | HTTP PATCH method | 


<a id="resource-plugin-type"></a>
### Resource Plugin Type { #resource-plugin-type }
- A plugin type that can be set for resources.

| Name | Description | Where the plugin can be applied |
| --- | --- | --- |
| HTTP | Forwards a API request received by API Gateway to the defined backend endpoint URL path. | Method |
| MOCK | Returns a defined response to a request received by API Gateway. | Method |
| CORS | Allows XMLHttpRequest API calls within a cross-site method. | Resource path |
| SET_REQUEST_HEADER | Adds or changes the request header. | Resource path, method |
| REMOVE_REQUEST_HEADER | Deletes the request header. | Resource path, method |
| SET_RESPONSE_HEADER | Adds the header to a backend response or changes the header. | Resource path, method |
| REMOVE_RESPONSE_HEADER | Deletes the header from a backend response. | Resource path, method |
| ADD_REQUEST_QUERY_PARAMETER | Adds a query string parameter to the backend endpoint request. | Resource path, method |


<a id="resource-requestresponse-parameter-data-type"></a>
### Resource Request/Response Parameter Data Type { #resource-requestresponse-parameter-data-type }
- A data type that can be set in resource request/response parameters.

| Name | Description |
| --- | --- |
| STRING | String data type |
| BOOLEAN | Boolean data type | 
| INTEGER | Integer data type | 
| LONG | Long data type | 
| FLOAT | Float data type | 
| DOUBLE | Double data type | 
| FILE | File data type. It can be set only in Request Parameters > Form Data. | 


<a id="stage-resource-plugin-type"></a>
### Stage Resource > Plugin Type { #stage-resource-plugin-type }
- A plugin type that can be configured on the stage resource path or method. 

| Name | Description | Where the plugin can be applied |
| --- | --- | --- |
| IP_ACL | IP access control plugin | Root (/) resource path |
| HMAC | HMAC request validation plugin | Root (/) resource path |
| JWT | JWT token validation plugin | Root (/) resource path |
| API_KEY | API Key validation plugin | Resource path, method |
| REQUEST_VALIDATOR | Request validator plugin | Resource path, method |
| PRE_API | Pre-call API plugin | Resource path, method |
| RATE_LIMIT | Request number limit plugin | Method |


<a id="jwt-encryption-algorithm"></a>
### JWT > Encryption Algorithm { #jwt-encryption-algorithm }
- The encryption algorithm used to sign the JWT token.

| Name | Description |
| --- | --- |
| HS256 | A symmetric key algorithm, which uses the HS256 (HMAC with SHA-256) algorithm to sign tokens.  |
| RS256 | An asymmetric key algorithm, which uses public/private keys to sign tokens using the RSA256 (RSA Signature with SHA-256) algorithm. | 


<a id="jwt-claim-data-type"></a>
### JWT > Claim Data Type { #jwt-claim-data-type }
- The data type of the JWT claim.

| Name | Description |
| --- | --- |
| Array | A data type of array format.  |
| String | A data type of string format. | 
| NumericDate | A data type representing the number of seconds from 1970-01-01T00:00:00Z UTC to the specified UTC date/time, ignoring milliseconds. |


<a id="jwt-rs256-encryption-algorithm-public-key-type"></a>
### JWT > RS256 Encryption Algorithm > Public Key Type { #jwt-rs256-encryption-algorithm-public-key-type }
- RS256 uses a public/private key based encryption algorithm. Set the public key setting method.

| Name | Description |
| --- | --- |
| RSA_PUBLIC_KEY | This method sets the public key in PEM format. |
| JWKS_URI | This method sets the JSON Web Key Set URI where public key can be queried.|


<a id="request-number-limit-limit-key"></a>
### Request Number Limit > Limit Key { #request-number-limit-limit-key }
- The key to which the request number limit applies.

| Name | Description |
| --- | --- |
| DEFAULT | Applies a limit on the number of requests for a resource method. |
| IP | Applies a limit on the number of requests for a resource method per client IP. |
| HEADER | Applies a limit on the number of requests for a resource method per value of the specified header name. |
| PATH_VARIABLE | Applies a limit on the number of requests for a resource method per path variable. |


<a id="stage-deployment-deployment-status"></a>
### Stage Deployment > Deployment Status { #stage-deployment-deployment-status }
- The status of the stage deployment job.

| Name | Description |
| --- | --- |
| DEPLOYING | Deployment in progress | 
| COMPLETE | Deployment complete (successful) | 
| FAILURE | Deployment failed | 


<a id="usage-plan-quota-period-unit"></a>
### Usage Plan > Quota Period Unit { #usage-plan-quota-period-unit }
- The unit of period for which the quota is initialized.

| Name | Description |
| --- | --- |
| DAY | Limit call volume per day. Reset daily at 00:00:00 UTC.| 
| MONTH | Limit call volume on a monthly basis. Reset at 00:00:00 UTC on the 1st of every month. | 


<a id="api-key-status"></a>
### API Key Status { #api-key-status }
- The status of the API Key.
- A deactivated API key fails to authenticate the API key, making API calls impossible. 

| Name | Description |
| --- | --- |
| ACTIVE | Active status | 
| INACTIVE | Inactive status |


<a id="api-key-type"></a>
### API Key Type { #api-key-type }
- The types of Primary API Key and Secondary API Key of the issued API Key. 

| Name | Description |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |


<a id="api-key-subscription-status"></a>
### API Key Subscription Status { #api-key-subscription-status }
- The subscription status of the API Key.

| Name | Description |
| --- | --- |
| APPROVAL | Approved status | 

<a id="statistics-data-time-unit"></a>
### Statistics Data Time Unit { #statistics-data-time-unit }
- The unit of time for which statistics data is collected

| Name | Description |
| --- | --- |
| ONE_MINUTES | Collects statistics data at 1 minute intervals  | 
| TEN_MINUTES | Collects statistics data at 10 minute intervals | 
| ONE_HOURS | Collects statistics data at 1 hour intervals | 
| ONE_DAYS | Collects statistics data at daily intervals | 


<a id="statistics-sort-top-10-services-by"></a>
### Statistics > Sort Top 10 Services By { #statistics-sort-top-10-services-by }
| Name | Description |
| --- | --- |
| CALL_COUNT | Sort by total API calls in descending order | 
| FAIL_CALL_COUNT | Sort by number of failed API calls in descending order | 
| AVG_RESPONSE_TIME | Sort by average response time in descending order | 


<a id="gateway-response-type"></a>
### Gateway response type { #gateway-response-type }
| Gateway response type | Default status codes | Description |
| ----------- | -------- | --- |
| UpstreamServiceUnavailable | 503 | Response that occurs when the backend endpoint service is unresponsive or experiencing a persistent response delay (60 seconds or more). |
| GatewayTimeout | 504 | Response that occurs when the gateway's maximum response time (60 seconds) is exceeded. |
| Unauthorized | 401 | Response that occurs when the requested information required for authentication is missing or if authentication fails. |
| JwksError | 500 | Response that occurs if the JWT's JWKS is set incorrectly. |
| PreApiFailed | 502 | Response that occurs when the pre-call API does not respond to a request from API Gateway. If the response status code of the pre-call API is not 200, the response from the pre-call API is passed to the client as it is. |
| Forbidden | 403 | Response that occurs when you deny a request that you are not authorized to access. |
| RateLimited | 429 | Response that occurs when rejecting a request that exceeds a limited number of requests. |
| UsageQuotaExceeded | 429 | Response that occurs when denying a request that exceeds a limited request quota. |
| InvalidUri | 400 | Response occurs when the URI configuration on the backend endpoint is incorrect. |
| NotFound | 404 | Response that occurs when making a request with an unregistered path and method. |
| BadGateway | 502 | Response that occurs when the backend endpoint is unresponsive or refuses to respond. |
| InvalidContextVariable | 500 | Response that occurs due to an incorrect context variable setting |
| BadRequest | 400 | Response that occurs due to an invalid client request. |
| InternalServerError | 500 | Response that occurs when an unexpected error occurred. |