## Application Service > API Gateway > Console User Guide

## API Gateway Service 
API Gateway service is a unit that allows users to manage APIs served through API Gateway.
Each API Gateway service can manage an API resource and a number of stages, and the API indexes can be checked through dashboard.

### Create API Gateway Service
You can enter API Gateway service information and click Create button to create API Gateway service.

* **Service Name**: The name of the service.
* **Service Description**: The service description.
* **Service ID**: A random ID issued to each service. 

> **[NOTE] API Gateway services creation limit
> **Up to 10** API Gateway Services can be created per project.

### View API Gateway Service
* The list of registered API Gateway services appears.
* If you select a service from the list, the list of registered stages appears.
* To manage resources, click the Resource button in the Service Settings column.
* To manage stages, click the **Stage** button in the Service Settings column.

## Resource
Resource is the area where you design an API that will serve through API Gateway.
All clients requesting APIs can make a request regarding the APIs defined in the Gateway resource.
Resource manages the resource path and method of the API.

1. Resource path: API path
2. Resource method: HTTP method
3. Plugin: Adds add-ins to the resource path or method. 

### Create Resource 
1. To create a resource, click the **Create Resource** button, or click **Create Resource** from the menu that appears upon right-clicking the Resource Tree screen on the left.
2. Write the **Resource Path**. The entire path including the written resource path must not exceed 255 characters.
    - –	e.g./products/, /products/{productsId}, /{proxy+}
3. **Path Variable**: Curly brackets can be used in the Resource path to create a **Path Variable**.
    - **Path Variable**containing **{variable}** or sub-path can be declared as **{variable+}**.
        - **Path Variable** can be utilized in the plugin and backend endpoint settings.
        - **{variable}** declares the value of the path where the path variable is located.
            - e.g./members/{memberId} 
                - **{memberId}** path variable value of /members/id1 request becomes **id1**.
        - **{variable+}** includes the sub-path where the path variable is located to declare a variable. A sub resource path cannot be created in the variable containing the sub-path.
            - e.g./{proxy+} 
                - **{proxy+}** path variable value of **/members/id1** becomes **members/id1**.
- **Plugin**: Check this box if you want to add a plugin that is added to the selected path to the created method as well.
- To create a resource and register a method at the same time, select HTTP method.
- If you make a request to API Gateway with an unregistered resource path, 404 Not Found response is returned.


### Create Method
- Create **HTTP Method** under the selected resource path. 
    - Supported HTTP methods: HEAD, OPTIONS, GET, POST, PUT, DELETE, PATCH
- **Method Name**: Canonical name of the method. The name is displayed as a description on the resource tree screen
- **Method Description**: It is a description about the method.
- **Backend endpoint type**
    - HTTP(S): Passes API requests received by API Gateway to the defined backend endpoint URL path.
    - Custom response: API Gateway returns a defined response regarding the received request.
- **Backend endpoint type: HTTP(S)**
    - Backend endpoint URL path: Sets the API URL of the backend endpoint service where the received API request should be forwarded to.
        - Must begin with the root (/).
        - You can set the path variable that is created from resource in the path.
        - The path variable can be resolved as follows:
            - Single path variable: `${request.path.variable-name}` 
            - Path variable containing sub-path: `${request.path.variable-name+}`
        - Can only set the path variable declared in the selected path and parent path.
- **Backend endpoint type: custom response**
    - Set the custom response.
    - Response status code: Enter the response HTTP status code. (required)
    - Header: Enter the name and value of the response header.
    - Response body: Enter the response body.
    - You can set the path variable that is created from resource in the header and response body.
        - The path variable can be resolved as follows:
            - Single path variable: `${request.path.variable-name}` 
            - Path variable containing sub-path: `${request.path.variable-name+}`
        - Can only set the path variable declared in the selected path and parent path.

- **Plugin**: Check this box if you want to add a plugin that is added to the selected path to the created method as well.
- If you request an unregistered HTTP method to API Gateway, 404 Not Found response is returned.

> **[Note] Resource methods creation limit** 
> **Up to 100** methods including all resource paths can be created.

###  Modify Resources And Methods
- Modify resource path
    - Resource path cannot be modified. To modify a path, it must be deleted and created again.
