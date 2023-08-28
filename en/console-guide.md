## Application Service > API Gateway > Console User Guide

## API Gateway Service 
API Gateway service is a unit that allows users to manage APIs served through API Gateway.
Each API Gateway service can manage an API resource and a number of stages, and the API indexes can be checked through dashboard.

### Create API Gateway Service
You can enter API Gateway service information and click Create button to create API Gateway service.

* **Service Name**: The name of the service.
* **Service Description**: The service description.
* **Service ID**: A random ID issued to each service. 

> **[NOTE] API Gateway services creation limit**
> **Up to 10** API Gateway Services can be created per project.

### View API Gateway Service
* The list of registered API Gateway services appears.
* If you select a service from the list, the list of registered stages appears.
* To manage resources, click the Resource button in the Service Settings column.
* To manage stages, click the **Stage** button in the Service Settings column.

### Delete API Gateway Service
* The list of registered API Gateway services is displayed.
* Select the service from the list, and click the **Delete** button.
* When the confirmation window appears, click the **OK** button. Deleted data cannot be restored.

> **[Caution] When API Gateway service cannot be deleted**
> API Gateway service cannot be deleted if there is a usage plan connected to the stage of the API Gateway service.

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
    - **Path Variable** containing **{variable}** or child path can be declared as **{variable+}**.
        - **Path Variable** can be utilized in the plugin and backend endpoint settings.
        - **{variable}** declares the value of the path where the path variable is located.
            - e.g./members/{memberId} 
                - **{memberId}** path variable value of /members/id1 request becomes **id1**.
        - **{variable+}** includes the child path where the path variable is located to declare a variable. A child resource path cannot be created in the variable containing the child path.
            - e.g./{proxy+} 
                - **{proxy+}** path variable value of **/members/id1** becomes **members/id1**.
- **Plugin**: Select this option if you want to add a plugin that is added to the selected path to the created method as well.
- To create a resource and register a method at the same time, select HTTP method.
- If you make a request to API Gateway with an unregistered resource path, 404 Not Found response is returned.

