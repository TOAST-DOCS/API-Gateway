## Application Service > API Gateway > Console User Guide

## Enable API Gateway  

To enable the API Gateway service, select a project to add services for, and go to **Select Services** and click **Application Service > API Gateway**.      

## Domains 

Below is the main page of API Gateway, which shows the list of registered domains.  

![apigw_01_201812](https://static.toastoven.net/prod_apigateway/apigw_01_201812.png)

### Create  

To set an endpoint server address to create domain address of API gateway and forward client's request, a domain must be created first.  

![apigw_02_201812](https://static.toastoven.net/prod_apigateway/apigw_02_201812.png)

1. Click **New Domain**.

2. Click **New Domain**.

3. Set domain. 
  - Domain Name: Alias of domain, which is used to tell each domain. 
  - Domain Key: Refers to domain's origin key. Key value is used for endpoint URL of API gateway. (api-gw.cloud.toast.com/{domainKey})
    - Path is not allowed for a domain key (e.g. /apis/gateway is unavailable).
  - URL for Endpoint Server: Enter URL of user API server for API gateway to deliver requests. 
  - Scheme: Select a scheme of domain URL provided by API Gateway.
> [Note] See [RFC3986](https://tools.ietf.org/html/rfc3986) for the URI part of endpoint server URL.   

4. Go to **Plugin Setting** to add a plugin. 
  - Plugins applied by domain are commonly applied to endpoints at the bottom of domains. 

5. Click **Save**.  

### Edit

You may edit the setting of a registered domain. 

![apigw_03_201812](https://static.toastoven.net/prod_apigateway/apigw_03_201812.png)

1. Click **Setting** of the domain you need to edit.  

2. Click **Domain** to go to edit.  

3. Change setting and click **Save**.

### Delete 

You may delete a registered domain. 

![apigw_04_201812](https://static.toastoven.net/prod_apigateway/apigw_04_201812.png)

1. Click **Delete**, and a pop-up for deleting domains shows. 

2. Confirm the domain you want to delete and enter domain key. 

3. Click **Delete**.

> [Caution] Domain key is required to delete a domain. Domains, once deleted, cannot be restored. 


### Clone 

By cloning the setting of domain already created, you may create a new domain.  

![apigw_05_201812](https://static.toastoven.net/prod_apigateway/apigw_05_201812.png)

1. Choose **Setting\> Clone from '___' domain** of a domain to clone. 

2. Modify information, if required, of a domain to be created by cloning. 

3. Click **Save**.


### Import and Export in Swagger 

Domains can be registered by importing swagger files, or registered domains may be exported to swagger files. 

#### Import in Swagger  

1. Write a swagger file in reference of the swagger specifications. 
  - [Swagger Specifications](http://swagger.io/docs/specification/what-is-swagger/)
2. To add plugin settings provided by TOAST Cloud API Gateway, add extension setting data for x-toastcloud-apigw. 
  - Example
```json
{
	"swagger": "2.0",
	"info": {
		"version": "2017-05-12T18:34:14.000+09:00",
		"title": "apigw example"
	},
	"host": "alpha-api-gw.cloud.toast.com",
	"basePath": "/example_apigw",
	"schemes": [
		"http"
	],
	"paths": {
		"/v1.0/apigw/**": {
			"get": {
				"parameters": [],
				"x-toastcloud-apigw": {
					"plugins": {
						"MOCK": {
							"statusCode": 200,
							"headers": {
								"x-cloudtoast-apigw": "mock_value"
							},
							"body": "mock response"
						},
						"ENDPOINT_USAGE_QUOTA": {
							"usageQuotaBeans": [
								{
									"maxUsageQuota": 1,
									"resetTimeSeconds": 10
								}
							]
						},
						"PRE_API": {
							"method": "GET",
							"url": "http://cloud.toast.com"
						},
						"HEADER": {
							"requestHeaders": {
								"x-cloudtoast-apigw-request": "add_request_header"
							},
							"responseHeaders": {
								"x-cloudtoast-apigw-response": "add_response_header"
							}
						}
					}
				}
			}
		}
	},
	"x-toastcloud-apigw": {
		"plugins": {
			"MAINTENANCE": {
				"isUse": true,
				"statusCode": 200,
				"headers": {
					"x-toastcloud-apigw": "value"
				},
				"body": "maintenance"
			},
			"IPACL": {
				"isPermit": true,
				"ipList": [
					{
						"ip": "192.168.0.1"
					}
				]
			},
			"HMAC": {
				"secretKey": "hmac_scret_key",
				"clockSkew": 100
			},
			"HTTP_PROXY": {
				"url": "http://cloud.toast.com"
			},
			"USAGE_QUOTA": {
				"usageQuotaBeans": [
					{
						"maxUsageQuota": 1,
						"resetTimeSeconds": 10
					}
				]
			},
			"URI_REWRITE": {
							"uriPattern": "/{version}/{path}",
							"rewriteUri": "/{path}/{version}"
			}
		}
	}
}
```

#### Export into Swagger 

![apigw_06_201812](https://static.toastoven.net/prod_apigateway/apigw_06_201812.png)

1. Click **Setting > Export into Swagger** of an exporting domain to download a swagger file. The default file name is export.json.
#### Default Domain Setting 

- Swagger: Enter version of a swagger: default is swagger 2.0.
- Info: Enter basic information. 
  - version: Enter version. 
  - title: Enter domain name. 
- Host: Enter domain of API Gateway.
- BasePath: Enter domain key. 
- Scheme: Enter scheme (either http or https).
- Path: Enter path of an endpoint. 

#### Domain Plugin Setting 

- For domain plugin, enter setting information for x-cloudtoast-apigw at the highest level. 
- HTTP_PROXY: Enter URL for endpoint server (*is required).
- IPACL: Enter Domain's Access Control > Setting information for the IP Access Control (IP ACL) plugin (only one out of many access control groups is available).
- HMAC: Enter Domain Authentication > Setting information for the HAMC plugin (only one out of many authentication groups is available).
- JWT: Enter Domain Authentication > Setting information for the JSON Web Token (JWT) plugin (only one out of many authentication groups is available).
- USAGE_QUOTA: Enter Domain's Quota Limit > Setting information for Usage Quota plugin (only one out of may quota limit groups is available).
- MAINTENANCE: Enter Domain's Maintenance > Setting information for Maintenance Response plugin (only one out of many maintenance groups is available).

#### Endpoint Plugin Setting 

- Enter setting information for x-cloudtoast-apigw at each level of path.  
- MOCK: Enter setting information for the Mock Response plugin.
- ENDPOINT_USAGE_QUOTA: Enter setting information for the Usage Quota plugin.
- PRE_API: Enter setting information for the Pre-call API plugin.
- HEADER: Enter setting information for the Modify Header plugin.
- URI_REWRITE: Enter setting information for the URL Rewrite plugin. 

![apigw_07_201812](https://static.toastoven.net/prod_apigateway/apigw_07_201812.png)

1. Click **Import Domain in Swagger**.

2. Attach the swagger file to import. 

3. Click **Import** and domain is registered like in the swagger file setting. 

## Endpoints

### Create 

Endpoints manage APIs to be provided via API Gateway, among user endpoint APIs. 

![apigw_08_201812](https://static.toastoven.net/prod_apigateway/apigw_08_201812.png)

1. Click **Setting** > **Endpoint** of a domain to create endpoints. 

2. Click **New Endpoint** and set HTTP method and path of an endpoint.  

3. To add a plugin, click **+**, select a plugin to add, and enter value.   

4. Click **Save**.

>  [Note] Path of Endpoints 
>  The endpoint path, if entered in the AntPattern format, may serve for many APIs.   
>
>  [Example of AntPattern]
>
>  - ?: serves for one character e.g) /docs/te?t : /docs/test , /docs/text 
>  - \*: serves for 0 or more than 1 character   e.g.) /docs/*.txt : /docs/example1.txt, /docs/example2.txt
>  - \*\*: serves for 0 or more than 1 path   e.g.) /docs/** : /docs/apigw/guide, /docs/image/guide
>  - {[a-z]+}: serves for path variables (path variable)에 대치   e.g.) /v1.0/appKeys/{appKey} : /v1.0/appKeys/myAppKey1, /v1.0/appKeys/myAppKey2 


> [Note] Endpoint Path Mapping 
> Request URI may match with patterns of many paths. 
> Connect API Gateway to the best matching Request URI path.  
>
> [Example]
> Suppose that following paths are registered in the endpoint path. 
>
>  - Path 1: /docs/apigw/guide
>  - Path 2: /docs/**
>    In case the Request URL is '/docs/apigw/guide', it matches with both path 1 and 2. 
>    Since path 1 has more matched patterns than path 2, it is connected to the path 1 URI.   
>    If a matched pattern regards to characters, it is higher on priority than the AntPattern expression.  

### Edit 

You may eidt the setting of a registered endpoint. 

![apigw_09_201812](https://static.toastoven.net/prod_apigateway/apigw_09_201812.png)

1. Click **Edit** on the right of an endpoint to edit from the list. 

2. Modify setting and click **Save** on the right. 

### Delete  

You may delete a registered endpoint. 

![apigw_10_201812](https://static.toastoven.net/prod_apigateway/apigw_10_201812.png)

1. Click **Delete** on the right of an endpoint to delete from the list. 

2. Click **OK**.

### Edit Endpoint Plugins 

You may edit the setting of an endpoint plugin. 

![apigw_11_201812](https://static.toastoven.net/prod_apigateway/apigw_11_201812.png)

1. Click a plugin to edit. 

2. Modify setting and click **Save**.


### Delete Endpoint Plugins

You may delete a registered endpoint plugin.  

![apigw_12_201812](https://static.toastoven.net/prod_apigateway/apigw_12_201812.png)

1. Click a plugin to delete. 

2. Click **Delete**.

3. Click **OK**.

## Plugins  

### Structure of Plugin Operations

API Gateway provides a variety of plugins, such as access control, authentication, usage quota, and message falsification. 

Plugins can be applied to domains and endpoints. Plugins that are added onto the domain hierarchy are commonly applied to endpoints at subdomains. 

Such is applicable only to the endpoints of a plugin that has been added to the endpoint hierarchy.   

![](http://static.toastoven.net/prod_apigateway/img_12.png)

When API Gateway receives a request, plugins operate in the order of configured attribute groups.    

- Access Control Filter denies requests from restricted users or those exceeding usage quota.  
- Authentication Filter denies requests that are not authenticated or fabricated.  
- Custom Filter fabricates messages for a request/response, or handles with mock responses. 
- Proxy Filter forwards requests to user's API server and is returned with response, which then is delivered to the requester. 

## Domain Plugins 

### IP Access Control 

With IP-based access control, particular IPs may be allowed or denied.  

![apigw_13_201812](https://static.toastoven.net/prod_apigateway/apigw_13_201812.png)

1. Click **Plugin Setting > Access Control** plugin and select **IP Access Control (IP ACL)**. 

2. Use Permit to set whether to allow or deny IP list. 
  * With True, it works as a whitelist (only set IPs are allowed, with all the other IPs denied).
  * With False, it works as blacklist (only set IPs are denied, with all the other IPs allowed).

3. Enter IP in the IPv4 format and click **Add** to add it on the IP list.  

4. After setting is completed, click **Save**. 


### Usage Quota 

API usage may be limited during a specified period. 

![apigw_14_201812](https://static.toastoven.net/prod_apigateway/apigw_14_201812.png)

1. Click **Plugin Setting > Usage Quota** plugin, and select  **Usage Quota**. 

2. Set up with conditions for usage quota.  
  * Specify the number of maximum available API calls for Max Usage Quota. 
  * Specify seconds for Time (Per(sec)). 
  * If it exceeds maximum allowed calls during specified time, API usage shall be limited. 
  * Many conditions can be added to restrict usage, and if more than one condition exceeds quota, usage shall be restricted. 

> [Note]
> The **Usage Quota** plugin set on the domain setting page applies to all endpoint API usage volume under a domain. 
> If usage quota is required for each endpoint, apply the **Endpoint Usage Quota** plugin of an endpoint. 

3. Click **Save** to save setting.  

### Maintenance

To return user-defined responses to all endpoint API calls, due to maintenance, you may use the **Maintenance** plugin. 

![apigw_15_201812](https://static.toastoven.net/prod_apigateway/apigw_15_201812.png)

1. Go to **Plugin Setting > Maintenance** plugin and select **Maintenance Response**.

2. Enter response for maintenance. 유지 관리(Maintenance) 응답 값을 입력합니다.

3. To save the setting, click **Save**.

After deployment, the response set for the Maintenance plugin shall be returned to endpoint API call. 

### Authentication

API Gateways can be authenticated with HMAC (Hash-based Message Authentication Code) or JWT (JSON Web Token).

#### HMAC

HMAC authentication is made available by using request URL and time as message.  

![apigw_16_201812](https://static.toastoven.net/prod_apigateway/apigw_16_201812.png)

1. Click **Plugin Setting > Authentication** plugin and select **HMAC**.

2. Set secret key and clock skew for HMAC.
> [Caution] Setup for Clock Skew   
> If the difference between server time at API Gateway and X-TC-Timestamp sent from client is larger than clock skew, HMAC authentication shall fail. 
> Clock skew is available between 0 and 86400 (sec), and if the value is 0, you may ignore the clock skew.  

3. After setting is completed, click **Save**. 

##### Authentication > HMAC > Call Authentication API 

To enable HMAC authentication, following must be included to the Request Header for a request.   

- Authorization: It is the value in combination of [Method + "\n "+ URL + "\n "+ Timestamp], which is encrypted using the HmacSHA1 algorithm and then base64 encoded. 

- X-TC-Timestamp : ISO datetime format (yyyy-MM-dd'T'HH:mm:ssZZ)

| Request                                                      | StringToSign                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| GET /test/1?query1=1&query2=2<br>X-TC-Timestamp: 2016-07-23T12:20:02+09:00<br><span style="color:red">Authorization: IqY8u/RZY8IMESwa/TPW9P9Z39Y=</span> | GET\n<br>/test/1?query1=1&query2=2\n<br>2016-07-23T12:20:02+09:00 |

> [Note] Request time follows the ISO Datetime format (yyyy-MM-dd'T'hh:mm:ssZ).

##### Code (Java) for Creating Authorization 
```java
String secretKey = "Secret key set on console";
SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes(), "HmacSHA1");
Mac mac = Mac.getInstance("HmacSHA1");
mac.init(signingKey);

String message = "StringToSign";
byte[] rawHmac;
rawHmac = mac.doFinal(message.getBytes());
String authorization = new String(Base64.encodeBase64(rawHmac));
```

#### JWT (JSON Web Token)

Here is how it is authenticated with JWT (Json Web Token).

![apigw_17_201812](https://static.toastoven.net/prod_apigateway/apigw_17_201812.png)

1. Click **Plugin Setting > Authentication** plugin and select **JWT**.

2. Set JWT Secret Key, clock skew, and issuer. 

3. After setting is completed, click **Save**.

> [Note]
> If the difference between the server time at API Gateway and expiration time sent from client is larger than clock skew, JWT authentication shall fail. 
> Anywhere between 0 and 86400 is available for clock skew. 

##### Authorization > JWT (JSON Web Token) > API Call for JWT Authentication

To apply JWT authentication, following value must be included to the Request Header for a request.  

- Authorization : Json Web Token

Request: GET /test/1?query1=1&query2=2<br>
 <span style="color:red">Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJpbnZhbGl...</span>

##### Code (Java) for Creating Authorization 

```
<dependency>
    <groupId>org.bitbucket.b_c</groupId>
    <artifactId>jose4j</artifactId>
	<version>0.5.0</version>
</dependency>
```

```
String secretKey = "secret key set on console";
int expireTimeMinutes = "token expiration time = current time + expireTimeMinutes";
String issuer = "issuer set on console";

JwtClaims claims = new JwtClaims();
claims.setIssuer(issuer);
claims.setExpirationTimeMinutesInTheFuture(expireTimeMinutes);

JsonWebSignature jws = new JsonWebSignature();
jws.setPayload(claims.toJson());
jws.setKey(new HmacKey(secretKey.getBytes()));
jws.setDoKeyValidation(false);
jws.setAlgorithmHeaderValue(AlgorithmIdentifiers.HMAC_SHA256);

String authorization = jws.getCompactSerialization();
```

### Cross-Origin Resource Sharing (CORS)

XMLHttpRequest API call is available by using the Cross-Site method. 

![apigw_18_201812](https://static.toastoven.net/prod_apigateway/apigw_18_201812.png)

1. Click **Plugin Setting > CORS** plugin and select **CORS**.

2. Enter set value for CORS.

  - Access-Control-Allow-Credentials: Set True if it is requested for credential. 

  - Access-Control-Max-Age: Requires by the second, regarding how long to cache response for a preflight. Anywhere between 0 and 86400 is available. 
  - Access-Control-Allow-Origin: Enter original/domain which can access resources.
      - With ''*'', all domains are allowed. (Note, however, since \* does not support credentials, domain must be specified for the allowed origin.)  
      - To allow within a specified domain only, delimit by ',' (comma). 
      - Enter domain in the URI type (scheme, domain, or port) (e.g.: http://api-gw.toast.com:8080).
  - Access-Control-Allow-Methods: Set a method to allow access to resources. Delimit by ',' to specify many methods. 
  - Access-Control-Allow-Headers: Set an HTTP header for a request. Delimit by ',' to set many headers.
  - Access-Control-Expose-Headers: Set a header to allow access by browser (client). Delimit by ',' to set many headers. 
  - For more details regarding CORS regulations, see https://www.w3.org/TR/cors/.

3. After setting is completed, click **Save**.


## Endpoint Plugins  

### Mock Responses

When a request URI for endpoint path is requested, such request is not forwarded to a specified endpoint server but user-defined mock response is returned. 

![apigw_21_201812](https://static.toastoven.net/prod_apigateway/apigw_21_201812.png)

1. Go to **Plugins** and add the **Mock Response** plugin. 

2. Set HTTP Status, Header, and Body for Mock Response and save. 
  - HTTP Status: Set status code for a response. 
  - Headers: Set header and header value to be added for a response header. 
  - Body: Set value for response body.  

3. After setting is completed, click **Save**.

### Pre-Call API

Pre-call API is called before an endpoint and its response code serves as an authentication to decide whether to call endpoint. 

Call Pre-call API, including the request header received via API Gateway, and then the Pre-call API return a response code in accordance with the received header.  

If the response code is 200, endpoint is called; otherwise, the result of response of Pre-call API is returned. 
If it fails to call Pre-call API, the error shall be returned. 

> [Note]  
> API Gateway delivers only the header information of request to URL of Pre-call API. 
> Request URL or body information cannot be delivered. 

![apigw_22_201812](https://static.toastoven.net/prod_apigateway/apigw_22_201812.png)

1. Go to **Plugins** and add the **Pre-call API** plugin.

2. Enter method type and URL for Pre-call API. 

3. After setting is completed, click **Save**.


### Falsify Headers

The Modify Headers plugin allows to falsify header value when request is forwarded to an endpoint server, or to falsify header of a response which is to be delivered from API Gateway to a client.  
![apigw_23_201812](https://static.toastoven.net/prod_apigateway/apigw_23_201812.png)

1. Go to **Plugins** and add the **Falsify Headers** plugin. 

2. Enter setting information. 
  - Request Headers regards to modifying request headers.  
  - Response Headers regards to modifying response headers. 

3. After setting is completed, click **Save**.

> [Note]
> If a header key already exists as set, it shall be overwritten.  



### Usage Quota

API usage may be restricted per path, during specific period. 

![apigw_24_201812](https://static.toastoven.net/prod_apigateway/apigw_24_201812.png)
​	

1. Go to **Plugins** and add the **Usage Quota** plugin. 

2. Enter the maximum available call count during specified time (sec). 
  - Many conditions can be added for usage quota, and if there is more than one configured condition exceeding quota, usage may be restricted. 

3. After setting is completed, click **Save**.


> [Caution]  
> 'Endpoint Usage Quota' refers to usage quota on each endpoint path.     
> If usage quota is required for domain, set Usage Quota on the page of domain setting.  
> Usage quota shall be applied to each, when the usage quota plugin is configured for each domain and endpoint.   
> If usage of domain is above the quota, request shall be denied even though endpoint usage does not exceed the quota; and the endpoint usage will also rise.     

When it exceeds the usage quota, HTTP STATUS 403 response is returned as below:  

```
{
  "header": {
    "resultCode": 20004,
    "resultMessage": "20004 Usage quota exceeded",
    "isSuccessful": false
  }
}
```

### Rewrite URLs

Request URL is rewritten in the pattern expression.  

![apigw_25_201812](https://static.toastoven.net/prod_apigateway/apigw_25_201812.png)

1. Go to **Plugins** and add the **Rewrite URL** plugin.

2. Enter setting information. 
  - Enter a pattern type of Request URL for URI Pattern. 
  - Enter a pattern for rewriting URL, regarding the URL pattern type on (2). 

3. After setting is completed, click **Save**.

#### [Example] Rewriting /api/v2.0/\*\* -> /api/v1.0/\*\*  

- URI Pattern: /api/v2.0/(.\*)
- Rewrite URI: /api/v1.0/%1

With the rules applied, the Request URL `/api/v2.0/members` is changed into  ` /api/v1.0/members` for a request.  


## API Deployment   

### Deploy APIs 

![apigw_26_201812](https://static.toastoven.net/prod_apigateway/apigw_26_201812.png)

1. Click **Deply** of a domain you need to deploy. 

2. Test if call for deployed API is properly made. 
    See if response is delivered as expected, when call is made for endpoint URL which is registered in the domain URL. 

```bash
$ curl -s http://api-gw.cloud.toast.com/apigw/hello
hello world
```

## Statistics 

### Query Statistics  

API statistics shows the average response time for API call at each domain and network traffic usage volume. Statistical data of deployed domains only are available.    

Click domain on the list of domains to see details by chart or UIR pattern. 
Charts are available by every 10 minutes, 1 hour, or 1 day, depending on the search period. 

Statistical data are not collected in real time.  
10-minute or 1-hour data are collected at every 10 minutes, while 1-day data are collected at every hour. 

- Below 6 Hours: By 10 minutes  
- More than 6 hours ~below 7 days: By the hour 
- More than 7 days ~30 days: By the day 
The maximum available search period is 30 days, and 10-minute statistical data are to be retained for up to 3 months. 

![apigw_27_201812](https://static.toastoven.net/prod_apigateway/apigw_27_201812.png)

1. Click **API Gateway > Dashboard** to go to the dashboard page. 

2. Set search period to check statistical data during the period.  
    Up to 30 days are available to search. 

- Domain Key: Origin domain key registered at API setting.  
- Number of successful API calls: Sum of successful API calls 
  - API call is deemed as successful if Response HTTP Status Code is below 400
- Number of failed API calls: Sum of failed API calls 
  - API call is deemed as failure if Response HTTP Status Code is over 400
- Number of immediate responses at API Gateway: When a request is not forwarded to the endpoint server but response is delivered from API Gateway 
  - Some plugins may return responses at API Gateway. For instance, if a request comes from an IP owner who is not allowed, the API Gateway returns 403 Forbidden. Such responses of API Gateway refer to the sum of API calls delivered to the client.  
- Number of API Calls: Sum of all API calls   
  - Number of all inbound API calls to API Gateway (Total API CALL Count = Success +Failure)  
- Average Response Time (ms): Average speed of response  
- Outbound Network Traffic (bytes): Sum of response volume transferred to client from API Gateway  

3. By specifying search period, statistical data can be found for each domain.  

4. Click domain on the list to find its statistical details.  

![apigw_28_201812](https://static.toastoven.net/prod_apigateway/apigw_28_201812.png)

Statistical details show graphs on the number of successful or failed API calls, average response time, or outbound network traffic. 

Statistics can be found in more details for each endpoint path, as in the table below.  

>  [Note] Usage volume of API Calls with CORS Plugin    
>  In the case of CORS plugin, the number of API calls may be larger than the actual volume. 
>  CORS may be requested for a total of two cases, such as a preflight request (OPTIONS method) and an actual request. 