- Modify method 
    1. HTTP method cannot be modified. To modify an HTTP method, it must be deleted and created again.
    2. Method name, description, and backend endpoint items can be modified. 
    3. To modify, select the method from the resource tree on the left.
    4. Change the settings and click the **Save Changes** button.

> **[Note] Modification of OPTIONS method registered by CORS plugin**
> OPTIONS method registered by CORS plugin cannot be modified.

### Delete Resources And Methods 
- Select the resource path and methods you want to delete.
    - Clicking the **Delete Selected** button brings up the Confirm Delete window.
    - If you right-click the resource tree on the left, a menu appears. If you click Delete Resource or Delete Method in the menu, a confirmation window appears.
-  To delete, click the **Confirm** button. Once deleted, data cannot be recovered.


> **[Caution] Resource path deletion**
> If you delete a resource path, all of its sub resource paths and methods of the selected resource path are deleted as well.

> **[Note] Deletion of OPTIONS method registered by CORS plugin**
>  OPTIONS method registered by CORS plugin cannot be deleted.


### Apply Stage Resource
To change resources and apply the changed resources to the stage, you must **Apply Stage Resource**.

1. To apply the changed resources to the stage, click the **Apply Stage Resource** button.
2. Select the **stage** to apply the changed resources.
3. Click the **Apply** button.


> **[Caution] Application of stage resource**
> - To apply a stage resource, one or more stages must exist.
> - Once a resource is applied to a stage, the resource cannot be restored to the previous state.
> - If the latest resource is already applied to the stage, stage resource cannot be applied.


###  Add/Delete Plugin
Plugin allows you to add additional functions provided by API Gateway.

- **Where to apply plugins**
    - Plugins can be added to the resource path or method.
    - When you add a plugin to a resource path, the plugin is batch applied to the sub methods in the selected path.
    - When you add a plugin to a method, the plugin is applied to the selected method only.
- **Steps for applying plugins**
    - Plugins can be applied during the **Backend Request Pre-Task** and **Frontend Response Pre-Task** steps.
        - **Backend Request Pre-Task**: Applies plugins before passing the API request received by API Gateway to the backend.
        - **Frontend Response Pre-Task**: Applies plugins before the response passed from the backend is forwarded to the frontend.
- **Add Plugin**
    - Click the **+ Plugin** button for the backend request pre-task and frontend response pre-task.
        1. Click the plugin to add.
        2. Enter necessary information in the plugin settings and click the **Add** button.
        3. To batch apply the plugin to the sub-path and method (including the selected path), check the **Overwrite Sub-path and Method** box.
            - **!Caution**: If the plugin is already registered in the sub-path and method, the settings will be overwritten.
        4. Click the **Save Changes** button. 
- **Delete Plugin**
    1. Select the registered plugins for the backend request pre-task and frontend response pre-task.
    2. To batch delete the plugin from the sub-path and method (including the selected path), check the **Overwrite Sub-path and Method** box.
    3. Click the **Delete** button.
    4. Click the **Save Changes** button. 

> **[Caution] Saving changes after adding plugins**
> You must click the **Save Changes** button after adding plugins to save the changed settings.


##  Plugin 
### CORS 
Allows you to call XMLHttpRequest API within the Cross-Site method.