### Import Resource
You can bring the resource through the file format of Swagger v2.0 [OpenAPI Specification](https://swagger.io/specification/v2/)
1. Click the button **Import Resource**.
2. Click the Swagger **Select File** button and choose the file, or directly enter the Swagger content.
3. Click the **Apply** button.

> **[Caution] When a resource is imported, the existing resources and models are overwritten**
> When a resource is imported, all existing resources are deleted and overwritten with the imported resource.
> When a resource is imported, all existing models created in the service are deleted and overwritten with the imported model.

> **[Note] Failing to import stage files exported before Nov. 23, 2021** 
> If you import resources with files downloaded via stage export before Nov. 23, 2021, the operation may fail.
> Use the resource import using the newly created file through stage export, or change the existing file with the following:
> Modification
> 1. Convert the plugin configuration string of x-api-nhn-apigateway > plugins in the file to a JSON object.
> 2. If the CORS plugin configuration string exists in the resource method > x-api-nhn-apigateway > plugins in the file, it must be removed. You cannot configure a CORS plugin on a resource method, and if a CORS plugin is configured in its parent resource path, it is automatically added when importing a resource.
> If the guide does not solve the problem, please contact the Customer Center.

<details>
<summary>Example of failing to import stage files exported before Nov. 23, 2021</summary>

```
- [Example 1] Import failure: Stage export files before Nov. 23, 2021 includes plugin setting of plugins in JSON format strings
{
... 
    "x-nhncloud-apigateway": {
        "plugins": {
            "HTTP": "{\"frontendEndpointPath\":\"/{proxy+}\",\"backendEndpointPath\":\"/anything/${request.path.proxy+}\"}",
        }
    }
...
}
```

```
- [Example 1] Import success: Stage export file in which JSON format string is modified into JSON object in plugin setting of plugins
{
...
    "x-nhncloud-apigateway": {
        "plugins": {
            "HTTP": {
                "frontendEndpointPath": "/{proxy+}",
                "backendEndpointPath": "/anything/${request.path.proxy+}"
            }
        }
    }
...
}
```

```
- [Example 2] Import failure: For stage export files before Nov. 23, 2021, if CORS plugin is configured in resource path, CORS plugin setting is included in child resource method
{
...
        "paths": {
            "/anything": {
                "get": {
                    ...
                    "x-nhncloud-apigateway": {
                        "plugins": {
                            "MOCK": {
                                "statusCode": 200
                            },
                            "CORS": {
                                "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                                "allowedHeaders": ["*"],
                                "allowedOrigins": ["*"],
                                "exposedHeaders": [],
                                "maxCredentialsAge": null,
                                "allowCredentials": false
                            }                            
                        }
                    }
                },
                "options": {
                    "summary": "CORS",
                    ...
                },
                "x-nhncloud-apigateway": {
                    "plugins": {
                        "CORS": {
                            "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                            "allowedHeaders": ["*"],
                            "allowedOrigins": ["*"],
                            "exposedHeaders": [],
                            "maxCredentialsAge": null,
                            "allowCredentials": false
                        }
                    }
                }
            }
        }
...
}
```

```
- [Example 2] Import success: Stage export file with CORS plugin setting removed from resource method
{
...
        "paths": {
            "/anything": {
                "get": {
                    ...
                },
                "options": {
                    "summary": "CORS",
                    ...
                },
                "x-nhncloud-apigateway": {
                    "plugins": {
                        "CORS": {
                            "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                            "allowedHeaders": ["*"],
                            "allowedOrigins": ["*"],
                            "exposedHeaders": [],
                            "maxCredentialsAge": null,
                            "allowCredentials": false
                        }
                    }
                }
            }
        }
...
}
```
</details>

### Create Method
- Create **HTTP Method** under the selected resource path. 
    - Supported HTTP methods: HEAD, OPTIONS, GET, POST, PUT, DELETE, PATCH
- **Method Name**: Canonical name of the method. The name is displayed as a description on the resource tree screen.
- **Method Description**: It is a description about the method.
- **Backend endpoint type**
    - HTTP(S): Passes API requests received by API Gateway to the defined backend endpoint URL path.
    - Custom response: API Gateway returns a defined response regarding the received request.
- **Backend endpoint type: HTTP(S)**
    - Backend endpoint URL path: Sets the API URL of the backend endpoint service where the received API request should be forwarded to.
        - Must begin with the root (/).
        - Context variables created by the resources can be set for the path. (For more information on context variables, see [Context Variables](./console-guide/#context-variables).)
- **Backend endpoint type: custom response**
    - Set the custom response.
    - Response status code: Enter the response HTTP status code. (required)
    - Header: Enter the name and value of the response header.
    - Response body: Enter the response body.
    - Context variables created by the resources can be set for the header. (For more information on context variables, see [Context Variables](./console-guide/#context-variables).)

- **Plugin**: Select this option if you want to add a plugin that is added to the selected path to the created method as well.
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
- To delete, click the **Confirm** button. Once deleted, data cannot be recovered.


> **[Caution] Deletion of resource path**
> If you delete a resource path, all child resource paths and methods of the selected resource path are deleted.

> **[Note] Deletion of OPTIONS method registered by CORS plugin**
>  OPTIONS method registered by CORS plugin cannot be deleted.


### Apply Stage Resource
To change resources and apply the changed resources to the stage, you must **Apply Stage Resource**.

1. To apply the changed resources to the stage, click the **Apply Stage Resource** button.
2. Select the **Stage** to apply the changed resources.
3. Click the **Apply** button.


> **[Caution] Applying stage resource**
> - To apply a stage resource, one or more stages must exist.
> - Once a resource is applied to a stage, the resource cannot be restored to the previous state.
> - If the latest resource is already applied to the stage, stage resource cannot be applied.


###  Add/Delete Plugin
Plugin allows you to add additional functions provided by API Gateway.

- **Where to apply plugins**
    - Plugins can be added to the resource path or method.
    - When you add a plugin to a resource path, the plugin is batch applied to the child methods of the selected path.
    - When you add a plugin to a method, the plugin is applied to the selected method only.
- **Steps for applying plugins**
    - Plugins can be applied during the **Backend Request Pre-Task** and **Frontend Response Pre-Task** steps.
        - **Backend Request Pre-Task**: Applies plugins before passing the API request received by API Gateway to the backend.
        - **Frontend Response Pre-Task**: Applies plugins before the response passed from the backend is forwarded to the frontend.
- **Add Plugin**
    - Click the **+ Plugin** button for the backend request pre-task and frontend response pre-task.
        1. Click the plugin to add.
        2. Enter necessary information in the plugin settings and click the **Add** button.
        3. To batch apply the plugin to the child path and method (including the selected path), select **Overwrite Child Path and Method**.
            - **!Caution**: If the plugin is already registered in the child path and method, the settings will be overwritten.
        4. Click the **Save Changes** button. 
- **Delete Plugin**
    1. Select the registered plugins for the backend request pre-task and frontend response pre-task.
    2. To batch delete the plugin from the child path and method (including the selected path), select **Overwrite Child Path and Method**.
    3. Click the **Delete** button.
    4. Click the **Save Changes** button. 

> **[Caution] Saving changes after adding plugins**
> You must click the **Save Changes** button after adding plugins to save the changed settings.


### Request Parameters
Set request parameters, response types, and content type for each resource method.  
Settings are applied to [API document](./console-guide/#api-document_1).

1. Select the resource method.
2. Click the **Request parameter** tab.
3. Enter the request parameter items. 
    - Click the **+ button** on the right side of items to add an item.
    - Click the **- button** on the right side of the item to delete the item.
    - Query String, Header, Form Data parameters
        - Name: Enter the parameter name. 
        - Description: Enter the parameter description.
        - Data Type: Enter the data type of the parameter.
        - Required: Select whether the parameter is required or not.
        - Array: Select whether the parameter data is array or not. 
    - Request Body parameter
        - Name: Enter the name of the request body parameter. 
        - Description: Enter the parameter description.
        - Model: Select the [Model](./console-guide/#model) of the request body.
    - Content Type
        - Enter the content type (e.g., application/json) of the documents to send to the server.
4. Click the **Save Changes button**.

### Response
Set header, request body, and content type for each HTTP response status code.
Settings are applied to [API document](./console-guide/#api-document_1).

1. Select the resource method.
2. Click the **Response** tab.
3. Click the **Add button** of the response HTTP status code to display the additional input screen.
4. Enter the response HTTP status code and description to add.

5. Click the **Create button**. 
6. Select the row for the added response HTTP status code.
7. Enter the response header and response body for each response HTTP status code.  
    - Header
        - Name: Enter the header name. 
        - Description: Enter the header description.
        - Data Type: Enter the data type of the response header.
    - Response Body 
        - Name: Enter the name of the response body parameter. 
        - Description: Enter the description of the response body parameter.
        - Model: Select the model of the response body. 
8. Enter the content type. 
    - Enter the content type (e.g., application/json) of the documents to respond to the client. 
9. Click the **Save Changes button**.

## Context Variables
The variables defined below can be used when creating methods of resources or setting plugins.

| Context Variables | Description |
| -- | -- |
| ${request.clientIp} | IP of the client that requested API |
| ${request.path.variable-name} | Reference the value of a single path variable {variable-name} declared by the resource |
| ${request.path.variable-name+} | Reference the value of the path variable including child paths {variable-name+} declared by the resource |

> **[Caution] Path Variables**
> You can only use the path variables declared in the selected path and its parent path.

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
>	If you selected the Overwrite Child Path and Method option, it is also registered in the child path.
>	If the OPTIONS method is already registered, it is replaced with the OPTIONS method automatically generated by CORS.
> - The OPTIONS method registered through the CORS plugin cannot be selected from the resource tree. Also, it cannot be modified or deleted.
> - If the CORS plugin gets deleted, the OPTIONS method auto-generated by the CORS plugin is batch deleted. 

### Change Request Header 
Adds or changes the request header. 

- **The location where the plugins can be applied to**: Resource path and method
- **Steps for applying plugins**: Backend request pre-task
- **Change Request Header Settings**
    - You can click the **\+** button to add a header list.
    - Enter the header name and value.
    - Context variables declared by the resources can be set for the header value. (For more information on context variables, see [Context Variables](./console-guide/#context-variables).) 
      
      
> **[Note] Adding and changing the request header**
> - Any headers missing from the original request are added.
> - Any headers available in the original request are replaced with the header value set by the change request header plugin.
> - Any headers available in the original request cannot be deleted.

### Change Response Header 
Change response header plugin adds the header to the backend response or changes the header. 

- **The location where the plugins can be applied to**: Resource path and method
- **Steps for applying plugins**: Frontend response pre-task
- You can click the **\+** button to add a header list.
- Enter the header name and value. 
- Context variables declared by the resources can be set for the header value. (For more information on context variables, see [Context Variables](./console-guide/#context-variables).)


> **[Note] Adding and changing the response header**
> - Any headers missing from the backend endpoint response are added.
> - Any headers available in the response of the backend endpoint response are replaced with the header value set by the change request header plugin.

### Add Request Query String Parameter
Adds a request query string parameter to backend endpoint.  
Example: If the parameter name and value are set to 'name' and 'value', **name=value** query string parameter is added when backend endpoint is requested. 

- **The location where the plugin can be applied**: Resource path, method
- **Steps for applying plugins**: Backend request pre-task
- **\+** button allows you to add a parameter list.
- Enter the parameter name and value. 
- Context variables declared by the resources can be set for the parameter value. (For more information on context variables, see [Context Variables](./console-guide/#context-variables).)

> **[Note] Request Query String Parameter**
> - The requested query string parameter that has the same key as the originally requested query string parameter does not replace the originally requested query string but instead adds the query string parameter. 
> - The value of the query string parameter is encoded and delivered to the backend endpoint.


## Stage
Stage is a phase where resources are deployed. 

- A unique Stage URL is issued per stage. 
- Stages can be used to categorize services by each service or environment (profile) or used for other purposes.

### Create Stage

1. From the API Gateway services list, click **Stage Settings**.
2. In the Stage tab, click **Create Stage**. 
3. Enter the stage information and click **Create**.
    - **Stage Name** 
        - Only lowercase alphanumeric characters are allowed, and the length cannot exceed 30 characters.
        - Stage Name is included in Stage URL.
        - A default stage is created if no stage name has been written. Stage Name is not included in the Stage URL of the default stage.
    - **Stage URL**: This is a stage URL which can be requested for integration with API Gateway. 
        - API request client can request APIs through the Stage URL.
        - Stage URLs are issued in the following format: 
            - Default stage: {region}-{api-gateway-service-id}.api.nhncloudservice.com
                - {region}:  Pangyo region(kr1)
                - {api-gateway-service-id}: API Gateway Service ID
            - Normal stage: {region}-{api-gateway-service-id}-{stage-name}.api.nhncloudservice.com
                - {region}:  Pangyo region(kr1)
                - {api-gateway-service-id}: API Gateway Service ID
                - {stage-name}: Entered stage name
    - Backend endpoint URL 
        - Writes the backend endpoint URL to which the request received by API Gateway is to be pass. 
        - You must include the scheme (http:// or https://) when writing the URL.
        - You may enter domain address only or include the child path when writing it.
            - e.g. https://api.nhn.com , https://api.nhn.com/apis
        - If you specify the port directly in the URL, only ports 80, 443, 10000-12000 can be used.


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
> - If there is a usage plan connected to the stage, the stage cannot be deleted.


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
    - If it is **Successfully Deployed**, the deployment is complete.
    - If it is **Failed to Deploy**, then there was an error during deployment . If deployment fails, please try it again. If the issue persists, please contact Customer Center.

### Stage Deployment History
You can verify deployment history after stage deployment, and go back stages by setting up Previous Deployment.

1. On the **Stage** tab, select a stage.
2. Select **Deployment History** tab.
3. You can verify history of Stage Deployment.
    - **Deployed Stage**: Refers to the deployment history applied to present API Gateway service. 
    - **Base Stage**: Refers to the deployment history that becomes the foundation for present stage setup. It is changed when conducting Stage Deployment or Restore Stage. 
    - **Restore Stage**: A stage setup of the relevant deployment history. The present Stage Setup is modified.
    - **Delete**: Unnecessary deployment history is deleted.

> **[Caution] Restore stage to previous deployment history**
> - If you use Restore Stage, you must deploy stage if you wish to apply it to API Gateway service.


### Export Stage
1. On the **Stage** tab, select a stage.
2. Select the **Export Stage** tab.
3. Click the **Export the Stage** button to save the selected stage’s resource in a Swagger file.


### API Document
You can check the configuration deployed through **stage deployment** with the API document.
Refer to [API document](./console-guide/#api-document_1) for details.

###  IP ACL
API Gateway requests can be allowed/denied for the client IDs specified through IP ACL.

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab. 
3. Select the Stage root(/) path on the Stage Tree screen. 
4. **Activate (On)** the IP ACL. 
5. Set up the IP ACL. 
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

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab.
3. Select the Stage root(/) path on the Stage Tree screen. 
4. In the authentication, select **HMAC**.
5. Enter the HMAC setup. 
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
>     - e.g. If headers="header1, header2", the headers must be added in the order of header1, header2 when generating the SignToString.
> - The entire header name of the SignToString must be changed to lowercase before generating it. 
>     - e.g. X-NHN-Header →  x-nhn-header
> - If there are a number of header values, they must be separated by commas (,) when writing them. 
>   - e.g. header1-name:header1-value1,header1-value2
> - The header names and values are separated by colon (:), and do not include space in-between when separating the values.

### Authentication > JWT  
Verifies the signature and claim of JWT token. Token values can be used without token verification for user services.

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab. 
3. Select the Stage root(/) path on the Stage Tree screen. 
4. In the authentication, select **JWT**.
5. Enter the JWT setup. 
    - **Token Encryption Algorithm**: Select the encryption algorithm used to sign the token. Encryption algorithm supports HS256 and RS256.
        - HS256 Token Algorithm
            - Secret Key: Enter the secret key used to sign the token. Secret key with the length of 256 or above is recommended.
        - RS256 Token Algorithm
            - Public Key (PEM): Enter the public key to verify the token. It must be entered in PEM format.
            - JWKS URI: Enter the HTTP JWKS (JSON Web Key Set) URI from which API Gateway retrieves the JWKS object required for token signature verification and encryption.
    - **Claim Verification Condition**
        - Enter the claim verification conditions for the registered claim of the token payload.
        - For more information on the registered claims, see [RFC7519-4.1.Registered Claim Names](https://tools.ietf.org/html/rfc7519#section-4.1).
        - If any one of the claim verification conditions is not met, verification fails.
        - **Claim**: Name of the registered claim of the token payload.
        - **Data Type and Claim Value**:
            - Array: Enter multiple strings separated by commas (,). If the string array contains at least one claim value of the request token, the verification succeeds.
            - String: Enter a single string. If it matches the claim value of the request token, the verification succeeds.
        - **Required**: Verification fails if claims do not exist in the request token when selected. A disabled checkbox cannot be selected or cleared.
        - **Value Verification**: If a claim exists in the request token when selected, verification will proceed to check whether the set claim value includes or matches the claim or not. A disabled checkbox cannot be selected or cleared.
    - **Verification Time Limit (sec)**: Apply verification time limit to verify exp and nbf claims of the request token. You can enter any number between 0 and 86,400 (sec).
6. Deploy the stage.
7. When requesting API Gateway, first add a JWT token to the Authorization Header and then make a request.

| Header name | Header value |
| --- | --- |
| Authorization | Bearer "<jwt-token\>" |

> **[Note] JWT Token Authentication Failure Response**
> If the authentication of JWT token fails, 401 Unauthorized response is returned.
> For more information, see the [Gateway Error Code](./error-code/) document.
>
> **[Note] Creating JWT Token**
> API Gateway only verifies whether the JWT token signature and claims match or not. A JWT Token must be created via user applications or authentication service providers.
> To learn how to create a JWT token for the purpose of development and testing, see [JWT Token Debugger](https://jwt.io/).
>
> **[Note] JWKS (JSON Web Key Set) URI description and precautions**
> JWKS is the JSON data for the JWK (JSON Web Key) encryption key that the API Gateway needs to verify token signatures.
> For more details and specifications on JWK, please refer to the [RFC7515](https://tools.ietf.org/html/rfc7517) document.
> The selected JWKS URI must be disclosed so that the API Gateway can access it, and should not be blocked with networks, firewalls, etc.
> The selected JWKS URI must be operated so that the API Gateway can always access it. 
> If you specify the port directly in the JWKS URI, only ports 80, 443, 10000-12000 can be used.
>
> **[Caution] JWKS Caching**
> API Gateway caches JWKS URI's response for 5 minutes.
> Due to caching by API Gateway, it may take a maximum of 5 minutes for modifications in JWKS to be reflected in API Gateway.

### Access Log
This is a feature that lets you store API Gateway's access logs in the Log & Crash Search service.

1. On the **Stage** tab, select a stage.
2. Select the **Settings** tab.
3. In the stage tree view, select the root (/) path of the stage. 
4. **Enable (On)** the access log feature. 
5. If you are not using the Log & Crash Search service, click **Enable Log & Crash Search Service** to enable the service. 
6. Click **Modify** to save your settings.
7. After running **Deploy Stage**, access logs are stored in the Log & Crash Search service. 

Access logs can be found in the Log & Crash Search service. 

1. Go to the Log & Crash Search service console page. 
2. Retrieve logs with logType field "NNH Cloud-API Gateway" in the Log & Crash Search service. 
    - Retrieval query: `logType: "NHN Cloud-APIGateway"`
    - For details on how to use the console, refer to the [Log & Crash Search service console guide](/Data%20&%20Analytics/Log%20&%20Crash%20Search/en/console-guide/).
3. The content of fields to be stored in Log & Crash Search is as follows.

| Field | Description |
| --- | --- |
| longRequestTime | Timestamp of the request date and time |
| requestPath | Request path |
| resourcePath | Resource path to which the request is mapped |
| requestHttpMethod | Request HTTP method |
| clientIp | Request client IP |
| responseHttpStatus | Response HTTP status code |
| body | String in the format {clientIp} - [{requestTime}] "{requestHttpMethod} {requestPath}" {responseHttpStatusCode} |
| host | Request host: Domain of the stage URL |
| logType | Log type: A fixed value of "NHN Cloud-APIGateway" |
| logLevel |  Log level: "INFO" for response status code lower than 400, "ERROR" for response status code 400 or higher |
| errorCode | Gateway error code if an error occurred in API Gateway, empty value if no error occurred |
| errorMessage | Gateway error message if an error occurred in API Gateway, empty value if no error occurred |


> **[Note]** Log & Crash Search usage fee information
> Access logs are stored in the Log & Crash Search service, and the Log & Crash Search service usage fee is charged separately.
> Refer to the links below for the Log & Crash Search service introduction and usage fee.
> <a class='text-guide' target='_blank' href='https://www.nhncloud.com/kr/service/analytics/log-crash-search'>Go to the Log & Crash Search service introduction</a>
> <a class='text-guide' target='_blank' href='https://www.nhncloud.com/kr/service/analytics/log-crash-search#price'>Go to the Log & Crash Search usage fee</a>
> 
> **[Caution]** Notification on disabling the Log & Crash Search service while using the access log feature
> If you disable the Log & Crash Search service while using the access log feature, the access logs are no longer stored and the access log feature is automatically disabled.
> To use the access log feature again, enable the Log & Crash Search service and then enable the access log feature again.



### Pre-call API
Pre-call API determines whether or not to call the backend endpoint depending on the call response code after calling the user-designated API before calling the backend endpoint.
Pre-call API including the request headers that came in through the API Gateway is called, and the Pre-call API will return the response code depending on the forwarded header content.

Backend endpoint is called if Pre-call API’s response code is 200; Pre-call API’s response result is returned if the response code is not 200.
If Pre-call API call fails, it returns an error.

This can be used in a situation where authentication through a separate API call is required before calling the backend endpoint or there is another API to be called.

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab. 
3. In the Stage Tree screen, select the path or method to apply the Pre-call API.
    - Pre-call API set in a path is applied to all child paths and method calls defined under the path.
    - Pre-call API set in a method is applied when calling the method, but Pre-call API set in the root path is not applied.
4. Activate the Pre-call API.
    - Enter the method type and URL for Pre-call API.
        - If you specify the port directly in the URL, only ports 80, 443, 10000-12000 can be used.	
    - Cache time limit can be set to 86400 sec at maximum, and the response results are cached for the period specified by the entered number (seconds).
    - If the cache time limit it set to 0, response results for Pre-call API will not be cached and Pre-call API will be called for every request.
  
> **[Note] Response Result Caching for Pre-call API**
> Response results are only cached if Pre-call API’s response result code is 200.
> If the response result code is not 200, response results will not be cached even if the cache time limit is set.

### Backend Endpoint URL Override

When passing the requests received by the API Gateway to the backend endpoint, the requests are (by default) passed to the backend endpoint URL defined in the stage.
To Override the backend endpoint URL concerning certain path or method, set up the redefinition of backend endpoint URL.

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab.
3. Select the path or method to redefine the backend endpoint URL in the Stage Tree screen.
4. Turn on override of the backend endpoint URL.
    - Writes the backend endpoint URL to which the request received by API Gateway is to be pass.
    - Can include the child path in it.
        - e.g. https://api.nhn.com , https://api.nhn.com/apis
    - If you specify the port directly in the URL, only ports 80, 443, 10000-12000 can be used.

### Request Number Limit

Requests received by the API gateway every second can be adjusted using the request number limit, and the backend endpoint can be protected via the request number limit.

1. On the **Stage** tab, select a stage.
2. Select the **Setup** tab. 
3. On the Stage Tree screen, select the root (/) path or method of the stage.
    - If set for the root path, request number limit will be applied to the stage.
    - If set for the method, request number limit will be applied to each method. Request number limit set for the parent path will be ignored. 
4. Turn the request number limit **On**. 
5. Set the request number limit. 
    - Requests per Second: Enter the maximum number of requests that can be called in seconds.
    - Request Limit Key: The default request limit key is stage when set for the root, and method when set for the method. A request limit key can be added to the default request limit key.
        - None: Limits requests to default request limit key.
        - Path Variable: Limits requests for the default request limit key and different path variables. It can be set if the selected method path has a path variable.  
        - IP: Limits requests for each default request limit key and request client IP.
        - Header: Limits requests for each default request limit key and set header name value. 

>
> **[Note] Request Number Limit Response**
> If requests per second is exceeded, the response of 429 Too Many Requests is returned.
>       
> **[Caution] Request Limit Key**
> When using the request limit key, the request must contain the specified key. For example, if header is selected for the request limit key and the X-NHN-CLOUD value is entered, the request header must contain X-NHN-CLOUD.      
> If the request limit key cannot be found from the request, the request number limit is not applied.
>
> **[Caution] Accuracy of Requests Per Second**
> - The requests per seconds set and the actual number of requests could slightly differ depending on the time delivered to API Gateway, request processing time, and other factors.  

### Request Restriction Policy 
Applies registered request restriction policy to stage resource paths or methods. For more information, see [Request Restriction Policy](./console-guide/#request-restriction-policy_1).

1. Select a stage on **Stage** tab.
2. Select **Settings** tab.
3. On Stage Tree screen, select a path or method you want to apply request restriction policy.
4. **Enables (On)** request restriction policy.
5. Select a request restriction policy to apply and click on **Modify** button to save it.
6. Click on the **Deploy Stage** button. When the stage deployment is complete, the set request restriction policy works.

### API Key

When making an API request to API Gateway, it is restricted to only the specified API key to be requested.

- Examines if it is a valid API key value.
- Only the API key connected to the stage of the usage plan can request the API of the stage. (For details, refer to [Usage Plan > Connect Stage to Usage Plan](./console-guide/#connect-stage-to-usage-plan).)
- Examines the request limit of the usage plan the API key is connected to. (For details on how to set the request limit of a usage plan, refer to [Usage Plan > Create Usage Plan](./console-guide/#create-usage-plan).)

> **[Note] API key failure response**
> The API request is rejected when the API key value is not included in the requested header, of its invalid, or exceeds the usage limit.
> For more information, see the [Gateway Error Code](./error-code/) document.

1. On the **Stage** tab, select a stage.
2. Select the **Settings** tab.
3. Select the path or method to enable API key in the stage tree screen.
   - The API key set in a path is applied to all child paths and method calls defined under the path.
4. Enable the API key.
5. Deploy the stage.
6. When requesting API, it is requested by adding the API key value to the x-nhn-apikey header.

| Header name | Header value |
| --- | --- |
| x-nhn-apikey | <primary api key or secondary api key\> |


## Model
You can define a model to specify the format of body that you can use in the request parameters and the response.

### Create Model
1. Click **Resource** in the service settings column from the list of API Gateway services.
2. In the **Model** tab, click the **Create model** button.
3. Enter the model information and click **Create**.
    - **Model name**:
        - The name of the model. It cannot be the same as the name of the existing model.
        - Only numbers and English letters can be entered, up to 50 characters.
    - **Model description**: It is the description of the model. (optional)
    - **Model schema**:
        - Define the structure that the model can have.
        - Use [JSON Schema](https://json-schema.org/) draft-04 for the model schema definition.

### Edit Model
1. Select the model to edit from the list of models.
2. Click the **Edit** button.
3. Edit the model information. Items that can be edited are model description and model schema.
4. After changing the settings, click the **Edit** button.

### Delete Model
1. Select the model to delete from the list of models.
2. Click the **Delete** button.
   - The model cannot be deleted while being used in the request parameters or response.
3. When the delete confirmation window appears, click the **Confirm** button. Deleted data cannot be restored.



## Model
You can define a model to specify the format of body that you can use in the request parameters and the response.

### Create Model
1. Click **Resource** in the service settings column from the list of API Gateway services.
2. In the **Model** tab, click the **Create model** button.
3. Enter the model information and click **Create**.
    - **Model name**:
        - The name of the model. It cannot be the same as the name of the existing model.
        - Only numbers and English letters can be entered, up to 50 characters.
    - **Model description**: It is the description of the model. (optional)
    - **Model schema**:
        - Define the structure that the model can have.
        - Use [JSON Schema](https://json-schema.org/) draft-04 for the model schema definition.

### Edit Model
1. Select the model to edit from the list of models.
2. Click the **Edit** button.
3. Edit the model information. Items that can be edited are model description and model schema.
4. After changing the settings, click the **Edit** button.

### Delete Model
1. Select the model to delete from the list of models.
2. Click the **Delete** button.
   - The model cannot be deleted while being used in the request parameters or response.
3. When the delete confirmation window appears, click the **Confirm** button. Deleted data cannot be restored.

## Request Restriction Policy 
request restriction policy is a feature that allows you to set IP ACLs and request count limits based on a request's path variable or request header value.

### Create request restriction policy 
1. In the list of API Gateway services, click **Resource** in Service Settings column.
2. On **Request Restriction Policy** tab, click on **Create Request Restriction Policy**.
3. Enter request restriction policy information. 
    - **Request Restriction Policy Name**: Enter the name of request restriction policy 
    - **Request Restriction Key Type**: Select the location of the request restriction key value to which the request restriction policy applies.
        - Path variable: Select a path variable to set the request restriction policy according to the value of the path variable in the requested path.
        - Request header: Select a request header to set a request restriction policy according to the value of specific request header.
    - **Request Restriction Key**: Enter the request restriction key according to the request restriction key type.
        - When request restriction key type is a path variable: Enter the name for the path variable. For example, when you set the request restriction policy for the path variable {memberId} in resource path {memberId}, type memberId.
        - When request restriction key type is a request header: Enter the header name where the restriction key value is located. 
    - **Requests per second by default**: When a request restriction policy is not set for the request restriction key value, set the request per second restriction to be applied by default  
        - If you do not enter it, you do not apply the request count restriction for the key values of unregistered request restriction.
        - You can set it from 1 to 5000. 
    - **Response Remaining Token Count**: When the request restriction is set, the number of remaining tokens that can be requested is passed to the 'X-NHN-RateLimit-Remaining' response header.

> **[Note] Limit the number of request restriction policies created**
> Request restriction policies can be created up to **10** per API Gateway service.


### Apply request restriction policy to Stage Resources 
1. Select a stage on **Stage** tab.
2. Select **Settings** tab.
3. On Stage Tree screen, select a path or method you want to apply request restriction policy.
4. **Enables (On)** request restriction policy.
5. Select request restriction policy to apply and click on **Modify** button.
6. Click on the **Deploy Stage** button. When the stage deployment is complete, the set request restriction policy works.

### Modify request restriction policy 
Allows you to modify the name of the request restriction policy, the default number of request restrictions per second, and the number of remaining tokens. 
The request restriction key type and request restriction key cannot be modified. 

1. From the list of request restriction, select the request restriction policy that you want to modify. 
2. Click on **Modify Request Restriction Policy**.
3. Modify the request restriction policy information and click on **Modify** button.

### Delete request restriction policy
1. From the list of request restriction, select the request restriction policy that you want to modify. 
2. Click on **Delete Request Restriction Policy**.
3. Click on **Confirm** button when the confirmation window appears. Deleted data cannot be recovered.

> **[Note] request restriction policy cannot be deleted** 
> When the request restriction policy to delete is set on the stage or is included in the deployed stage, it cannot be deleted. 
> To delete, delete the request restriction policy set on the stage, deploy the stage and then delete it.

### Create request restriction key value
Create key value of request restriction policy Depending on the restriction key value, you can set different IP ACLs and request count limits. 
1. Select the request restriction policy to which you want to add the request restriction key value. 
2. On the bottom tab, click on the **Create Request Restriction Key Value** button. 
3.  Enter the information of request restriction key value. 
    - **Request Restriction Key Value**: Enter a request restriction key value. Allows you to set IP ACLs and request count limits for each request restriction key value. 
    - **Requests Per Second**: Enter the request restriction value per second for the request restriction key value. 
        - If not entered, it is limited to the default number of requests per second value set in the request restriction policy. 
    - **IP Access Control Type**:- Allow: Allows you to access only to the specified IP and denies all remaining IPs. (Whitelist method) 
        - Reject: Allows access only to the specified IP and allows all remaining IPs. (Blacklist method) 
    - **IP Access Destination**: 
        - You can easily register an IP list by selecting either single entry or bulk entry method. 
        - IP access destinations can be entered as a single IP or CIDR for IPv4. 
            - Single IP example: 10.0.0.1 
            - CIDR example: 10.0.0.1/24 
        - IP ACL access control does not work unless you enter any IP access destinations.

### Modify request restriction key value 
Modify the request restriction per second, IP access control type, and IP access destination. Cannot modify request restriction key value 

1. On the bottom tab of request restriction policy, select a **request restriction key value** row to modify. 
2. Click **Modify Request Restriction Key Value** button.
3. Modify request restriction key value and click **Modify** button.

### Delete request restriction key value  
1. From the request restriction key value list, select the request restriction key value to delete. 
2. Click on **Delete Request Restriction Key Value** button
3. Click on **Confirm** button when the confirmation window appears. Deleted data cannot be recovered.

## Check API Call

1. With the Setup tab within the Stage tab, select the Stage Tree method.
2. See the Stage URL on the right.
3. Call the API with the HTTP method where the Stage URL is specified. 
    - Example: 
        - Method: GET
        - Stage URL: https://kr1-xxxxx-test.api.nhncloudservice.com/example
        - `curl --request GET 'https://kr1-xxxxx-test.api.nhncloudservice.com/example'`
    ```

> **[Caution] Stage deployment** 
> To call the API, there must be a deployed stage with the status: Successfully Deployed. 

> **[Note] If the API is not called properly**
> - If 404 NotFound HTTP status code is returned: 
>    1. See if the stage deployment status is Deployed.
>    2. See if the request method and stage URL/path are correct.
>    3. In the backend *endpoint* service, see if there is a request URL regarding the backend endpoint URL path. 
> - As for other error codes, see [Gateway Error Code](./error-code/) documentation. 


> **[Caution] API Call constraints**
> - In the Gateway client, the request size with the API Gateway is restricted to **max. 10MB.** This value cannot be adjusted.
> - In the API Gateway, the response size of the Gateway client is **max. 10MB.** This value cannot be adjusted. 
> - Response timeout for the request is **max. 60 seconds.** If there is a response delay in the backend endpoint service, a timeout may occur.


> **[Caution] API Gateway request ban policy**
> - If the endpoint service does not respond or continues to cause delayed response (over 60 sec) as a way of protecting the API Gateway Services and backend endpoint service, the request relating to the backend endpoint service is temporarily denied.
> - It is not banned by the internal errors (4xx, 5xx, etc.) of the backend endpoint service.
> - It is not recommended to link the backend endpoint service if it is not properly operable or if the delayed response (timeout) persists for over 60 seconds.


## API Document
You can use the API document to manage the specification of the API registered in API Gateway as a web page document.

### Publish API document
Here is the process of publishing API documentation.

1. Click **Model** tab from the resource setting page to request and register the model of the body.
2. Select the resource method from the resource setting page and enter the request parameters and response.
3. Click **Apply stage resource** to apply the changed resource details to the stage.
4. Click **Deploy stage** button of the stage setting page. 
5. Click **API document tab** of the stage setting page.
6. Select the publish type of the API document.
    - **Publish type**: You can set access restrictions for the API document.
        - **Public**: Access to the API document is allowed without access restrictions.
        - **Private**: Only users who are accessible to console can access the API document.
7. The API document is available at the URL that appears in the **Publish link**.  

> **[Note] Stage deployment and API document publishing**
> - An API document is published after the initial stage deployment, with the initial publishing type set to Private.
> - The API document is updated to the configuration deployed when a stage deployment is performed.
>
> **[Caution] CORS setting when testing API calls from a published API document**
> - Since the domain address of the published API document and the domain address of the calling API are different, CORS setting might be necessary to test your calls within the API document.
- Example:
  Access-Control-Allow-Origin: https://kr1-docs-apigw.api.nhncloudservice.com
  Access-Control-Allow-Method: GET, POST, DELETE, PUT, PATCH, HEAD, OPTIONS
  Access-Control-Allow-Headers: Authorization, x-nhn-apikey, x-nhn-date
>

## Dashboard 

Check the API statistical indexes by API Gateway Service and API key using the dashboard.  

### Stage Tab  

1. Go to the **Dashboard** tab. 
2. Move to the **Stage** tab.    
3. Select the API Gateway Service to view the statistics. 
3. From the list, select the stage to views statistics. 
4. In the **Stage Statistics** tab at the bottom, there are statistical indexes for the stage. 
5. In the **Resources Statistics** tab at the bottom, there are statistical indexes for each HTTP method and path.  

### Note on Statistical Data

- **Max. Search Period**
    - Only statistical data for the last 90 days can be viewed.
- **Statistical Data Generation Cycle**
    - Statistical data of all time-unit(1 min./10 min./1 hr./1 day) is renewed every minute. 
    - The generation of statistical data can be delayed depending on the size of the data.

### Stage Statistics

- **Graph Display Standard**
    - The units of the statistics are displayed as the following depending on the search period.
        - Less than 1 hour: unit of 1 minute
        - Longer than 1 hour - less than 1 day: unit of 10 minutes
        - Longer than 1 day - less than 1 week: unit of 1 hour
        - Longer than 1 week: unit of 1 day
- **Statistical Graph**
    - Number of successful API calls: Number of API calls with the responded HTTP status code of 2XX, 3XX 
    - Number of failed API calls: Number of API calls with the responded HTTP status code of 4XX, 5XX 
    - Average response time (ms): The average time spent from the point where the request entered the API Gateway to the point where the response was given to the API request client
    - Network outbound traffic: The byte size of the data responded with the API request client at the API Gateway

### Resource Statistics 
You can see more detailed statistical indexes categorized by resource path and HTTP method. 

- **HTTP method**: Requested HTTP method
- **Path**: Resource path mapped with the request 
- **Number of successful API calls**: Number of API calls with the responded HTTP status code of 2XX, 3XX 
- **Number of failed API calls**: Number of API calls with the responded HTTP status code of 4XX, 5XX
- **HTTP 2XX~5XX code**: Number of API calls by status code group
- **Number of immediate responses at the API Gateway**: Number of API calls responded at the API Gateway without passing the request to the backend endpoint service 
- **Average response time (ms)**: The average time spent from the point where the request entered the API Gateway to the point where the response was given to the API request client
- **Network outbound traffic**: The byte size of the data responded with the API request client at the API Gateway

### API Key Statistics
The number of calls can be checked for each API key on a daily graph

1. Go to the **Dashboard** tab.
2. Go to the **API Key** tab.
3. Select the API Key to view the statistics.
    - **Graph Display Standard**
        - The search period can be set in units of day(s) and displayed in units of day(s).
    - **Statistical Graph**
        - **API Call Count**: The count of all API calls where the API key was used
        - **Count of immediate responses at the API Gateway**: Number of API calls responded at the API Gateway without passing API Gateway plugins or usage limit

## Usage Plan
Limit the ability to request stage APIs only by API key connected to the stage of the usage plan, the same usage limit can be applied to each connected API key in the usage control settings.

- The following process is needed to apply the usage plan in the API Gateway service.
- `Create Usage Plan -> Connect Stage to Usage Plan -> Connect API Key to Stage Connected to Usage Plan -> Enable API Key in Stage Settings`
- See below for details on creating a usage plan and connecting stage and API key.

### Create Usage Plan
1. Click the **Create Usage Plan** button in the usage plan list.
2. Enter the usage plan information and click **Create**.
    - **Name of Usage Plan**: The name of usage plan.
    - **Description of Usage Plan**: The description of usage plan. (Optional)
    - **Requests per Second**: Enter the maximum number of requests that can be called in seconds.(Optional)
    - **Quota Period Unit**: Enter the maximum number of requests per day/month. (Optional)
    - **Request Quota**: Set the quota period unit to enter the maximum number of requests during the specified quota period.

> **[Note] Reset request quota limits**
> The request quota resets on the 1st of each month(monthly) and every day (daily) at UTC 00:00:00.

### Edit Usage Plan
1. Select the usage plan to be edited in the usage plan list.
2. Click the **Edit** button.
3. Edit the usage plan information
4. After changing the settings, click the **Edit** button.

> **[Caution] Edit usage plan request control settings**
> When editing the limited requests per second and request quota in the usage plan, it will be reflected in the connected API without a separate process.
> If you modify the quota period unit to “day” or “month,” the usage of the connected API Key request quota is maintained. If the request quota limit is lowered, the usage may be exceeded.
> If the quota period unit is modified to “None,” the requested quota usage of the associated API keys is initialized.



### Delete Usage Plan
1. Select the usage plan to delete in the usage plan list.
2. Click the **Delete** button and the Confirm Delete window will be displayed.
3. When the confirmation window appears, click the **OK** button. Deleted data cannot be restored.

> **[Note] Usage plan cannot be deleted when connected to a stage**
> Usage plan can be deleted after disconnecting all stages that are connected to the usage plan.

### Connect Stage to Usage Plan
Connect a stage to the usage plan to define which stages the API key can request.

1. Click the **Name** link in the Usage Plan Name column in the usage plan list.
2. Click the **Connect Stage** button.
3. Click the **OK** button after selecting the API Gateway service and stage.

> **[Note] Already connected stage**
> The already connected stage is not included in the selection list.

### Disable Stage Connected to the Usage Plan
1. Click the **Name** link in the Usage Plan Name column in the usage plan list.
2. Select the stage in the Connected Stage list to disconnect.
3. Click the **Disconnect Stage** button.
4. Click the **OK** button when the confirmation window appears.

> **[Note] If there is an API key connected, stage cannot be disabled**
> In order to disable the stage connected to the usage plan, all API keys connected to the stage must be disabled.

### Connect API Key
Connect the API key to call the API of a stage connected to the usage plan.

1. Click the **Name** link in the Usage Plan Name column in the usage plan list.
2. Select the stage in the Connected Stage list to connect to the API key.
3. Click the **Connect API Key** button at the bottom
4. After selecting the API key to be added, click the **OK** button.

> **[Note]** API keys connected to the same stage of different usage plans do not appear in the selection list and cannot be connected.

### Disconnect API Key
1. Click the **Name** link in the Usage Plan Name column in the usage plan list.
2. From the Connected Stage list, select the stage to disconnect the API Key.
3. After selecting the API key to disconnect from the bottom list, click the **Disconnect API Key** button.
4. Click the **OK** button when the confirmation window appears.

### Change the Usage Plan of API Key
1. Click the **Name** link in the Usage Plan Name column in the usage plan list.
2. Select the stage that has the API key with the usage plan to be changed in the Connected Stage.
3. After selecting the API key with the usage plan to be changed from the bottom list, click the **Change Usage Plan** button.
4. Click the **OK** button after selecting the usage plan to be changed.
   
> **[Note]** The selected stage can only be changed to a different usage plan than it is connected to.


> **[Caution]** Initialize usage of API Key request quota when changing the usage plan
> If the quota period unit is changed to a “daily” or “monthly” usage plan, the requested quota usage of the associated API Key remains. The usage may be exceeded if changed to the usage plan with a low request quota limit.
> If changing to the usage plan with a quota period unit of “None,” the requested quota usage of the associated API keys is initialized.


## API Key
- API key manages the string values for API gateway service API access that is connected to the usage plan and stage.
- When requesting API, primary API key and secondary API key can be used as API key value.

### Create API Key
1. Click the **Create Usage Plan** button in the API key list.
2. Enter the API key information and click the **Create** button.
    - **Name of API Key**: The name of the API key.
    - **Description of API Key**: The description of API key. (Optional)
    - **Status of API Key**: Select the status of API key.
        - ACTIVE: API key is active and can be used.
        - INACTIVE: API key is inactive and cannot be used.
        - **Primary API Key**: When selected user customization, it is generated by directly entering the Primary Key value. When not selected, it is automatically generated as an arbitrary string.
        - **Secondary API Key**: When selected user customization, it is generated by directly entering the Secondary Key value. When not selected, it is automatically generated as an arbitrary string.
> **[Caution]** Custom Primary/Secondary API Key 
> For custom Primary/Secondary API Key, it is generated with a string of at least 10 alphanumeric characters and numbers. 
> Must be unique across API Gateway services. 
> It is recommended to make the keys complicated and not to be exposed.

### Export API Key 
Export a registered API Key in CSV format file. 

1. On the API Key list page, click on **Export** button. 
2. Download CSV file.

> [Note] Only API Keys that are queried in API Key list are exported to a file.

### Import API Key
Import API keys with CSV format file.

1. On API Key list page, click **Import** button and then click on **Select File** button to select CSV file to import. 
2. A list of API keys registered based on CSV files is displayed on the screen. 
    - If the imported data includes some parts to be modified, the data cannot be imported. 
3.  Click on **Import** button. 

> **[Note]** Import failed when API Key is duplicated  
> All API keys Importing fails if duplicate Primary API Key and Secondary API Key exists. Please modify the duplicate API key and import it again. 

### Edit API Key
1. Select the API key to edit in the API key list.
2. Click the **Edit** button.
3. Edit the API key. Items that can be edited are Name of API Key, Description of API Key, and Status of API Key.
4. After changing the settings, click the **Edit** button.

> **[Caution] Edit status of API key**
> If the status of API key is changed to INACTIVE, the API key cannot be used.

### Delete API Key
1. Select the API key to be deleted from the API key list.
2. Click the **Delete** button and the Confirm Delete window will be displayed.
3. When the confirmation window appears, click the **OK** button. Deleted data cannot be restored.

> **[Note] If there are connected usage plan and stage, it cannot be deleted**
> The API key cannot be deleted if there are connected usage plan and stage.

### Regenerate API Key
When requesting API, primary API key and secondary API key that are used as API key value can be regenerated.

1. Select the API key in the API key list.
2. Go to the **API Key** tab at the bottom.
3. Click the **Regenerate** button next to the primary API key and secondary API key list and the confirmation window will be displayed.
4. Click the **OK** button when the confirmation window appears.
    - If you selected Custom, enter your own API Key value to reissue. If not selected, it will be automatically reissued as a random string.
    - The existing API key value is no longer valid when regenerated.
    

### Stage Connected to API Key
1. Select the API key in the API key list.
2. Go to the **Connected Stage** tab at the bottom.
3. The list of connected stage can be checked.
    - **Stage URL**: The stage URL is connected.
    - **Usage Plan**: The usage plan information is connected.

## Custom domain
Default stage domain is randomly issued in {Region}-{ServiceId}-{StageName}.api.nhncloudservice.com format.  
Instead of domains randomly issued as custom domains, users can create domains in {CustomDomainPrefix}.capi.nhncloudservice.com format by specifying the domain's prefix. 

### Create custom domain 
1. Go to **Custom Domain**
2. Click **Create Custom Domain**.
3. Custom domain: Enter the prefix of domain that you want to create in custom domain. The entered value is specified in {CustomDomainPrefix} part of {CustomDomainPrefix}.capi.nhncloudservice.com domain.
4. GSLB Domain: Enter the GSLB domain to configure API Gateway region redundancy. For more information about API Gateway Region Redundancy Guide, see [API Gateway Region Redundancy Guide](./console-guide/#api-gateway-region-redundancy). 
5. Click **Create** button to create a custom domain in {CustomDomainPrefix}.capi.nhncloudservice.com format. 

> **[Note]**Custom domain 
> Custom domain is to be created with strings of at least 2 characters, up to 50 alphanumeric characters, numbers and - characters. 
> Must be unique across API Gateway services. 

### Delete custom domain 

1. Go to **Custom Domain**
2. Select custom domain to delete 
2. Click on **Delete Custom Domain** button.
3. If clicking on the **Delete** button, confirmation window for deletion is to be displayed. 
4. Click on **Confirm** button when the confirmation window appears. Deleted data cannot be recovered.

> **[Note]** Unable to delete custom domain 
> Custom domains connected to stage cannot be deleted. 
> Please disconnect custom domain in stage and then delete. 

### Connect stage of custom domain
1. Go to stage to connect with custom domain
2. Go to stage tab>custom domain tab 
3. Click on **Connect with Stage** button in the custom domain you want to connect to. 

### Disconnect stage from a custom domain
1. Go to the stage where you want to disconnect the custom domain.
2. Go to stage tab>custom domain tab 
3. Click on **Disconnect from Stage** button in the custom domain that you want to disconnect. 

> **[Note]** When disconnecting a stage, API cannot be called to a custom domain. 
> When you disconnect a stage of custom domain, the stage API can no longer be called to the custom domain. 
> Please make sure that there are no clients calling the API using the custom domain and then disconnect. 

## API Gateway region redundancy 
If the region where the API Gateway is located fails, the API Gateway for that region may not operate normally.  
To operate API Gateway service without the impact of a specific region failure, you can avoid it by configuring the API Gateway for multiple regions with redundancy.  
The following is a scenario in which API Gateway is newly configured in the existing Pangyo Region and the API Gateway is configured in Pyeongchon Region to redundancy the Region. 

### 1. Service and Create stage in Pyeongchon Region 
1. Create API Gateway service in Pyeongchon region.
2. Registers the same resources as the Pangyo Region Stage in operation with the API Gateway service in Pyeongchon Region.  
In order to transfer easily, download the resources registered on the stage through [Stage > Import Resource](./console-guide/#import-resource_1) as Swagger file, then you can register a resource with the downloaded Swagger file through [Resource > Import Resource](./console-guide/#import-resource). 
3. Create a stage for Pyeongchon region and if there is a stage setting required, modify and deploy the stage. 

> [Note] Resources > Stage plug-in settings when importing resources. 
> When importing resources with Swagger file, do not import the plug-ins set on stage. Please add the necessary plug-ins separately in stage setting.

### 2. Create GSLB 
This guide uses the GSLB of NHN Cloud DNS Plus service. For more information on setting up GSLB, refer to [DNS Plus Console Usage Guide](https://docs.nhncloud.com/en/Network/DNS%20Plus/en/console-guide/).

1. Go to DNS Plus service
2. Create GSLB 
3. Create health check. 
    * For Health check path, registered health check resource path by configuring resource method to use for health check in API Gateway in Pangyo and Pyeongchon regions.
    * A pool that failed health check is excluded from service.
4. Create Pool 
    * For health check in Create Pool, select the health check that you created above. 
    * For endpoint address, enter API Gateway stage domain for Pangyo and Pyeongchon regions. 
    * For weights and states, set according to redundancy structure (Active, Active-StandBy) that you want to configure. 
5. Check whether or not the status of the pool connected with the GSLB is ACTIVE. 

### 3.  Create custom domain 
1. Create a custom domain to be used in Pangyo and Pyeongchon Region when calling Stage API. You have to create a custom domain for each region, and have to create it with the same custom domain. 
2. When creating a custom domain, enter the GSLB domain that you created in GSLB domain  

### 4. Connect custom domain to stages in each region
1. Connect the custom domains you created to each API Gateway stage in Pangyo and Pyeongchon Region. For more information, refer to [Guide to connect Custom Domain with stage](./console-guide/#connect-stage-of-custom-domain).
2. Check whether or not the API is successfully called to the custom domain and that traffic is distributed according to GSLB configuration. 