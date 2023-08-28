## Application Service > API Gateway > Enum Code

## Enum Code
This document describes Enum codes referenced in the API v1.0 guide.

### API Gateway Region
- Indicates the region where the API Gateway server is located.

| Name | Description |
| --- | --- |
| KR1 | Korea (Pangyo) Region |
| KR2 | Korea (Pyeongchon) Region |


### API Gateway Service Type
- The service type of API Gateway according to the Shared or Dedicated type. 
- Currently, only Shared API Gateway service type is supported. 

| Name | Description |
| --- | --- |
| SHARED | Shared API Gateway service type |


### HTTP Method Type
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


### Resource Plugin Type
- A plugin type that can be set for resources.

| Name | Description | Where the plugin can be applied |
| --- | --- | --- |
| HTTP | Forwards a API request received by API Gateway to the defined backend endpoint URL path. | Method |
| MOCK | Returns a defined response to a request received by API Gateway. | Method |
| CORS | Allows XMLHttpRequest API calls within a cross-site method. | Resource path |
| SET_REQUEST_HEADER | Adds or changes the request header. | Resource path, method |
| SET_RESPONSE_HEADER | Adds the header to a backend response or changes the header. | Resource path, method |
| ADD_REQUEST_QUERY_PARAMETER | Adds a query string parameter to the backend endpoint request. | Resource path, method |


### Resource Request/Response Parameter Data Type
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


### Stage Resource > Plugin Type
- A plugin type that can be configured on the stage resource path or method. 

| Name | Description | Where the plugin can be applied |
| --- | --- | --- |
| IP_ACL | IP access control plugin | Root (/) resource path |
| HMAC | HMAC request validation plugin | Root (/) resource path |
| JWT | JWT token validation plugin | Root (/) resource path |
| API_KEY | API Key validation plugin | Resource path, method |
| PRE_API | Pre-call API plugin | Resource path, method |
| RATE_LIMIT | Request number limit plugin | Method |


### JWT > Encryption Algorithm 
- The encryption algorithm used to sign the JWT token.

| Name | Description |
| --- | --- |
| HS256 | A symmetric key algorithm, which uses the HS256 (HMAC with SHA-256) algorithm to sign tokens.  |
| RS256 | An asymmetric key algorithm, which uses public/private keys to sign tokens using the RSA256 (RSA Signature with SHA-256) algorithm. | 


### JWT > Claim Data Type 
- The data type of the JWT claim.

| Name | Description |
| --- | --- |
| Array | A data type of array format.  |
| String | A data type of string format. | 
| NumericDate | A data type representing the number of seconds from 1970-01-01T00:00:00Z UTC to the specified UTC date/time, ignoring milliseconds. |


### JWT > RS256 Encryption Algorithm > Public Key Type 
- RS256 uses a public/private key based encryption algorithm. Set the public key setting method.

| Name | Description |
| --- | --- |
| RSA_PUBLIC_KEY | This method sets the public key in PEM format. |
| JWKS_URI | This method sets the JSON Web Key Set URI where public key can be queried.|


### Request Number Limit > Limit Key
- The key to which the request number limit applies.

| Name | Description |
| --- | --- |
| DEFAULT | Applies a limit on the number of requests for a resource method. |
| IP | Applies a limit on the number of requests for a resource method per client IP. |
| HEADER | Applies a limit on the number of requests for a resource method per value of the specified header name. |
| PATH_VARIABLE | Applies a limit on the number of requests for a resource method per path variable. |


### Stage Deployment > Deployment Status
- The status of the stage deployment job.

| Name | Description |
| --- | --- |
| DEPLOYING | Deployment in progress | 
| COMPLETE | Deployment complete (successful) | 
| FAILURE | Deployment failed | 


### Usage Plan > Quota Period Unit
- The unit of period for which the quota is initialized.

| Name | Description |
| --- | --- |
| DAY | Limit call volume per day. Reset daily at 00:00:00 UTC.| 
| MONTH | Limit call volume on a monthly basis. Reset at 00:00:00 UTC on the 1st of every month. | 


### API Key Status
- The status of the API Key.
- A deactivated API key fails to authenticate the API key, making API calls impossible. 

| Name | Description |
| --- | --- |
| ACTIVE | Active status | 
| INACTIVE | Inactive status |


### API Key Type
- The types of Primary API Key and Secondary API Key of the issued API Key. 

| Name | Description |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |


### API Key Subscription Status
- The subscription status of the API Key.

| Name | Description |
| --- | --- |
| APPROVAL | Approved status | 

### Statistics Data Time Unit
- The unit of time for which statistics data is collected

| Name | Description |
| --- | --- |
| ONE_MINUTES | Collects statistics data at 1 minute intervals  | 
| TEN_MINUTES | Collects statistics data at 10 minute intervals | 
| ONE_HOURS | Collects statistics data at 1 hour intervals | 
| ONE_DAYS | Collects statistics data at daily intervals | 


### Statistics > Sort Top 10 Services By 
| Name | Description |
| --- | --- |
| CALL_COUNT | Sort by total API calls in descending order | 
| FAIL_CALL_COUNT | Sort by number of failed API calls in descending order | 
| AVG_RESPONSE_TIME | Sort by average response time in descending order | 