- **The location where the plugins can be applied to**: Resource path
- **Steps for applying plugins**: Backend pre-request task
- **CORS plugin setup**
    - **Access-Control-Allow-Credentials**: Set to True when requesting with a credential.
    - **Access-Control-Max-Age**: Enter for how long you will be caching the response to preflight in seconds. You can enter a value between 0 and 86400.
    - **Access-Control-Allow-Origin**: Enter the domain of the original server where you can access the resource.
        - Enter \* to allow all domains. (However, \* does not support credentials, so a specific domain must be specified in the allowed origin.) 
        - To allow multiple domains, separate them by commas (,).
        - Domains must be entered in the URI format (scheme, domain, port) (e.g. http://example.nhncloudservice.com:8080).
    - **Access-Control-Allow-Methods**: Set the methods to allow access to resources. To specify multiple methods, separate them by ','.
    - **Access-Control-Allow-Headers**: Set the HTTP header which can be used at the request. To set multiple headers, separate them by ','.
    - **Access-Control-Expose-Headers**: Set the header accessible by the browser (client). To set multiple headers, separate them by ','.
    - To find out more about CORS rules, see https://www.w3.org/TR/cors/.

> **[Caution] CORS plugin**
> - Registering the CORS plugin also registers the OPTIONS method to the method of the selected path.
>	If you checked the Overwrite Sub-path and Method box, it is also registered in the sub-path as well.
>	If the OPTIONS method is already registered, it is replaced with the OPTIONS method automatically generated by CORS.
> - The OPTIONS method registered through the CORS plugin cannot be selected from the resource tree. Also, it cannot be modified or deleted.
> - If the CORS plugin gets deleted, the OPTIONS method auto-generated by the CORS plugin is batch deleted. 

### Change Request Header 
Add or change the request header. 

- **The location where the plugins can be applied to**: Resource path and method
- **Steps for applying plugins**: Backend request pre-task
- **Change Request Header Settings**
    - You can click the **\+** button to add a header list.
    - Enter the header name and value.
    - In the header value, you can set the path variable declared from the resource. 
        - The path variable can be resolved as follows:
            - Single path variable: `${request.path.variable-name}` 
            - Path variable containing sub-path: `${request.path.variable-name+}`
        - (Note) Only the path variable declared in the selected path and parent path can be configured.

> **[Note] Addition and change of request header**
> - Any headers missing from the original request are added.
> - Any headers available in the original request are replaced with the header value set by the change request header plugin.
> - Any headers available in the original request cannot be deleted.

###   Change Response Header 
Change response header plugin adds the header to the backend header or changes it. 

- **The location where the plugins can be applied to**: Resource path and method
- **Steps for applying plugins**: Frontend response pre-task
- You can click the **\+** button to add a header list.
- Enter the header name and value. 
- In the header value, you can set the path variable declared from the resource. 
    - The path variable can be resolved as follows:
        - Single path variable: `${request.path.variable-name}` 
        - Path variable containing sub-path: `${request.path.variable-name+}`
    - (Note) Only the path variable declared in the selected path and parent path can be configured.


> **[Note] Addition and change of the response header**
> - Any headers missing from the backend endpoint response are added.
> - Any headers available in the response of the backend endpoint response are replaced with the header value set by the change request header plugin.
    
## Stage
Stage is a phase where resources are deployed. 

- A unique Stage URL is issued per stage. 
- Stages can be used to categorize services by each service or environment (profile) or used for other purposes as well.


### Create Stage

1. From the API Gateway services list, click **Stage Settings**.
2. In the Stage tab, click **Create Stage**. 
3. Enter the stage information and click **Create**.
    - **Stage Name** 
        - Only lowercase alphanumeric characters are allowed, and the length cannot exceed 30 characters.
        - Stage Name is included in Stage URL.
        - A basic stage is created if no stage name has been written. Stage Name is not included in the Stage URL of the basic stage.
    - **Stage URL**: This is a stage URL which can be requested for integration with API Gateway. 
        - API request client can request APIs through the Stage URL.
        - Stage URLs are issued in the following format: 
            - Basic stage: {region}-{api-gateway-service-id}.api.nhncloudservice.com
                - {region}:  Pangyo region(kr1)
                - {api-gateway-service-id}: API Gateway Service ID
            - Normal stage: {region}-{api-gateway-service-id}-{stage-name}.api.nhncloudservice.com
                - {region}:  Pangyo region(kr1)
                - {api-gateway-service-id}: API Gateway Service ID
                - {stage-name}: Entered stage name
    - Backend endpoint URL 
        - Writes the backend endpoint URL to which the request received by API Gateway is to be pass. 
        - You must include the scheme (http:// or https://) when writing the URL.
        - You may enter domain address only or include the sub-path when writing it.
            - e.g. https://api.nhn.com , https://api.nhn.com/apis


> **[Note] Stage** 
> - To create a stage, one or more resources methods must have been registered.
> - **Up to 10** stages can be created per stage. 
> - When passing requests received by API Gateway to backend endpoint, they are passed to the backend endpoint URL defined in the stage by default.


### Modify Stage 
1. Select the stage to modify. 
2. Click the **Modify Stage** button.
3. Modify stage information. The stage description and backend endpoint URL can be modified.
4. After changing the settings, click the **Modify** button.

> **[Caution] Deployment of stage** 
> To apply the modified backend *endpoint* URL to the API Gateway, the stage needs to be deployed.


### Delete Stage
1. Select the stage to delete.
2. Click the **Delete Stage** button.
3. Click **Confirm** in the Confirm delete window. This action cannot be canceled. 

> **[Caution] Deletion of stage**
> - If you delete a stage being used by the service, its request no longer enters the API Gateway. 
> - Since deleted stage cannot be recovered, make sure it is not being used by the service before deleting it.


### Import Resource
To change resources and apply the changed resources to the stage, you must import resources on the stage management screen. 

1. To apply the changed resources to the stage, click the **Import Resource** button.

> **[Caution] Importing resources**
> - Once resources are applied to the stage, they cannot be restored to the previous state.
> - If there is no change to the resources, the Import Resource button is disabled.


###  Deploy Stage
To apply the resources and settings for the stage to the API Gateway Services, the stage needs to be deployed. 

1. In the Stage tab, select the stage to deploy. 
2. Click the **Deploy Stage** button.
3. The Deploy Stage screen appears.
4. Enter the description about the stage deployment. (optional)
5. Click the **Deploy Stage** button.
6. See the stage deployment status for the deployment status.
    -  If it is **Successfully Deployed**, the deployment is complete.
    -  If it is **Failed to Deploy**, then there was an error during deployment . If deployment fails, please try it again. If the issue persists, please contact Customer Center.

> **[Caution] Irrecoverable stage deployment**
> - Once the stage is deployed, it cannot be reverted to the previous deployment settings. (We are currently developing the recovery function which uses the previous deployment history.)

###  IP ACL
API Gateway requests can be allowed/denied for the client IDs specified through IP ACL.

1. In the Stage tab, select the stage.
2. In the Stage Tree screen, select the root (/) path of the stage. 
3. Turn **On** the IP ACL. 
4. Set the IP ACL. 
    - **IP Access Control Type**
        - Allow: Only allow access of specific IPs, and deny all the other IPs. (Whitelist method)
        - Deny: Only deny access of specific IPs, and allow all the other IPs. (Blacklist method)
    - **IP access target**
        - You can choose between single input or bulk input to easily register the IP list.
        - IP access targets can be entered as IPv4's single IP or CIDR.
            - Single IP: 10.0.0.1
            - CIDR example: 10.0.0.1/24


> **[Note] IP ACLs registration count limit and client IP check**
> - For IP ACL, **up to 100** IP access targets can be entered.
> - If the source IP of the client has been changed by network address translation (NAT), please note that the IP ACLs will be checked based on the changed IP.

### Authentication > HMAC
HMAC authentication prevents requests received by the API Gateway being tampered by middle attackers, and also prevents reply attack by setting the expiration period for the requests.

1. In the Stage tab, select the stage.
2. In the Stage Tree screen, select the root (/) path of the stage. 
3. In the Authentication, select HMAC.
4. Enter the HMAC settings. 
    - Secret key: It is a secret key for encrypting SignToString. Make sure the key is not exposed to others. 
    - Request expiration (sec): Denies the request that exceeds the bidirectional time (before and after the past/future point of the request time) of the set expiration. If the request expiration is set to 0, the API Gateway does not check the expiration time.
    - Required validation header list: Write the header list which must be included in the API request validation. When entering a number of lists, separate them by commas (,).
    

> **[Note] HMAC authentication failure response**
> If HMAC authentication fails, 401 Unauthorized response is returned.
>
> **[Caution] Request expiration**
> - If set to 0, it does not check the request expiration. It this case, it can be vulnerable to reply attacks. 
> - If the expiration is too short, the expiration can be elapsed before the API Gateway validates the request, which could lead to the request being denied. It is recommended to set the time to 10 seconds or longer than the expected request expiration.
> - You must check if the NTP (Network Time Protocol, NTP) of the API client is valid because requests can be denied due to non-synced time information.
>
> **[Note] Required validation header**
> If you have set the required validation header, it validates if the required validation header is included in the request and if it is the value containing the header in the signature while validating the API request.
> During the setup, make sure the required validation header is included when creating a request and signature.


#### API Client Actions For HMAC Authentication 
To perform HMAC authentication, the API request client must include the following validation header and request time header when making the request.

| Header Name | Header Value |
| --- | --- |
| Authorization | hmac algorithm="<encrypt_algorithm\>", headers="<validation_headers\>", signature="<base64_digest\>" |
| x-nhn-date |  ISO8601 time format|

> **[Note] x-nhn-date's ISO8601 format** 
> - UTC format: yyyy-MM-dd'T'HH:mm:ssZ
> - UTC-based time offset forma: yyyy-MM-dd'T'HH:mm:ss±hh:mm

- If the authorization or x-nhn-date header is not included in the request, HMAC authentication fails.

- Authorization header values are created as shown below:

| Credential name  | Value   |
| --- | --- |
| algorithm  | HmacSHA256 or HmacSHA1 |
| headers |  When proceeding with HMAC authentication,  the header list console must include the headers registered in the HMAC  validation required header.  |
| signature |  A value encoded with Base64 after  encrypting the SiginToString string  |

#### SignToString Format
```
[HTTP Method]\n
[Request URL]\n
[Request datetime]\n
[header1-name]:[value1]\n
[header2-name]:[value1,value2...]\n
...
```

#### SignToString Example 

- HTTP request original body
```
GET /members?isEnable=false&type=public HTTP/1.1
Host: http://kr1-example.api.nhncloudservice.com
x-nhn-date: 2021-02-23T00:00:00+09:00
x-nhn-client-id: nhn
x-nhn-client-ip: 10.0.0.1,10.0.0.2
```

- SignToString regarding the HTTP request original body 
```
GET
/members?isEnable=false&type=public
2021-02-23T00:00:00+09:00
host:kr1-example.api.nhncloudservice.com
x-nhn-client-id: nhn
x-nhn-client-ip: 10.0.0.1,10.0.0.2
```

- signature generation code example (Java): A value encoded with Base64 after encrypting the SignToString with HMAC
```
String secretKey = "Secret key set to HMAC";
// encryption algorithm HmacSHA1 or HmacSHA256
SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes(), "HmacSHA256");  
Mac mac = Mac.getInstance("HmacSHA256");
mac.init(signingKey);

String message = "StringToSign";
byte[] rawHmac;
rawHmac = mac.doFinal(message.getBytes());
String authorization = new String(Base64.encodeBase64(rawHmac));
```


- Complete HMAC authentication header 
```
Authorization:hmac algorithm="HmacSHA256", headers="host,x-nhn-client-id,x-nhn-client-ip" , signature="V5Dye9kgG3tvZOOZertd5LXE0q8CcJGXCxEFCR71hUE="
x-nhn-date:2021-02-23T00:00:00+09:00
```


> **[Caution] Cautions when generating SignToString**
> - SignToString Each field is separated by new-line characters(\n).
> - Headers defined in headers must be included when generating SignToString.
> - If the defined header is missing from the headers, [header name] and [header value] are not included in the SignToString generation.
> - SignToString must be generated in the order defined in the headers.
>     - e.g. If headers="header1, header2", the headers must be added in the order of header1, header2 when generating the SignToString as well.
> - The entire header name of the SignToString must be changed to lowercase before generating it. 
>     - e.g. X-NHN-Header →  x-nhn-header
> - If there are a number of header values, they must be separated by commas (,) when writing them. 
>   - e.g. header1-name:header1-value1,header1-value2
> - The header names and values are separated by colon (:), and do not include space in-between when separating the values.


### Backend Endpoint URL Override

When passing the requests received by the API Gateway to the backend endpoint, the requests are (by default) passed to the backend endpoint URL defined in the stage.
To override the backend endpoint URL regarding a specific method, set the backend endpoint URL override.

1. In the Stage tab, select the stage.
2. In the Stage tree screen, select the method to override the backend endpoint URL.
3. Turn on override of the backend endpoint URL.
    - Writes the backend endpoint URL to which the request received by API Gateway is to be pass.
    - Can include the sub-path in it.
        - e.g. https://api.nhn.com , https://api.nhn.com/apis

## Check API Call

1. In the Stage tab, select the method of the stage tree.
2. See the Stage URL on the right.
3. Call the API with the HTTP method where the Stage URL is specified. 
    - Example: 
        - Method: GET
        - Stage URL: https://kr1-xxxxx-test.api.nhncloudservice.com/example
    ```
    curl --request GET 'https://kr1-xxxxx-test.api.nhncloudservice.com/example'
    ```


> **[Caution] Stage deployment** 
> To call the API, there must be a deployed stage with the status: Successfully Deployed. 

> **[Note] If the API is not called properly**
> - If 404 NotFound HTTP status code is returned: 
>    1. See if the stage deployment status is Deployed.
>    2. See if the request method and stage URL/path are correct.
>    3. In the backend *endpoint* service, see if there is a request URL regarding the backend endpoint URL path. 
> - As for other error codes, see [Error Code](error-code/) documentation. 


> **[Caution] API Call constraints**
> - In the Gateway client, the request size with the API Gateway is restricted to **max. 10MB.** This value cannot be adjusted.
> - In the API Gateway, the response size of the Gateway client is **max. 10MB.** This value cannot be adjusted. 
> - Response timeout for the request is **max. 60 seconds.** If there is a response delay in the backend endpoint service, a timeout may occur.


> **[Caution] API Gateway request ban policy**
> - If the endpoint service does not respond or continues to cause delayed response (over 60 sec) as a way of protecting the API Gateway Services and backend endpoint service, the request relating to the backend endpoint service is temporarily denied.
> - It is not banned by the internal errors (4xx, 5xx, etc.) of the backend endpoint service.
> - It is not recommended to link the backend endpoint service if it is not properly operable or if the delayed response (timeout) persists for over 60 seconds.


## Dashboard 

You can see the API statistical indexes by each API Gateway Service.  

1. Go to the **Dashboard** tab. 
2. Select the API Gateway Service to see the statistics. 
3. From the list, select the stage to check the statistics. 
4. In the Stage statistics tab at the bottom, you can see the statistical indexes for the stage. 
5. In the Resources statistics tab at the bottom, you can see the statistical indexes for each HTTP method and path.

### Note on Statistical Data

- **Max. Search Period**
    - Only data for the past 3 months can be viewed.
- **Statistical Data Generation Cycle**
    - Statistical data is generated in the following cycle. The statistical data can be delayed depending on the size of the collected data.
        - 1 minute: e.g. Statistical data for 10:00 gets generated after 10:01.
        - 10 minutes: e.g. Statistical data for 10:10 gets generated after 10:11.
        - 1 hour: e.g. Statistical data for 10 gets generated after 11.
        - 11 day: e.g. Statistical data for day 1 gets generated after day 2, 00:00.

### Stage Statistics

- **Graph Display Standard**
    - The units of the statistics are displayed as the following depending on the search period.
        - Less than 1 hour: unit of 1 minute
        - Longer than 1 hour - less than 1 day: unit of 10 minutes
        - Longer than 1 day - less than 1 week: unit of 1 hour
        - Longer than 1 week: unit of 1 day
-  **Statistical Graph**
    - Number of successful API calls: Number of API calls with the responded HTTP status code of 2XX, 3XX 
    - Number of failed API calls: Number of API calls with the responded HTTP status code of 4XX, 5XX 
    - Average response time (ms): The average time spent from the point where the request entered the API Gateway to the point where the response was given to the API request client
    - Network outbound traffic: The byte size of the data responded with the API request client at the API Gateway

### Resources Statistics 
You can see more detailed statistical indexes categorized by resource path and HTTP method. 

- **HTTP method**: Requested HTTP method
- **Path**: Resource path mapped with the request 
- **Number of successful API calls**: Number of API calls with the responded HTTP status code of 2XX, 3XX 
- **Number of failed API calls**: Number of API calls with the responded HTTP status code of 4XX, 5XX
- **HTTP 2XX~5XX code**: Number of API calls by status code group
- **Number of immediate responses at the API Gateway**: Number of API calls responded at the API Gateway without passing the request to the backend endpoint service 
- **Average response time (ms)**: The average time spent from the point where the request entered the API Gateway to the point where the response was given to the API request client
- **Network outbound traffic**: The byte size of the data responded with the API request client at the API Gateway
