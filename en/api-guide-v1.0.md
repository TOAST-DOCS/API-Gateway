## Application Service > API Gateway > API v1.0 Guide

This guide describes Public API v1.0 provided by NHN Cloud API Gateway.

## API Common Information

### Domain

| Name      | Region | Domain                                            |
|---------|-----|------------------------------------------------|
| API domain | Korea (Pangyo) | https://kr1-apigateway.api.nhncloudservice.com |
| API domain | Korea (Pyeongchon) | https://kr2-apigateway.api.nhncloudservice.com |

### Prerequisites

To use the API, you need an Appkey.
You can find your Appkey in the **URL & Appkey** menu at the top right of the console.

### Request Common Information

#### Path Parameter

All APIs must specify the appkey as a path parameter.
* Example) /v1.0/appkeys/**{appKey}**/**

| Name     | Description                    |
| ------ | --------------------- |
| appKey | Appkey issued from the console |

### Response Common Information

#### Header
The service responds with **200 OK** to all API requests. For detailed response results, refer to the header of the response body as in the following example.

[Success: Response Body]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

| Field | Type | Description |
| --- | --- | --- |
| header               | Object  | Header area  |
| header.isSuccessful  | Boolean | Successful or not  |
| header.resultCode    | Integer | Result code  |
| header.resultMessage | String  | Result message |

[Failure: Response Body]

```json
{
  "header": {
    "isSuccessful": false,
    "resultCode": 400,
    "resultMessage": "Bad Request"
  },
  "errorList": [
    {
      "resultCode": 400,
      "errorProperty": "postApigwServiceRequest",
      "errorField": "apigwServiceName",
      "errorMessage": "Cannot be empty."
    }
  ]
}
```

| Field | Type | Description |
| --- | --- | --- |
| errorList            | List  | Error list area  |
| errorList[0].resultCode  | Integer | Error Code  |
| errorList[0].errorProperty | String | Error property (model) |
| errorList[0].errorField | String  | Error details field |
| errorList[0].errorMessage | String  | Error Message |

* If an invalid API request is made, detailed error reason and field information is responded in the errorList field.


## API Gateway Service

### List API Gateway Services 
- Retrieves the list of API Gateway services.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | Required | N/A | KR1, KR2 | See [API Gateway Region Enum Code](./enum-code/#api-gateway-region) |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

#### Response

[Response]

```json
{
   "header":{
      "isSuccessful":true,
      "resultCode":0,
      "resultMessage":"SUCCESS"
   },
   "paging":{
      "limit":10,
      "page":1,
      "totalCount":100
   },
   "apigwServiceList":[
      {
         "apigwServiceId":"{apigwServiceId}",
         "apigwServiceAlias":"{apigwServiceAlias}",
         "apigwServiceName":"test api gateway",
         "apigwServiceDescription":"description of test api gateway service",
         "apigwDomain":"api.nhncloudservice.com",
         "appKey":"{appKey}",
         "regionCode":"KR1",
         "serverGroupId":"{serverGroupId}",
         "dedicatedId":null,
         "createdAt":"2021-10-19T07:25:23.000Z",
         "updatedAt":"2021-10-19T07:25:23.000Z",
         "apigwServiceTypeCode":"SHARED"
      }
   ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | Paging area                                        |
|paging.page                          |Integer | Current page                                        |
|paging.limit                         |Integer | Count per page                                  |
|paging.totalCount                    |Integer | Total count                                        |
|apigwServiceList                     |List    | API Gateway service list area                         |
|apigwServiceList[0].apigwDomain         |String  | API Gateway service domain                  |
|apigwServiceList[0].apigwServiceAlias   |String  | API Gateway service alias               |
|apigwServiceList[0].apigwServiceId      |String  | API Gateway service ID                  |
|apigwServiceList[0].apigwServiceTypeCode|Enum    | See [API Gateway Service Type Enum Code](./enum-code/#api-gateway-service-type)|
|apigwServiceList[0].appKey              |String  | AppKey                                        |
|apigwServiceList[0].dedicatedId         |String  | ID of the dedicated API Gateway service                        |
|apigwServiceList[0].apigwServiceDescription         |String  | API Gateway service alias                                        |
|apigwServiceList[0].apigwServiceName                |String  | API Gateway service name                                        |
|apigwServiceList[0].regionCode          |Enum    | See [API Gateway Region Enum Code](./enum-code/#api-gateway-region) |
|apigwServiceList[0].serverGroupId       |String  | ID of the server group to which the API Gateway service belongs                              |
|apigwServiceList[0].createdAt           |DateTime| API Gateway service creation date and time                                      |
|apigwServiceList[0].updatedAt           |DateTime| API Gateway service modification date and time                                      |


### Get API Gateway Service 
- Retrieves a single API Gateway service with API Gateway service ID.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:28:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object  | API Gateway service area                         |
|apigwService.apigwDomain         |String  | API Gateway service domain                  |
|apigwService.apigwServiceAlias   |String  | API Gateway service alias                            |
|apigwService.apigwServiceId      |String  | API Gateway service ID                            |
|apigwService.apigwServiceTypeCode|Enum    | See [API Gateway Service Type Enum Code](./enum-code/#api-gateway-service-type) |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | ID of the dedicated API Gateway service                        |
|apigwService.apigwServiceDescription         |String  | API Gateway service alias                                        |
|apigwService.apigwServiceName                |String  | API Gateway service name                                        |
|apigwService.regionCode          |Enum    |See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)|
|apigwService.serverGroupId       |String  | ID of the server group to which the API Gateway service belongs                              |
|apigwService.createdAt           |DateTime| API Gateway service creation date and time                                      |
|apigwService.updatedAt           |DateTime| API Gateway service modification date and time                                      |



### Create API Gateway Service
- Creates an API Gateway service.
- You can choose the region where the API Gateway server will be created. Currently, only the Korea (Pangyo) region is supported.
- When you create an API Gateway service, an API Gateway service ID is automatically issued.


#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services |

[Request Body]

```json
{
  "regionCode": "KR1",
  "apigwServiceName": "service name",
  "apigwServiceDescription": "service description"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| regionCode | Enum | Required | N/A | KR1, KR2 | See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)|
| apigwServiceName | String | Required | N/A | Max. 50 characters  | API Gateway service name |
| apigwServiceDescription | String | Optional | N/A | Max. 200 characters  | API Gateway service alias |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:28:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    | API Gateway service area                         |
|apigwService.apigwDomain         |String  | API Gateway service domain                  |
|apigwService.apigwServiceAlias   |String  | API Gateway service alias                            |
|apigwService.apigwServiceId      |String  | API Gateway service ID                            |
|apigwService.apigwServiceTypeCode|Enum    | See [API Gateway Service Type Enum Code](./enum-code/#api-gateway-service-type) |
|apigwService.appKey              |String  | AppKey                                        |
|apigwService.dedicatedId         |String  | ID of the dedicated API Gateway service                        |
|apigwService.apigwServiceDescription         |String  | Service description                                        |
|apigwService.apigwServiceName    |String  | API Gateway service name                                        |
|apigwService.regionCode          |Enum    | See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)|
|apigwService.serverGroupId       |String  | ID of the server group to which the API Gateway service belongs                              |
|apigwService.createdAt           |DateTime| API Gateway service creation date and time                                      |
|apigwService.updatedAt           |DateTime| API Gateway service modification date and time                                      |


### Modify API Gateway Service
- Modifies the name and description of an API Gateway service.

#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| PUT  | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |


[Request Body]

```json
{
  "apigwServiceName": "update service name",
  "apigwServiceDescription": "test of api gateway service"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceName | String | Required | N/A | Max. 50 characters  | API Gateway service name |
| apigwServiceDescription | String | Optional | N/A | Max. 200 characters  | API Gateway service alias |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apigwService": {
    "apigwServiceId": "{apigwServiceId}",
    "apigwServiceAlias": "{apigwServiceAlias}",
    "apigwServiceName": "test api gateway",
    "apigwServiceDescription": "description of test api gateway",
    "apigwDomain": "api.nhncloudservice.com",
    "appKey": "{appKey}",
    "regionCode": "KR1",
    "serverGroupId": "{serverGroupId}",
    "dedicatedId": null,
    "createdAt": "2021-10-19T07:28:44.946Z",
    "updatedAt": "2021-10-19T07:50:44.946Z",
    "apigwServiceTypeCode": "SHARED"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|apigwService                     |Object    |API Gateway service area                         |
|apigwService.apigwDomain         |String  |API Gateway service domain                  |
|apigwService.apigwServiceAlias   |String  |API Gateway service alias                            |
|apigwService.apigwServiceId      |String  |API Gateway service ID                            |
|apigwService.apigwServiceTypeCode|Enum    |See [API Gateway Service Type Enum Code](./enum-code/#api-gateway-service-type)|
|apigwService.appKey              |String  |AppKey                                        |
|apigwService.dedicatedId         |String  |ID of the dedicated API Gateway service                        |
|apigwService.apigwServiceDescription         |String  |Service description                                        |
|apigwService.apigwServiceName                |String  |Service name                                        |
|apigwService.regionCode          |Enum    |See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)|
|apigwService.serverGroupId       |String  |ID of the server group to which the service belongs                              |
|apigwService.createdAt           |DateTime|Service creation date and time                                      |
|apigwService.updatedAt           |DateTime|Service modification date and time                                      |

### Delete API Gateway Service
- Deletes an API Gateway Service.  
- Deleting the API Gateway service deletes all stages.  
- If the stage of the API Gateway service you want to delete is associated with a usage plan, the service cannot be deleted. To delete the service, disassociate all stages associated with the usage plan and then delete it.
- Please note that deleted API Gateway services cannot be recovered.

#### Request

[URI]

| Method    | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |

#### Response

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

## Resource

### List Resources

- Retrieves a list of resources.

#### Request

[URI]

| Method | URI | 
| --- | --- | 
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "15ea79f5-a0fc-4f78-a498-c7c49898dcb4",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-10-25T05:05:23.000Z",
      "updatedAt": "2021-10-25T05:05:23.000Z",
      "resourcePluginList": []
    },
    {
      "resourceId": "f7906669-687b-423a-9101-6f86f2777d2f",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/path",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-10-25T05:06:10.000Z",
      "updatedAt": "2021-10-25T05:06:10.000Z",
      "resourcePluginList": []
    },
    {
      "resourceId": "cd66701a-e2a8-47d2-b3cb-245a6d8e0145",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/path",
      "methodType": "GET",
      "methodName": "example",
      "methodDescription": "This is a method description",
      "createdAt": "2021-10-25T05:06:10.000Z",
      "updatedAt": "2021-10-25T05:06:10.000Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "847efa44-f405-4b43-824b-95ec1a146ac4",
          "resourceId": "cd66701a-e2a8-47d2-b3cb-245a6d8e0145",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/path",
            "backendEndpointPath": "/anything"
          },
          "createdAt": "2021-10-25T05:06:10.000Z",
          "updatedAt": "2021-10-25T05:06:10.000Z"
        }
      ]
    }
  ]
}
```

| Field                                                     | Type       | Description                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | Resource list area                                      |
| resourceList[0].resourceId                             | String   | Resource ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway service ID                             |
| resourceList[0].path                                   | String   | Resource path                                         |
| resourceList[0].createdAt                              | DateTime | Resource creation date and time                                       |
| resourceList[0].updatedAt                              | DateTime | Resource modification date and time                                       |
| resourceList[2].methodType                             | Enum     | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourceList[2].methodName                             | String   | Method resource name                                     |
| resourceList[2].methodDescription                      | String   | Method resource description                                     |
| resourceList[2].resourcePluginList                     | List     | Resource plugin list area                                 |
| resourceList[2].resourcePluginList[0].resourcePluginId | String   | Resource plugin ID                                    |
| resourceList[2].resourcePluginList[0].resourceId       | String   | Resource ID                                         |
| resourceList[2].resourcePluginList[0].pluginType       | Enum     | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type)    |
| resourceList[2].resourcePluginList[0].pluginConfigJson | Object   | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)                   |
| resourceList[2].resourcePluginList[0].createdAt        | DateTime | Resource plugin creation date and time                                  |
| resourceList[2].resourcePluginList[0].updatedAt        | DateTime | Resource plugin modification date and time                                  |

### Create Resource Paths and Methods
- You can create multiple resource paths and methods, and set the plugin at the time of creation.
- Resource methods are optional input. To add a method under the created resource path, you need to use the [Create Resource Methods API](./api-guide-v1.0/#create-resource-methods).
- Resource methods must have either HTTP or MOCK plugin set. HTTP and MOCK plugins cannot be set at the same time.
- The created resource path cannot be modified.
- The resource path plugins defined in the pathPluginList field are the list of plugins that are applied to child methods of that path.

#### Request

[URI]

| Method | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |


[Request Body]

```json
{
   "resourcePathList":[
      {
         "path":"/members/{memberId}",
         "pathPluginList":[
            {
               "pluginConfigJson":{
                  "allowedMethods":[
                     "GET",
                     "POST",
                     "DELETE",
                     "PUT",
                     "OPTIONS",
                     "HEAD",
                     "PATCH"
                  ],
                  "allowedHeaders":[
                     "*"
                  ],
                  "allowedOrigins":[
                     "*"
                  ],
                  "exposedHeaders":[

                  ],
                  "maxCredentialsAge":null,
                  "allowCredentials":false
               },
               "pluginType":"CORS"
            }
         ],
         "methodList":[
            {
               "methodDescription":"Edit a member information",
               "methodName":"PutMember",
               "methodPluginList":[
                  {
                     "pluginConfigJson":{
                        "frontendEndpointPath":"/members/{memberId}",
                        "backendEndpointPath":"/api/v1/members/${request.path.memberId}"
                     },
                     "pluginType":"HTTP"
                  }
               ],
               "methodType":"PUT"
            },
            {
               "methodDescription":"Query a member",
               "methodName":"GetMember",
               "methodPluginList":[
                  {
                     "pluginConfigJson":{
                        "frontendEndpointPath":"/members/{memberId}",
                        "backendEndpointPath":"/api/v1/members/${request.path.memberId}"
                     },
                     "pluginType":"HTTP"
                  },
                  {
                     "pluginConfigJson":{
                        "parameters":{
                           "id":"${request.path.memberId}"
                        }
                     },
                     "pluginType":"ADD_REQUEST_QUERY_PARAMETER"
                  }
               ],
               "methodType":"GET"
            }
         ]
      }
   ]
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| resourcePathList | List | Required | N/A | N/A  | Resource path list |
| resourcePathList[0] | Object | Required | N/A | N/A  | Resource path area |
| resourcePathList[0].path | Object | Required | N/A | A valid path consisting of alphanumeric characters, path variables, and limited characters (. + - /)  | Resource path |
| resourcePathList[0].pathPluginList | List | Optional | N/A | N/A | Resource path plugin list |
| resourcePathList[0].pathPluginList[0] | Object | Optional | N/A | N/A | Resource path plugin area |
| resourcePathList[0].pathPluginList[0].pluginType | Enum | Required | N/A | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | The plugin type that can be set in the resource path among [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type) |
| resourcePathList[0].pathPluginList[0].pluginConfigJson | Object | Required | N/A | N/A | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)|
| resourcePathList[0].methodList | List | Optional | N/A | N/A | List of methods under the resource path |
| resourcePathList[0].methodList[0] | Object | Optional | N/A | N/A | Area for methods under the resource path |
| resourcePathList[0].methodList[0].methodType | Enum | Required | N/A | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourcePathList[0].methodList[0].methodName | String | Required | N/A | Max. 50 characters | Method name |
| resourcePathList[0].methodList[0].methodDescription | String | Optional | N/A | Max. 200 characters | Method description |
| resourcePathList[0].methodList[0].methodPluginList | List | Required | N/A | N/A | Resource method plugin list |
| resourcePathList[0].methodList[0].methodPluginList[0] | Object | Required | N/A | N/A | Resource method plugin area, requires input of one of the 'HTTP' or 'MOCK' plugin |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginType | Enum | Required | N/A | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | The plugin type that can be set in the resource method among [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type) |
| resourcePathList[0].methodList[0].methodPluginList[0].pluginConfigJson | Object | Required | N/A | N/A | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)|

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.297Z",
      "updatedAt": "2021-12-23T23:55:11.297Z",
      "resourcePluginList": [],
      "parentPath": "/"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.298Z",
      "updatedAt": "2021-12-23T23:55:11.298Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.298Z",
          "updatedAt": "2021-12-23T23:55:11.298Z"
        }
      ],
      "parentPath": "/members"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "PUT",
      "methodName": "PostMember",
      "methodDescription": "Edit a member info",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "24bef5d0-feaf-4469-9619-a31e9e35a622",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId": "321d99cc-cb26-473e-ab76-84249a82b262",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "GET",
      "methodName": "GetMember",
      "methodDescription": "Query a member",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "ADD_REQUEST_QUERY_PARAMETER",
          "pluginConfigJson": {
            "parameters": {
              "id": "${request.path.memberId}"
            }
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    },
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "methodType": "OPTIONS",
      "methodName": "CORS",
      "methodDescription": null,
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "CORS",
          "pluginConfigJson": {
            "allowedMethods": [
              "GET",
              "POST",
              "DELETE",
              "PUT",
              "OPTIONS",
              "HEAD",
              "PATCH"
            ],
            "allowedHeaders": [
              "*"
            ],
            "allowedOrigins": [
              "*"
            ],
            "exposedHeaders": [],
            "maxCredentialsAge": null,
            "allowCredentials": false
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ],
      "parentPath": "/members/{memberId}"
    }
  ]
}
```

| Field                                                     | Type       | Description                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | Resource list area                                      |
| resourceList[1].resourceId                             | String   | Resource ID                                         |
| resourceList[1].apigwServiceId                         | String   | API Gateway service ID                             |
| resourceList[1].path                                   | String   | Resource path                                         |
| resourceList[1].parentPath                             | String   | Parent resource path                                         |
| resourceList[1].createdAt                              | DateTime | Resource creation date and time                                       |
| resourceList[1].updatedAt                              | DateTime | Resource modification date and time                                       |
| resourceList[1].methodType                             | Enum     | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourceList[1].methodName                             | String   | Method resource name                                     |
| resourceList[1].methodDescription                      | String   | Method resource description                                     |
| resourceList[1].resourcePluginList                     | List     | Resource plugin list area                                 |
| resourceList[1].resourcePluginList[0].resourcePluginId | String   | Resource plugin ID                                    |
| resourceList[1].resourcePluginList[0].resourceId       | String   | Resource ID                                         |
| resourceList[1].resourcePluginList[0].pluginType       | Enum     | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type)    |
| resourceList[1].resourcePluginList[0].pluginConfigJson | Object   | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)                   |
| resourceList[1].resourcePluginList[0].createdAt        | DateTime | Resource plugin creation date and time                                  |
| resourceList[1].resourcePluginList[0].updatedAt        | DateTime | Resource plugin modification date and time                                  |


### Create Resource Methods
- Creates resource methods under the created resource path.
- Resource methods must have either HTTP or MOCK plugin set. HTTP and MOCK plugins cannot be set at the same time.

#### Request

[URI]

| Method | URI | 
| --- | --- | 
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/methods |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId | String | Required    | N/A  | N/A    | Resource path ID |


[Request Body]

```json
{
  "methodList": [
    {
      "methodType": "DELETE",
      "methodName": "DeleteMember",
      "methodDescription": "Delete a member",
      "methodPluginList": [
        {
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          }
        }
      ]
    }
  ]
}   
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| methodList | List | Required | N/A | N/A | List of methods under the resource path |
| methodList[0] | Object | Required | N/A | N/A | Area for methods under the resource path |
| methodList[0].methodType | Enum | Required | N/A | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| methodList[0].methodName | String | Required | N/A | Max. 50 characters | Method name |
| methodList[0].methodDescription | String | Optional | N/A | Max. 200 characters | Method description |
| methodList[0].methodPluginList | List | Required | N/A | N/A | Resource method plugin list |
| methodList[0].methodPluginList[0] | Object | Required | N/A | N/A | Resource method plugin area, requires input of one of the 'HTTP' or 'MOCK' plugin |
| methodList[0].methodPluginList[0].pluginType | Enum | Required | N/A | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | The plugin type that can be set in the resource method among [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type) |
| methodList[0].methodPluginList[0].pluginConfigJson | Object | Required | N/A | N/A | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)|

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members/{memberId}",
      "methodType": "GET",
      "methodName": "GetMember",
      "methodDescription": "Query a member",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        },
        {
          "resourcePluginId":  "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "ADD_REQUEST_QUERY_PARAMETER",
          "pluginConfigJson": {
            "parameters": {
              "id": "${request.path.memberId}"
            }
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ]
    },
    ...
  ]
}
```

| Field                                                     | Type       | Description                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | Resource list area                                      |
| resourceList[0].resourceId                             | String   | Resource ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway service ID                             |
| resourceList[0].path                                   | String   | Resource path                                         |
| resourceList[0].parentPath                             | String   | Parent resource path                                         |
| resourceList[0].createdAt                              | DateTime | Resource creation date and time                                       |
| resourceList[0].updatedAt                              | DateTime | Resource modification date and time                                       |
| resourceList[0].methodType                             | Enum     | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourceList[0].methodName                             | String   | Method resource name                                     |
| resourceList[0].methodDescription                      | String   | Method resource description                                     |
| resourceList[0].resourcePluginList                     | List     | Resource plugin list area                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | Resource plugin ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | Resource ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type)    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | Resource plugin creation date and time                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | Resource plugin modification date and time                                  |


### Modify/Delete Resource Path Plugins
- Adds, modifies, or deletes resource path plugins.
- If you set a plugin that has not been added to the resource path, the plugin is added.
- If you set a plugin that has been added to the resource path, it is changed to the requested plugin setting.
- If the delete field is set to true, the plugin of the requested plugin type is deleted. If the delete field is true, the pluginConfigJson field does not need to be defined.
- If the applyChildPath field is set to true, the plugin is set on all paths and methods under the resource path.
- If both applyChildPath and delete fields are set to true, the plugin will be deleted for all paths and methods under the resource path.
- If the CORS plugin is set, the OPTIONS method is automatically created as a child method. Note that if there is an existing OPTIONS method, it will be deleted and replaced.
- Only the plugins that can be set in the resource path can be set. For more information, see [Resource Plugins](./api-guide-v1.0/#resource-plugin).

#### Request

[URI]

| Method | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-paths/{resourceId} |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId | String | Required    | N/A  | N/A    | Resource path ID |

[Request Body]

```json
{
  "pathPluginList":[
    {
      "applyChildPath": true,
      "delete": true,
      "pluginConfigJson":{
        "allowedMethods":[
            "GET",
            "POST",
            "DELETE",
            "PUT",
            "OPTIONS",
            "HEAD",
            "PATCH"
        ],
        "allowedHeaders":[
            "*"
        ],
        "allowedOrigins":[
            "*"
        ],
        "exposedHeaders":[

        ],
        "maxCredentialsAge":null,
        "allowCredentials":false
      },
      "pluginType":"CORS"
    }
  ]
}   
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pathPluginList | List | Optional | N/A | N/A | Resource path plugin list |
| pathPluginList[0] | Object | Optional | N/A | N/A | Resource path plugin area |
| pathPluginList[0].pluginType | Enum | Required | N/A | {pluginCode} CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER,ADD_REQUEST_QUERY_PARAMETER | The plugin type that can be set in the resource path among [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type) |
| pathPluginList[0].pluginConfigJson | Object | Conditionally required | N/A | N/A | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin), required input when the delete field is false.|
| pathPluginList[0].applyChildPath | Boolean | Optional | false | true, false | Whether to overwrite child paths and methods |
| pathPluginList[0].delete | Boolean | Optional | false | true, false | Whether to delete the plugin |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members",
      "methodType": "DELETE",
      "methodName": "DeleteMember",
      "methodDescription": "Delete a member",
      "createdAt": "2021-12-23T23:55:11.298Z",
      "updatedAt": "2021-12-23T23:55:11.298Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "{resourcePluginId}",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v1/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.298Z",
          "updatedAt": "2021-12-23T23:55:11.298Z"
        }
      ]
    }
    ...
  ]
}
```

| Field                                                     | Type       | Description                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | Resource list area                                      |
| resourceList[0].resourceId                             | String   | Resource ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway service ID                             |
| resourceList[0].path                                   | String   | Resource path                                         |
| resourceList[0].parentPath                             | String   | Parent resource path                                         |
| resourceList[0].createdAt                              | DateTime | Resource creation date and time                                       |
| resourceList[0].updatedAt                              | DateTime | Resource modification date and time                                       |
| resourceList[0].methodType                             | Enum     | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourceList[0].methodName                             | String   | Method resource name                                     |
| resourceList[0].methodDescription                      | String   | Method resource description                                     |
| resourceList[0].resourcePluginList                     | List     | Resource plugin list area                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | Resource plugin ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | Resource ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type)    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | Resource plugin creation date and time                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | Resource plugin modification date and time                                  |


### Modify/Delete Resource Method Information and Plugins
- You can modify the name and description of the resource method.
- Adds, modifies, or deletes resource method plugins.
- If you set a plugin that has not been added to the resource method, the plugin is added.
- If you set a plugin that has been added to the resource method, it is changed to the requested plugin setting.
- If the delete field is set to true, the plugin of the requested plugin type is deleted. If the delete field is true, the pluginConfigJson field does not need to be defined.
- Only the plugins that can be set on resource methods can be set. For more information, see [Resource Plugins](./api-guide-v1.0/#resource-plugin).

#### Request

[URI]

| Method | URI | 
| --- | --- | 
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resource-methods/{resourceId} |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId | String | Required    | N/A  | N/A    | Resource method ID |

[Request Body]

```json
{
  "methodName":"PutMember",
  "methodDescription":"Edit a member information",
  "methodPluginList":[
    {
        "pluginConfigJson":{
          "frontendEndpointPath":"/members/{memberId}",
          "backendEndpointPath":"/api/v2/members/${request.path.memberId}"
        },
        "pluginType":"HTTP"
    },
    {
      "delete": true,
      "pluginType": "ADD_REQUEST_QUERY_PARAMETER"
    }
  ]
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| methodName | String | Required | N/A | Max. 50 characters | Method name |
| methodDescription | String | Optional | N/A | Max. 200 characters | Method description |
| methodPluginList | List | Optional | N/A | N/A | Resource method plugin list |
| methodPluginList[0] | Object | Required | N/A | N/A | Resource method plugin area |
| methodPluginList[0].pluginType | Enum | Required | N/A | {pluginCode} HTTP, MOCK, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | The plugin type that can be set in the resource method among [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type) |
| methodPluginList[0].pluginConfigJson | Object | Conditionally required | N/A | N/A | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin), required input when the delete field is false.|
| methodPluginList[0].delete | Boolean | Optional | false | N/A | Whether to delete the plugin |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "resourceList": [
    {
      "resourceId": "{resourceId}",
      "apigwServiceId": "{apigwServiceId}",
      "path": "/members/{memberId}",
      "parentPath": "/members/{memberId}",
      "methodType": "PUT",
      "methodName": "PostMember",
      "methodDescription": "Edit a member info",
      "createdAt": "2021-12-23T23:55:11.300Z",
      "updatedAt": "2021-12-23T23:55:11.300Z",
      "resourcePluginList": [
        {
          "resourcePluginId": "24bef5d0-feaf-4469-9619-a31e9e35a622",
          "resourceId": "{resourceId}",
          "pluginType": "HTTP",
          "pluginConfigJson": {
            "frontendEndpointPath": "/members/{memberId}",
            "backendEndpointPath": "/api/v2/members/${request.path.memberId}"
          },
          "createdAt": "2021-12-23T23:55:11.300Z",
          "updatedAt": "2021-12-23T23:55:11.300Z"
        }
      ]
    }
  ]
}
```

| Field                                                     | Type       | Description                                             |
| ------------------------------------------------------ | -------- | ---------------------------------------------- |
| resourceList                                           | List     | Resource list area                                      |
| resourceList[0].resourceId                             | String   | Resource ID                                         |
| resourceList[0].apigwServiceId                         | String   | API Gateway service ID                             |
| resourceList[0].path                                   | String   | Resource path                                         |
| resourceList[0].parentPath                             | String   | Parent resource path                                         |
| resourceList[0].createdAt                              | DateTime | Resource creation date and time                                       |
| resourceList[0].updatedAt                              | DateTime | Resource modification date and time                                       |
| resourceList[0].methodType                             | Enum     | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| resourceList[0].methodName                             | String   | Method resource name                                     |
| resourceList[0].methodDescription                      | String   | Method resource description                                     |
| resourceList[0].resourcePluginList                     | List     | Resource plugin list area                                 |
| resourceList[0].resourcePluginList[0].resourcePluginId | String   | Resource plugin ID                                    |
| resourceList[0].resourcePluginList[0].resourceId       | String   | Resource ID                                         |
| resourceList[0].resourcePluginList[0].pluginType       | Enum     | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type)    |
| resourceList[0].resourcePluginList[0].pluginConfigJson | Object   | See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin)                   |
| resourceList[0].resourcePluginList[0].createdAt        | DateTime | Resource plugin creation date and time                                  |
| resourceList[0].resourcePluginList[0].updatedAt        | DateTime | Resource plugin modification date and time                                  |


### Delete Resource
- Deletes a resource.
- The root ("/") path resource cannot be deleted.
- The OPTIONS method created by the CORS plugin cannot be deleted. 
- The OPTIONS method created by the CORS plugin is deleted collectively when the CORS plugin is removed from the resource for which the plugin is set.
- Deleting a path resource deletes all child paths and method resources.
- Deleted resources cannot be recovered.

#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| resourceId | String | Required | N/A | N/A | Resource ID |

#### Response

[Response Body]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

### Import Resource
- Imports resources from a file in the [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) format.
- When resources are imported, all existing resources created in the service are deleted and overwritten with the imported resources.
- When a resource is imported, all existing models created in the service are deleted and overwritten with the imported model.
- Note that data of invalid operation in Swagger paths > path > operation will be ignored and not registered.

#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| POST  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/import |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |

[Request Body]
```json
{
  "swaggerData": {
    "info": {
      "title": "Swagger Petstore",
      "version": "1.0.5"
    },
    "paths": {
      "/pet/{petId}": {
        "get": {
          "summary": "Find pet by ID",
          "description": "Returns a single pet",
          "consumes": [
            "application/json"
          ],
          "parameters": [
            {
              "name": "userId",
              "in": "header",
              "required": false,
              "type": "string"
            }
          ],
          "produces": [
            "application/json"
          ],
          "responses": {
            "200": {
              "description": "successful operation",
              "headers": {
                "response-header1": {
                  "description": "This is a response header",
                  "type": "string"
                }
              },
              "schema": {
                "$ref": "#/definitions/Pet"
              }
            }
          },
          "x-nhncloud-apigateway": {
            "plugins": {
              "MOCK": {
                "statusCode": 200,
                "headers": {
                  "Content-Type": "application/json"
                },
                "body": "{\"id\":1,\"name\":\"Dog1\"}\"}"
              }
            }
          }
        }
      }
    },
    "definitions": {
      "Pet": {
        "type": "object",
        "required": [
          "name"
        ],
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| swaggerData | Object  | Required    | N/A | Swagger JSON format | [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/) |
| swaggerData.info | Object | Required | N/A | N/A | API metadata area. See [Info Object](https://swagger.io/specification/v2/#swagger-object) |
| swaggerData.info.title | String | Optional | N/A | N/A | API title. See [Info Object](https://swagger.io/specification/v2/#info-object) |
| swaggerData.info.version | String  | Optional | N/A | N/A | API version information. See [Info Object](https://swagger.io/specification/v2/#info-object) |
| swaggerData.paths | Object | Required | N/A | N/A | Object area with route information of the API that sets the API Gateway route. See [Paths Object](https://swagger.io/specification/v2/#paths-object) |
| swaggerData.paths.{path} | Object | Required | N/A | {path} Max. 255 characters | Object area with {path}, which is the API Gateway route, and method information in {path}. See [Paths Item Object](https://swagger.io/specification/v2/#path-item-object) |
| swaggerData.paths.{path}.{operation} | Object | Optional | N/A | {operation} get, post, put, delete, head, options, patch | Object area with {operation}, which is the API Gateway method, and method information. Data from invalid operations is ignored and not registered. See [Operation Object](https://swagger.io/specification/v2/#operation-object)  |
| swaggerData.paths.{path}.{operation}.summary | String | Optional | {operation} Uppercase | Max. 50 characters | API Gateway method name. |
| swaggerData.paths.{path}.{operation}.description | String | Optional | {operation} Uppercase | Max. 200 characters | API Gateway method description. |
| swaggerData.paths.{path}.{operation}.consumes | Array | Optional | Empty Array | N/A | API Gateway resource request parameters > Content Type List area. |
| swaggerData.paths.{path}.{operation}.consumes[0] | String  | Optional | N/A | \*/* format | API Gateway Resource Request Parameters > Content Type. |
| swaggerData.paths.{path}.{operation}.parameters | Array | Optional | N/A | N/A | API Gateway resource request parameters > Query String, Header, Form Data, Request Body area. See [Parameter Object](https://swagger.io/specification/v2/#parameter-object) |
| swaggerData.paths.{path}.{operation}.parameters[0].name | String | Required | N/A | Max. 50 characters | API Gateway resource request parameters > Query String, Header, Form Data, Request Body name. |
| swaggerData.paths.{path}.{operation}.parameters[0].in | String | Required | N/A | query, header, formData, body | API Gateway resource request parameters > Separate Query String, Header, Form Data, and Request location. |
| swaggerData.paths.{path}.{operation}.parameters[0].description | String | Optional | N/A | Max. 200 characters | API Gateway resource request parameters > Query String, Header, Form Data, Request Body description. |
| swaggerData.paths.{path}.{operation}.parameters[0].required | Boolean | Required | N/A | true, false | API Gateway resource request parameters > Query String, Header, Form Data, Request Body required |
| swaggerData.paths.{path}.{operation}.produces | Array | Optional | Empty Array | N/A | API Gateway resource response > Content Type List area. |
| swaggerData.paths.{path}.{operation}.produces[0] | String | Optional | N/A | \*/* format | API Gateway Resource Response > Content Type. |
| swaggerData.paths.{path}.{operation}.responses | Object | Optional | N/A | N/A | API Gateway resource response > Object area with response HTTP status code information. See [Responses Object](https://swagger.io/specification/v2/#response-object) |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode} | Object | Optional | N/A | {httpStatusCode} 100~599 | API Gateway resource response > Response HTTP status code object area. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.description | String | Optional | N/A |Max. 200 characters | API Gateway resource response > Response HTTP status code > Description. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers | Object | Optional | N/A | N/A | API Gateway resource response > Response HTTP status code > Header object area. See [Header Object](https://swagger.io/specification/v2/#headers-object) |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName} | Object | Optional | N/A | {headerName} Max. 50 characters | API Gateway resource response > Response HTTP status code > Header area. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.description | String | Optional | N/A | Max. 200 characters | API Gateway resource response > Response HTTP status code > Header > Description. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.headers.{headerName}.type | String | Required | N/A | string, number, integer, boolean | API Gateway resource response > Response HTTP status code > Header > Data Type. |
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema | Object | Optional | N/A | N/A | API Gateway resource response > Response HTTP status code > Response Body area.|
| swaggerData.paths.{path}.{operation}.responses.{httpStatusCode}.schema.$ref | String | Required | N/A | Objects declared in Swagger definitions | API Gateway resource response > Response HTTP status code > Response Body > Model. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway | Object | Optional | N/A | N/A | API Gateway-provided feature definition object area. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins | Object | Required | N/A | N/A | API Gateway custom plugin object area. |
| swaggerData.paths.{path}.{operation}.x-nhncloud-apigateway.plugins.{pluginCode} | Object | Required | N/A | {pluginCode} HTTP, MOCK, CORS, SET_REQUEST_HEADER, SET_RESPONSE_HEADER, ADD_REQUEST_QUERY_PARAMETER | See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type). See [JSON setting value by resource plugin type](./api-guide-v1.0/#resource-plugin). |
| swaggerData.definitions | Object | Optional | N/A | N/A | API Gateway resource request parameters, body object definition area used in response. See [Definitions Object](https://swagger.io/specification/v2/#definitionsObject) |




## Resource Plugin

### HTTP
- Sets the backend endpoint path to forward the request to for the resource path where API Gateway will receive the request.
- It can only be set in resource methods.
- It cannot be set at the same time as the MOCK plugin.

```json
{
  "frontendEndpointPath": "/path",
  "backendEndpointPath": "/anything"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| frontendEndpointPath | String | Required | N/A | Max. 255 characters | The resource path where API Gateway will receive requests. |
| backendEndpointPath  | String | Required | N/A | Max. 255 characters | Backend endpoint path to forward requests received from API Gateway |

### MOCK
- Returns a response defined for a received request.
- It can only be set on resource methods.
- It cannot be set at the same time as the HTTP plugin.
```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"isSuccess\":true}\"}"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| statusCode | String | Required | N/A | 100-599 | Custom response HTTP status code                 |
| headers | Map | Optional | N/A | N/A |Custom response header object area                  |
| headers[{HeaderName}] | String | Required | N/A | N/A | The object property key/value is the name and value of the custom response header. |
| body                  | String | Optional | N/A | N/A | Custom response body                         |

### CORS
- Allows XMLHttpRequest API calls within a cross-site method.
- It can only be set on resource paths.
- The OPTIONS method is automatically created under the path where the CORS plugin is set, and if there is a registered OPTIONS method, it is replaced.
```json
{
  "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
  "allowedHeaders": ["*"],
  "allowedOrigins": ["*"],
  "exposedHeaders": ["X-NHN-HEADER"],
  "maxCredentialsAge": 60,
  "allowCredentials": false
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| allowedMethods | List | Required | N/A | N/A | Area for the list of methods to allow access to resources |
| allowedMethods[0] | Enum | Required | N/A | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | See [HTTP Method Type Enum Code](./enum-code/#http-method-type) |
| allowedHeaders | List | Required | N/A | N/A | Area for the list of HTTP headers that can be used in the request. |
| allowedHeaders[0] | String | Required | N/A | N/A | HTTP header that can be used in the request (e.g. wildcard format: '\*' or 'X-NHN-HEADER, Content-Type') |
| allowedOrigins    | List | Required | N/A | N/A | Area for the list of domains of the origin servers that can access the resource. |
| allowedOrigins[0] | String | Required | N/A | N/A | Domain of the origin server that can access the resource (e.g., wildcard format: '\*' or 'http://example.nhncloudservice.com:8080') |
| exposedHeaders    | List | Optional | N/A | N/A | Area for list of headers accessible by browser (client) |
| exposedHeaders[0] | String | Required | N/A | N/A |Header accessible by browser (client) |
| maxCredentialsAge | Integer | Optional | N/A | -1~86400 |Response browser cache time for preflight requests (in seconds) |
| allowCredentials  | Boolean | Required | N/A |true/false | Whether to request with credentials |



### SET_REQUEST_HEADER
- Add or change the request header. 
- It can be set in the resource path and method.
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| headers | Map | Required | N/A | N/A | Area for request header object to add or change |
| headers[{HeaderName}] | String | Required | N/A | N/A | The name and value of the request header to be added/changed by the object property key/value. |

### SET_RESPONSE_HEADER
- The response header change plugin adds or changes a header to backend responses. 
- It can be set in the resource path and method.
```json
{
  "headers": {
    "headerName": "headerValue"
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| headers | Map | Required | N/A | N/A | Area for request header object to add or change |
| headers[{HeaderName}] | String | Required | N/A | N/A | The name and value of the response header to be added/changed by the object property key/value |

### ADD_REQUEST_QUERY_PARAMETER
- Add a query string parameter to the backend endpoint request.
- It can be set in the resource path and method.
```json
{
  "parameters": {
    "queryName1": "queryValue1"
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| parameters | Map| Required | N/A | N/A | Area for objects of request query string parameters to add |
| parameters[{QueryName}] | String | Required | N/A | N/A | The object property key/value is the name and value of the request query string parameters to be added |

## Resource Parameter

### List Resource Parameters 
- Retrieves a list of resource parameters.

#### Request

[URI]
 
| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId     | String | Required    | N/A  | N/A    | API Gateway resource ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "queryStringList": [
    {
      "name": "query1",
      "description": "This is a query1",
      "dataType": "STRING",
      "required": false,
      "isArray": false
    }
  ],
  "headerList": [
    {
      "name": "header1",
      "description": "This is a header1",
      "dataType": "STRING",
      "required": false,
      "isArray": null
    }
  ],
  "formDataList": [
    {
      "name": "formDataString",
      "description": "This is a formData String",
      "dataType": "STRING",
      "required": false,
      "isArray": false
    },
    {
      "name": "formDataFile",
      "description": "This is a formData File",
      "dataType": "FILE",
      "required": false,
      "isArray": false
    }
  ],
  "requestBody": {
    "name": "requestBody",
    "description": "This is a requestBody",
    "modelId": "{modelId}"
  },
  "contentTypeList": [
    "application/json"
  ]
}
```

| Field                             | Type      | Description                                                   |
| ------------------------------ | ------- | ---------------------------------------------------- |
| queryStringList                | List    | Query string list area                                         |
| queryStringList[0].name        | String  | Query string name                                            |
| queryStringList[0].description | String  | Query string description                                            |
| queryStringList[0].dataType    | Enum    | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type)|
| queryStringList[0].required    | Boolean | Whether the query string is required or not                                         |
| queryStringList[0].isArray     | Boolean | Whether the query string is Array or not                                      |
| headerList                     | List    | Header list area                                             |
| headerList[0].name             | String  | Header Value                                                |
| headerList[0].description      | String  | Header description                                                |
| headerList[0].dataType         | Enum    | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type) |
| headerList[0].required         | Boolean | Header required or not                                             |
| headerList[0].isArray          | null    | Whether the header is Array is not provided.                                      |
| formDataList                   | List    | Form data list area                                          |
| formDataList[0].name           | String  | Form data name                                             |
| formDataList[0].description    | String  | Form data description                                             |
| formDataList[0].dataType       | Enum    | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type) |
| formDataList[0].required       | Boolean | Whether the form data is required or not                                          |
| formDataList[0].isArray        | Boolean | Whether the form data is Array or not                                       |
| requestBody                    | Object  | Request body area                                             |
| requestBody.name               | String  | Request body name                                             |
| requestBody.description        | String  | Request body description                                             |
| requestBody.modelId            | String  | Model ID associated with the request body                                     |
| contentTypeList                | List    | Content type list area                                         |
| contentTypeList[0]             | String  | Enter the content type (e.g., application/json) of the documents to send to the server.                                               |



### Create Resource Parameters
- Creates parameters of a resource method.
- Existing resource parameters are deleted, and requested resource parameters are created. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/parameters |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId     | String | Required    | N/A  | N/A    | API Gateway resource ID |

[Request Body]
```json
{
  "queryStringList": [
    {
      "name": "query1",
      "description": "This is a query1",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "headerList": [
    {
      "name": "header1",
      "description": "This is a header1",
      "dataType": "BOOLEAN",
      "required": true
    }
  ],
  "formDataList": [
    {
      "name": "formDataString",
      "description": "This is a formDataString",
      "dataType": "BOOLEAN",
      "required": true,
      "isArray": true
    }
  ],
  "requestBody": {
    "name": "requestBody",
    "description": "This is a requestBody",
    "modelId": "{modelId}"
  },
  "contentTypeList": [
    "application/json"
  ]
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| queryStringList                | List    | Optional    | Empty List    | Max. 50 items                                              | Query string list area                                         |
| queryStringList[0].name        | String  | Required    | N/A           | Max. 50 characters                                              | Query string name                                            |
| queryStringList[0].description | String  | Optional    | N/A           | Max. 200 characters                                             | Query string description                                            |
| queryStringList[0].dataType    | Enum    | Required    | N/A           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type)|
| queryStringList[0].required    | Boolean | Required    | N/A           | true, false                                          | Whether the query string is required or not                                         |
| queryStringList[0].isArray     | Boolean | Required    | N/A           | true, false                                          | Whether the query string is Array or not                                      |
| headerList                     | List    | Optional    | Empty List    | Max. 50 items                                              | Header list area                                             |
| headerList[0].name             | String  | Required    | N/A           | Max. 50 characters                                              | Header Value                                                |
| headerList[0].description      | String  | Optional    | N/A           | Max. 200 characters                                             | Header description                                                |
| headerList[0].dataType         | Enum    | Required    | N/A           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE        | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type)|
| headerList[0].required         | Boolean | Required    | N/A           | true, false                                          | Header required or not                                             |
| formDataList                   | List    | Optional    | Empty List    | Max. 50 items                                              | Form data list area                                          |
| formDataList[0].name           | String  | Required    | N/A           | Max. 50 characters                                              | Form data name                                             |
| formDataList[0].description    | String  | Optional    | N/A           | Max. 200 characters                                             | Form data description                                             |
| formDataList[0].dataType       | Enum    | Required    | N/A           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE, FILE  | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type)|
| formDataList[0].required       | Boolean | Required    | N/A           | true, false                                          | Whether the form data is required or not                                          |
| formDataList[0].isArray        | Boolean | Required    | N/A           | true, false                                          | Whether the query string is Array or not. false if dataType is FILE.            |
| requestBody                    | Object  | Optional    | Empty Object  | N/A                                                  | Request body object area                                          |
| requestBody.name               | String  | Required    | N/A           | Max. 50 characters                                              | Request body name                                             |
| requestBody.description        | String  | Optional    | N/A           | Max. 200 characters                                             | Request body description                                             |
| requestBody.modelId            | String  | Required    | N/A           | N/A                                                  | Model ID associated with the request body                                    |
| contentTypeList                | List    | Optional    | Empty List    | Max. 10 items                                              | Content type list area                                         |
| contentTypeList[0]             | String  | Required    | N/A           | \*/* format                                             | Enter the content type (e.g., application/json) of the documents to send to the server.                                               |

#### Response

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

## Resource Response

### Get Resource Response 
- Retrieves the header, request body item, and content type for each HTTP response status code.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId     | String | Required    | N/A  | N/A    | API Gateway resource ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "responseList": [
    {
      "responseStatusCode": 200,
      "description": "HTTP Status 200",
      "headerList": [
        {
          "name": "header1",
          "description": "This is a response header1",
          "dataType": "STRING"
        }
      ],
      "responseBody": {
        "name": "responseBody",
        "description": "This is a responseBody",
        "modelId": "{modelId}"
      }
    }
  ],
  "contentTypeList": [
    "application/json"
  ]
}
```

| Field                                        | Type      | Description                                                   |
| ----------------------------------------- | ------- | ---------------------------------------------------- |
| responseList                              | List    | Response information list area by HTTP response status code                           |
| responseList[0].responseStatusCode        | Integer | HTTP response status code                                        |
| responseList[0].description               | String  | HTTP response status code description                                     |
| responseList[0].headerList                | List    | HTTP response header list area                                     |
| responseList[0].headerList[0].name        | String  | Response header name                                             |
| responseList[0].headerList[0].description | String  | Response header description                                             |
| responseList[0].headerList[0].dataType    | Enum    | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type)|
| responseList[0].responseBody              | Object  | HTTP response body object area                                     |
| responseList[0].responseBody.name         | String  | Response body name                                             |
| responseList[0].responseBody.description  | String  | Response body description                                             |
| responseList[0].responseBody.modelId      | String  | Model ID associated with the response body                                     |
| contentTypeList                           | List    | Content type list area                                         |
| contentTypeList[0]                        | String  | Enter the content type (e.g., application/json) of the documents to send to the server.                                               |


### Create Resource Responses
- Existing resource responses are deleted, and header, request body items, and content type for each requested HTTP response status code are created.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/resources/{resourceId}/responses |

[Path Parameter]

| Name             | Type     | Required | Default value | Valid range | Description                 |
| -------------- | ------ | ----- | --- | ----- | ------------------ |
| apigwServiceId | String | Required    | N/A  | N/A    | API Gateway service ID |
| resourceId     | String | Required    | N/A  | N/A    | API Gateway resource ID |

[Request Body]
```json
{
  "responseList": [
    {
      "responseStatusCode": 200,
      "description": "HTTP Status 200",
      "headerList": [
        {
          "name": "header1",
          "description": "This is a response header1",
          "dataType": "STRING"
        }
      ],
      "requestBody": {
        "name": "responseBody",
        "description": "This is a response body",
        "modelId": "{modelId}"
      }
    }
  ],
  "contentTypeList": [
    "application/json"
  ]
}
```

| Name                                        | Type      | Required | Default value          | Valid range                                         | Description                                                   |
| ----------------------------------------- | ------- | ----- | ------------ | --------------------------------------------- | ---------------------------------------------------- |
| responseList                              | List    | Optional    | Empty List   | N/A                                            | Response information list area by HTTP response status code                           |
| responseList[0].responseStatusCode        | Integer | Required    | N/A           | 100-599                                       | HTTP response status code                                        |
| responseList[0].description               | String  | Optional    | N/A         | Max. 200 characters                                       | HTTP response status code description                                     |
| responseList[0].headerList                | List    | Optional    | Empty List   | Max. 50 items                                        | HTTP response header list area                                     |
| responseList[0].headerList[0].name        | String  | Required    | N/A           | Max. 50 characters                                        | Response header name                                             |
| responseList[0].headerList[0].description | String  | Optional    | N/A         | Max. 200 characters                                       | Response header description                                             |
| responseList[0].headerList[0].dataType    | Enum    | Required    | N/A           | STRING, BOOLEAN, INTEGER, LONG, FLOAT, DOUBLE | See [Resource Request/Response Parameter Data Type Enum Code](./enum-code/#resource-requestresponse-parameter-data-type) |
| responseList[0].responseBody              | Object  | Optional    | Empty Object | N/A                                            | HTTP response body object area                                     |
| responseList[0].responseBody.name         | String  | Required    | N/A           | Max. 50 characters                                        | Response body name                                             |
| responseList[0].responseBody.description  | String  | Optional    | N/A         | Max. 200 characters                                       | Response body description                                             |
| responseList[0].responseBody.modelId      | String  | Required    | N/A           | N/A                                           | Model ID associated with the response body                                     |
| contentTypeList                           | List    | Optional    | Empty List   | Max. 10 items                                        | Content type list area                                         |
| contentTypeList[0]                        | String  | Required    | N/A           | \*/* format                                        | Enter the content type (e.g., application/json) of the documents to send to the server.                                               |


#### Response

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

## Model

### List Models 
- Retrieves a list of models.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |
| modelName | String | Optional | N/A | Max. 50 characters  | Model name filter condition. It must contain a string of the model name.|

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "modelList": [
    {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 128
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:47.000Z"
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | Paging area                                        |
|paging.page                          |Integer | Current page                                        |
|paging.limit                         |Integer | Count per page                                  |
|paging.totalCount                    |Integer | Total count                                        |
|modelList                     |List    | Model list area                         |
|modelList[0].apigwServiceId  |String  |API Gateway service ID |
|modelList[0].modelId         |String  |Model ID              |
|modelList[0].modelName       |String  |Model name              |
|modelList[0].modelDescription|String  |Model description              |
|modelList[0].modelSchema     |Object  |[JSON Schema](https://json-schema.org/) draft-04 JSON object of model |
|modelList[0].createdAt       |DateTime|Model creation date and time            |
|modelList[0].updatedAt       |DateTime|Model modification date and time            |



### Create Model
- Creates a model in JSON Schema format.
- Mode names cannot be duplicated.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |


[Request Body]

```json
{
  "modelName": "UserModel",
  "modelDescription": "This is a user model.",
  "modelSchema": {
    "type": "object",
    "properties": {
      "userName": {
        "type": "string"
      },
      "userDescription": {
        "description": "user description",
        "type": "string",
        "maxLength": 128
      }
    },
    "required": [
      "userName"
    ]
  }
}
```

| Name               | Type     | Required | Default value | Valid range   | Description                                                           |
| ---------------- | ------ | ----- | --- | ------- | ------------------------------------------------------------ |
| modelName        | String | Required    | N/A  | Max. 50 characters  | Model name                                                        |
| modelDescription | String | Optional    | N/A  | Max. 200 characters | Model description                                                        |
| modelSchema      | Object | Required    | N/A  | Max. 65535 characters| [JSON Schema](https://json-schema.org/) draft-04 JSON object of model |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 128
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:47.000Z"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | Model area                         |
|model.apigwServiceId  |String  |API Gateway service ID |
|model.modelId         |String  |Model ID              |
|model.modelName       |String  |Model name              |
|model.modelDescription|String  |Model description              |
|model.modelSchema     |Object  |[JSON Schema](https://json-schema.org/) draft-04 JSON object of model |
|model.createdAt       |DateTime|Model creation date and time            |
|model.updatedAt       |DateTime|Model modification date and time            |


### Modify Model 
- Modifies the description and schema of model. 
- Model name cannot be changed. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| modelId | String | Required | N/A | N/A | Model ID |

[Request Body]

```json
{
  "modelDescription": "This is user model.",
  "modelSchema": {
    "type": "object",
    "properties": {
      "userName": {
        "type": "string"
      },
      "userDescription": {
        "description": "user description",
        "type": "string",
        "maxLength": 256
      }
    },
    "required": [
      "userName"
    ]
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| modelDescription | String | Optional    | N/A  | Max. 200 characters | Model description                                                        |
| modelSchema      | Object | Required    | N/A  | Max. 65535 characters| [JSON Schema](https://json-schema.org/) draft-04 JSON object of model |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "model": {
      "modelId": "{modelId}",
      "apigwServiceId": "{apigwServiceId}",
      "modelName": "UserModel",
      "modelDescription": "This is a user model.",
      "modelSchema": {
        "type": "object",
        "properties": {
          "userName": {
            "type": "string"
          },
          "userDescription": {
            "description": "user description",
            "type": "string",
            "maxLength": 256
          }
        },
        "required": [
          "userName"
        ]
      },
      "createdAt": "2021-10-11T23:51:47.000Z",
      "updatedAt": "2021-10-11T23:51:50.000Z"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|model                     |Object    | Model area                         |
|model.apigwServiceId  |String  |API Gateway service ID |
|model.modelId         |String  |Model ID              |
|model.modelName       |String  |Model name              |
|model.modelDescription|String  |Model description              |
|model.modelSchema     |Object  |[JSON Schema](https://json-schema.org/) draft-04 JSON object of model |
|model.createdAt       |DateTime|Model creation date and time            |
|model.updatedAt       |DateTime|Model modification date and time            |


### Delete Model
- Deletes a model.
- If the model is referenced in a request parameter or response of a resource, the model cannot be deleted. To delete a model, please release the reference and then delete the model.

#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/models/{modelId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| modelId | String | Required | N/A | N/A | Model ID |

#### Response

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```

## Stage

### List Stages 
- Retrieves a list of stages.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "stageList": [
    {
      "stageId": "{stageId}",
      "apigwServiceId": "{apigwServiceId}",
      "regionCode": "KR1",
      "stageName": "alpha",
      "stageDescription": "alpha environment stage",
      "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "backendEndpointUrl": "https://backend.com",
      "resourceUpdatedAt": "2021-10-20T06:43:26.000Z",
      "createdAt": "2021-10-20T06:43:26.000Z",
      "updatedAt": "2021-10-20T06:43:26.000Z"
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | Paging area                                        |
|paging.page                          |Integer | Current page                                        |
|paging.limit                         |Integer | Count per page                                  |
|paging.totalCount                    |Integer | Total count                                        |
|stageList        |List    | Stage list area |
|stageList[0].regionCode       |Enum    |See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)                |
|stageList[0].apigwServiceId   |String  |API Gateway service ID  |
|stageList[0].stageId          |String  |Stage ID             |
|stageList[0].stageName        |String  |Stage name             |
|stageList[0].stageUrl         |String  |Stage URL            |
|stageList[0].stageCustomDomainList   |List  |Area for the list of stage custom domain   |
|stageList[0].stageCustomDomainList[0].customDomain   |String  |Custom domain   |
|stageList[0].stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
|stageList[0].stageDescription |String  |Stage description             |
|stageList[0].backendEndpointUrl|String  |Backend endpoint URL       |
|stageList[0].resourceUpdatedAt|DateTime|Date and time of importing resource to the stage recently |
|stageList[0].createdAt        |DateTime|Stage creation date and time           |
|stageList[0].updatedAt        |DateTime|Stage modification date and time           |


### Swagger Export
- Retrieves a Swagger document. 
- Swagger documents are extracted based on the current stage settings, not the settings deployed in API Gateway.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/swagger |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

#### Response

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "string"
  },
  "swaggerData": "{swaggerJson}"
}
```

|Field                                  |Type     |Description                                           |
|-------------------------------------|--------|----------------------------------------------|
|swaggerData        |Object    | A Swagger JSON object based on the current stage. See [Swagger v2.0 OpenAPI Specification](https://swagger.io/specification/v2/). |


### Create Stage
- Creates a stage. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |


[Request Body]
```json
{
  "stageName": "alpha",
  "stageDescription": "alpha environment stage",
  "backendEndpointUrl": "https://backend.com"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| stageName | String | Conditionally required | N/A | Max. 30 characters, English lowercase letters and numbers only | Stage name<br/>Required for non-default stage.  |
| stageDescription | String | Optional | N/A | Max. 200 characters  | Stage description |
| backendEndpointUrl | String | Required | N/A | Max. 150 characters, URL format  | Backend endpoint URL |

- The stageName field value must be unique. 
- Setting the stageName field to null creates a default stage. Only one default stage can be created. 
- The stage URL changes according to the stageName field value.
    - Stage URL format: {regionCode}-{apigwServiceId}-{stageName}.api.nhncloudservice.com



#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stage": {
    "stageId": "{stageId}",
    "apigwServiceId": "{apigwServiceId}",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alpha environment stage",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomDomainList": [],
    "backendEndpointUrl": "https://backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createdAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | Stage area |
|stage.regionCode       |Enum    |See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)                |
|stage.apigwServiceId   |String  |API Gateway service ID  |
|stage.stageId          |String  |Stage ID             |
|stage.stageName        |String  |Stage name             |
|stage.stageUrl         |String  |Stage URL            |
|stage.stageCustomDomainList   |List  |Area for the list of stage custom domain   |
|stage.stageCustomDomainList[0].customDomain   |String  |Custom domain   |
|stage.stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
|stage.stageDescription |String  |Stage description             |
|stage.backendEndpointUrl      |String  |Backend endpoint URL       |
|stage.resourceUpdatedAt|DateTime|Date and time of importing resource to the stage recently |
|stage.createdAt        |DateTime|Stage creation date and time           |
|stage.updatedAt        |DateTime|Stage modification date and time           |

### Modify Stage 
- You can modify the backend endpoint URL and description of the stage.
- Stage name cannot be changed.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |


[Request Body]
```json
{
  "backendEndpointUrl": "https://v2.backend.com",
  "stageDescription": "alpha v2 environment stage"
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| backendEndpointUrl | String | Required | N/A | Max. 150 characters, URL format  | Backend endpoint URL |
| stageDescription | String | Optional | N/A | Max. 200 characters  | Stage description |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stage": {
    "stageId": "{stageId}",
    "apigwServiceId": "{apigwServiceId}",
    "regionCode": "KR1",
    "stageName": "alpha",
    "stageDescription": "alpha v2 environment stage",
    "stageUrl": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
    "stageCustomDomainList": [],
    "backendEndpointUrl": "https://v2.backend.com",
    "resourceUpdatedAt": "2021-10-22T02:22:11.182Z",
    "createdAt": "2021-10-22T02:22:11.182Z",
    "updatedAt": "2021-10-22T02:22:11.182Z"
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stage        |Object    | Stage area |
|stage.regionCode       |Enum    |See [API Gateway Region Enum Code](./enum-code/#api-gateway-region)                |
|stage.apigwServiceId   |String  |API Gateway service ID  |
|stage.stageId          |String  |Stage ID             |
|stage.stageName        |String  |Stage name             |
|stage.stageUrl         |String  |Stage URL            |
|stage.stageCustomDomainList   |List  |Area for the list of stage custom domain   |
|stage.stageCustomDomainList[0].customDomain   |String  |Custom domain   |
|stage.stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
|stage.stageDescription |String  |Stage description             |
|stage.backendEndpointUrl      |String  |Backend endpoint URL       |
|stage.resourceUpdatedAt|DateTime|Date and time of importing resource to the stage recently |
|stage.createdAt        |DateTime|Stage creation date and time           |
|stage.updatedAt        |DateTime|Stage modification date and time           |


### Delete Stage
- Deletes a stage.
- If the stage you want to delete is connected to a usage plan, it cannot be deleted. Disconnect the stage from the usage plan and delete it.
- Deleted stages cannot be recovered.

#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| DELETE  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

#### Response

[Response Body]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### List Stage Resources 
* Retrieves a list of resources registered on the stage. The stage resource plugin information set for each resource is included.
* For more information about the stage resource plugin, see [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin).


#### Request

[URI]

| Method  | URI                                  |
| ---- | ------------------------------------ |
| GET  | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |


#### Response

[Response]
```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |Stage resource list area                             |
|stageResourceList[0]      |Object    |Stage resource area                             |
|stageResourceList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].path                   |String  |Stage resource path                                |
|stageResourceList[0].parentPath             |String  |Parent resource path of the stage (parentPath for root (/) path is null)|
|stageResourceList[0].stageId                |String  |Stage ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |Backend endpoint override URL                          |
|stageResourceList[0].methodType             |Enum    |See [HTTP Method Type Enum Code](./enum-code/#http-method-type)  |
|stageResourceList[0].methodName             |String  |Method name                                     |
|stageResourceList[0].methodDescription      |String  |Method description                                     |
|stageResourceList[0].createdAt              |DateTime|Stage resource creation date and time                              |
|stageResourceList[0].updatedAt              |DateTime|Stage resource modification date and time                              |
|stageResourceList[0].stageResourcePluginList|List    |Stage resource's plugin list area                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |Stage resource's plugin area                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |Stage resource's plugin ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type), [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |See configuration JSON by [Resource Plugin Type](./api-guide-v1.0/#resource-plugin), [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|Stage resource plugin creation date and time                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|Stage resource plugin modification date and time                         |



### Import Resources to Stage
* Imports API Gateway Service > Resources to stage. 
* When a resource is imported, stage resources and stage resource plugins are all newly created. 
* Existing resource paths and stage resource plugin settings set in methods are maintained. 
* If no changes are found on the resource, no action is taken.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |


#### Response

[Response]
```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |Stage resource list area                             |
|stageResourceList[0]      |Object    |Stage resource area                             |
|stageResourceList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].path                   |String  |Stage resource path                                |
|stageResourceList[0].parentPath             |String  |Parent resource path of the stage (parentPath for root (/) path is null)|
|stageResourceList[0].stageId                |String  |Stage ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |Backend endpoint override URL                          |
|stageResourceList[0].methodType             |Enum    |See [HTTP Method Type Enum Code](./enum-code/#http-method-type)               |
|stageResourceList[0].methodName             |String  |Method name                                     |
|stageResourceList[0].methodDescription      |String  |Method description                                     |
|stageResourceList[0].createdAt              |DateTime|Stage resource creation date and time                              |
|stageResourceList[0].updatedAt              |DateTime|Stage resource modification date and time                              |
|stageResourceList[0].stageResourcePluginList|List    |Stage resource's plugin list area                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |Stage resource's plugin area                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |Stage resource's plugin ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type), [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |See configuration JSON by [Resource Plugin Type](./api-guide-v1.0/#resource-plugin), [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|Stage resource plugin creation date and time                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|Stage resource plugin modification date and time                         |



### Modify Stage Resource
* Modifies the backend endpoint URL override and stage resource plugin set in the resource path or resource method.
* When a stage resource is modified, all registered stage resource plugins are deleted, and only the requested resource plugin is newly registered.
* For more information about the Stage Resource Plugin, see [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin).

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/resources/{stageResourceId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |
| stageResourceId | String | Required | N/A | N/A | Stage resource ID |


[Request Body]

```json
{
  "customBackendEndpointUrl": "http://custom.backendpoint.com",
  "stageResourcePluginList": [
    {
      "pluginConfigJson": {"isActive": true},
      "pluginType": "API_KEY"
    }
  ]
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| customBackendEndpointUrl | String | Optional | N/A | Max. 150 characters, URL format | Backend endpoint override URL |
| stageResourcePluginList | List | Required | N/A | N/A | Stage resource's plugin list area |
| stageResourcePluginList[0] | Object | Required | N/A | N/A | Stage resource's plugin area |
| stageResourcePluginList[0].pluginType  | Enum | Required | N/A | IP_ACL, HMAC, JWT, API_KEY, PRE_API, RATE_LIMIT | See [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)|
| stageResourcePluginList[0].pluginConfigJson | Object | Required | N/A | N/A | JSON-format object for each stage resource plugin<br>See configuration JSON by [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)|

* The customBackendEndpointUrl field cannot be set in the root (/) resource path.


#### Response

[Response]
```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "parentPath": null,
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customBackendEndpointUrl": null,
      "createdAt": "2021-10-22T04:43:14.000Z",
      "updatedAt": "2021-10-22T04:44:42.000Z",
      "stageResourcePluginList": [
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "HMAC",
          "pluginConfigJson": {
            "secretKey": "hmac-secret-key",
            "clockSkewSeconds": 10,
            "enforceHeaders": []
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        },
        {
          "stageResourcePluginId": "{stageResourcePluginId}",
          "stageResourceId": "{stageResourceId}",
          "pluginType": "RATE_LIMIT",
          "pluginConfigJson": {
            "requestPerSec": 10,
            "defaultKey": "kr1-{apigwServiceId}.alpha-api.nhncloudservice.com/:",
            "keyType": "DEFAULT",
            "extraKeyValue": null
          },
          "createdAt": "2021-10-22T04:44:42.000Z",
          "updatedAt": "2021-10-22T04:44:42.000Z"
        }
      ]
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |Stage resource list area                             |
|stageResourceList[0]      |Object    |Stage resource area                             |
|stageResourceList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].path                   |String  |Stage resource path                                |
|stageResourceList[0].parentPath             |String  |Parent resource path of the stage (parentPath for root (/) path is null)|
|stageResourceList[0].stageId                |String  |Stage ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |Backend endpoint override URL                          |
|stageResourceList[0].methodType             |Enum    |See [HTTP Method Type Enum Code](./enum-code/#http-method-type)               |
|stageResourceList[0].methodName             |String  |Method name                                     |
|stageResourceList[0].methodDescription      |String  |Method description                                     |
|stageResourceList[0].createdAt              |DateTime|Stage resource creation date and time                              |
|stageResourceList[0].updatedAt              |DateTime|Stage resource modification date and time                              |
|stageResourceList[0].stageResourcePluginList|List    |Stage resource's plugin list area                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |Stage resource's plugin area                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |Stage resource's plugin ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type), [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)                        |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |See configuration JSON by [Resource Plugin Type](./api-guide-v1.0/#resource-plugin), [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)            |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|Stage resource plugin creation date and time                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|Stage resource plugin modification date and time                         |


## Stage Resource Plugin
* For resources of the stage, features such as access control, authentication, and usage control can be set in the form of plug-ins. 
* When a plugin is set in the upper level, it is applied to all child methods collectively, and can be overridden in child paths/methods. 

* [Example]: Plugin configuration override
    ```
    /
  /members
    - GET
    - POST
        ```
    * Configuration 
        1. Limit the request number limit on the root (/) resource path to 100 per second
        2. Limit the request number limit on the POST resource method to 10 per second (override)
    * Operation result 
        - For GET /members, limit of 100 per second on the request limit set on root (/) is applied.
        - For POST /members, the 100 requests per second limit set on root (/) is ignored, and the 10 per second limit is applied.

* Plugins configurable depending on resources

| Resource type | List of configurable plugins |
| --- | --- |
| Root (/) resource path |IP ACL, Authentication (either JWT or HMAC), Pre-call API, Request number limit, API key |
| Resource path |Backend endpoint URL override, Pre-call API, API Key |
| Resource method  |Backend endpoint URL override, Pre-call API, Request number limit, API Key |


### IP ACL 
* API Gateway requests can be allowed/denied for the client IDs specified through IP ACL.
* It can only be set on the root (/) resource path. The settings are applied to all child resources.

```json
{
  "pluginType": "IP_ACL",
  "pluginConfigJson": {
    "isPermit": false,
    "ipAclList": [
      {
        "ipCidrAddress": "192.168.0.1",
        "description": "ip format"
      },
      {
        "ipCidrAddress": "192.168.0.0/24",
        "description": "cidr format"
      }
    ]
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | IP_ACL | See IP_ACL in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A | N/A | IP ACL plugin configuration area |
| pluginConfigJson.isPermit | Boolean | Required | N/A | true, false | If set to false, the request is denied for the configured IP/CIDR. If set to true, the request is allowed only for the configured IP/CIDR.  |
| pluginConfigJson.ipAclList | List | Required | N/A | 1~100 items | Area for IP or CIDR list to allow/deny requests |
| pluginConfigJson.ipAclList[0].ipCidrAddress | String | Required | N/A | IP or CIDR format | Set IP or CIDR. |
| pluginConfigJson.ipAclList[0].description | String | Optional | N/A | Max. 200 characters | Set the description. |


### HMAC
* Settings for validating the tampering of client requests through HMAC signature verification. 
* It can only be set on the root (/) resource path. The settings are applied to all child resources.
* HMAC authentication cannot be set at the same time as JWT authentication. 
* Set the secret key used for signing.
* Set the validation validity period to prevent validation failures caused by time differences.
* Set a list of headers that must be included in the request.

```json
{
  "pluginType": "HMAC",
  "pluginConfigJson": {
    "secretKey": "{secretKey}",
    "clockSkewSeconds": 0,
    "enforceHeaders": [
      "Authorization"
    ]
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | HMAC | See HMAC in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A | N/A | HMAC plugin configuration area |
| pluginConfigJson.secretKey | String | Required | N/A | N/A | Set the secret key used for signing. It is recommended to set it to a string of at least 32 bytes.|
| pluginConfigJson.clockSkewSeconds | Integer | Optional | 0 | 0~86400 | Specify the request validity period (in seconds). |
| pluginConfigJson.enforceHeaders | Array | Optional | Empty List | N/A | Enter a string array of required validation headers. |
| pluginConfigJson.enforceHeaders[0] | String | Required | N/A | N/A| String of required validation headers |


### JWT 
* Settings for validating the signature of the JWT token and request claims.
* It can only be set on the root (/) resource path. The settings are applied to all child resources.
* JWT authentication cannot be set at the same time as HMAC authentication.
* Set the token encryption algorithm for signature verification and the private or public key according to the encryption algorithm method.
* Set the claim validation condition to validation the value of the request claim and whether it is required or not. 
* Set the validation validity period to prevent validation failures caused by time differences.
* **Encryption Algorithm HS256** 
```json
{
  "pluginType": "JWT",
  "pluginConfigJson": {
    "encryptAlgorithm": "HS256",
    "hs256": {
      "secretKey": "{secretKey}"
    },
    "clockSkew": 0,
    "claimValidationCondition": {
      "iss": {
        "value": [],
        "dataType": "Array",
        "required": false,
        "validate": false
      },
      "aud": {
        "value": [],
        "dataType": "Array",
        "required": false,
        "validate": true
      },
      "sub": {
        "value": "",
        "dataType": "String",
        "required": false,
        "validate": false
      },
      "jti": {
        "value": "",
        "dataType": "String",
        "required": false,
        "validate": false
      },
      "exp": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      },
      "iat": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      },
      "nbf": {
        "value": "",
        "dataType": "NumericDate",
        "required": false,
        "validate": true
      }
    }
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | JWT | See JWT in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A  | N/A | JWT plugin configuration area |
| pluginConfigJson.encryptAlgorithm | Enum | Required | HS256 | HS256 | See [JWT > Encryption Algorithm Enum Code](./enum-code/#jwt-encryption-algorithm)  |
| pluginConfigJson.hs256 | Object | Required | N/A | N/A | HS256 validation area |
| pluginConfigJson.hs256.secretKey | String | Required | N/A | N/A | Set the secret key used for signing. It is recommended to set it to a string of at least 32 bytes.|
| pluginConfigJson.clockSkew | Integer | Optional | 0 | 0~86400 | Specify the validation validity period (in seconds) of the exp, nbf claim. |
| pluginConfigJson.claimValidationCondition | Object | Optional | Default Object | N/A | Claim validation condition area |
| pluginConfigJson.claimValidationCondition.iss | Object | Optional | Default Object | N/A | The iss claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.iss.value | Array | Required | Empty Array | N/A |  Set the value of the claim to allow among the values of the iss request claim as a string array. |
| pluginConfigJson.claimValidationCondition.iss.value[0] | String | Optional | N/A | N/A |  Set the string to allow among the values of the iss request claim. |
| pluginConfigJson.claimValidationCondition.iss.dataType | Enum | Optional | Array | Array | Set the data type of the iss claim. Only Array is valid. See <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type) |
| pluginConfigJson.claimValidationCondition.iss.required | Boolean | Required | false | true, false | Set whether the iss request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.iss.validate | Boolean | Required | false | true, false | Set whether to validate the iss request claim value. |
| pluginConfigJson.claimValidationCondition.aud | Object | Optional | Default Object | N/A | The aud claim validation condition area. If not requested, it will be stored as the default value for each field.  |
| pluginConfigJson.claimValidationCondition.aud.value | Array | Required | Empty Array | N/A |  Set the value of the claim to allow among the values of the aud request claim as a string array. |
| pluginConfigJson.claimValidationCondition.aud.value[0] | String | Optional | N/A | N/A |  Set the string to allow among the values of the aud request claim. |
| pluginConfigJson.claimValidationCondition.aud.dataType | Enum | Optional | Array | Array | Set the data type of the aud claim. Only Array is valid. <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type) |
| pluginConfigJson.claimValidationCondition.aud.required | Boolean | Required | false | true, false | Set whether the aud request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.aud.validate | Boolean | Required | true | true | Set whether to validate the aud request claim value. Only true is valid. |
| pluginConfigJson.claimValidationCondition.sub | Object | Optional | Default Object | N/A | The sub claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.sub.value | String | Required | Empty String | N/A |  Set the value of the claim to allow among the values of the sub request claim as a string value. |
| pluginConfigJson.claimValidationCondition.sub.dataType | Enum | Optional | String | String | Set the data type of the sub claim. Only Array is valid.<br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type)|
| pluginConfigJson.claimValidationCondition.sub.required | Boolean | Required | false | true, false | Set whether the sub request claim value is required to be validated. <br/> If the validate field value is true, required must be set to true.  |
| pluginConfigJson.claimValidationCondition.sub.validate | Boolean | Required | false | true, false | Set whether to validate the sub request claim value. |
| pluginConfigJson.claimValidationCondition.jti | Object | Optional | Default Object | N/A | The jti claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.jti.value | String | Required | Empty String | N/A | The jti claim does not require setting the validation values to allow, so set it to an empty string. |
| pluginConfigJson.claimValidationCondition.jti.dataType | Enum | Optional | String | String | Set the data type of the jti claim. <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type)|
| pluginConfigJson.claimValidationCondition.jti.required | Boolean | Required | false | true, false | Set whether the jti request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.jti.validate | Boolean | Required | false | false | Set whether to validate the jti request claim value. Only false is valid.|
| pluginConfigJson.claimValidationCondition.exp | Object | Optional | Default Object | N/A | The exp claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.exp.dataType | Enum | Optional | NumericDate | NumericDate | Set the data type of the exp claim. Only NumericDate is valid. See <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type) |
| pluginConfigJson.claimValidationCondition.exp.required | Boolean | Required | false | true, false | Set whether the exp request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.exp.validate | Boolean | Optional | true | true | Set whether to validate the exp request claim value. Only true is valid. |
| pluginConfigJson.claimValidationCondition.iat | Object | Optional | Default Object | N/A | The iat claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.iat.dataType | Enum | Optional | NumericDate | NumericDate | Set the data type of the iat claim. Only NumericDate is valid. See <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type) |
| pluginConfigJson.claimValidationCondition.iat.required | Boolean | Required | false | true, false | Set whether the iat request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.iat.validate | Boolean | Optional | true | true | Set whether to validate the iat request claim value. Only true is valid. |
| pluginConfigJson.claimValidationCondition.nbf | Object | Optional | Default Object | N/A | The nbf claim validation condition area. If not requested, it will be stored as the default value for each field. |
| pluginConfigJson.claimValidationCondition.nbf.dataType | Enum | Optional | NumericDate | NumericDate | Set the data type of the nbf claim. Only NumericDate is valid. See <br/>[JWT > Claim Data Type Enum Code](./enum-code/#jwt-claim-data-type)|
| pluginConfigJson.claimValidationCondition.nbf.required | Boolean | Required | false | true, false | Set whether the nbf request claim value is required to be validated. |
| pluginConfigJson.claimValidationCondition.nbf.validate | Boolean | Optional | true | true | Sets whether to validate the nbf request claim value. Only true is valid. |


* **Encryption algorithm RS256: (PEM format public key setting method)** 

```json
{
  "pluginType": "JWT",
  "pluginConfigJson": {
    "encryptAlgorithm": "RS256",
    "rs256": {
      "publicKeyType": "RSA_PUBLIC_KEY",
      "rsaPublicKey": "-----BEGIN PUBLIC KEY-----\n{publicPemKey}\n-----END PUBLIC KEY-----"
    },
    "clockSkew": 0,
    "claimValidationCondition": {
      ...
    }
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | JWT | See JWT in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A  | N/A | JWT plugin configuration area |
| pluginConfigJson.encryptAlgorithm | Enum | Required | RS256 | RS256 | See [JWT > Encryption Algorithm Enum Code](./enum-code/#jwt-encryption-algorithm)  |
| pluginConfigJson.rs256 | Object | Required | N/A | N/A | RS256 configuration area |
| pluginConfigJson.rs256.publicKeyType | Enum | Required | N/A | RSA_PUBLIC_KEY | Set the public key in PEM format. See [JWT > RS256 Encryption Algorithm > Public Key Type Enum Code](./enum-code/#jwt-rs256-encryption-algorithm-public-key-type) |
| pluginConfigJson.rs256.rsaPublicKey | String | Required | N/A | Public key in PEM format | Set the public key value in PEM format. It must be entered including the newline character (\\n). |
| pluginConfigJson.clockSkew | Integer | Optional | 0 | 0~86400 | Specify the validation validity period (in seconds) of the exp, nbf claim. |
| pluginConfigJson.claimValidationCondition | Object | Optional | Default Object | N/A | Claim validation condition field (encryption algorithm: same as claimValidationCondition field description of HS256) |


* **Encryption algorithm RS256: (JSON Web Key Set URI public key setting method)** 

```json
{
  "pluginType": "JWT",
    "pluginConfigJson": {
      "encryptAlgorithm": "RS256",
      "rs256": {
        "publicKeyType": "JWKS_URI",
        "jwksUri": "https://examp.com/.well-known/jwks.json"
      },
      "clockSkew": 0,
      "claimValidationCondition": {
        ...
    }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | JWT | See JWT in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A  | N/A | JWT plugin configuration area |
| pluginConfigJson.encryptAlgorithm | Enum | Required | RS256 | RS256 |See [JWT > Encryption Algorithm Enum Code](./enum-code/#jwt-encryption-algorithm)  |
| pluginConfigJson.rs256 | Object | Required | N/A | N/A | RS256 configuration area |
| pluginConfigJson.rs256.publicKeyType | String | Required | N/A | JWKS_URI | Set the public key in JSON Web Key Set (JWKS) URI format. See [JWT > RS256 Encryption Algorithm > Public Key Type Enum Code](./enum-code/#jwt-rs256-encryption-algorithm-public-key-type) |
| pluginConfigJson.rs256.rsaPublicKey | String | Required | N/A | N/A | Set the JSON Web Key Set URI. |
| pluginConfigJson.clockSkew | Integer | Optional | 0 | 0~86400 | Specify the validation validity period (in seconds) of the exp, nbf claim. |
| pluginConfigJson.claimValidationCondition | Object | Optional | Default Object | N/A | Claim validation condition field (encryption algorithm: same as claimValidationCondition field description of HS256) |


### Pre-call API 
* The pre-call API calls the user-specified API before calling the backend endpoint to ensure that the backend endpoint is called only if the call's response code is 200 OK.
* It can be set on any resource path and method. 

```json
{
  "pluginType": "PRE_API",
  "pluginConfigJson": {
    "httpMethod": "POST",
    "url": "http://auth.check.com",
    "cacheTtl": 0
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | PRE_API | See PRE_API in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A | N/A | Pre-call API plugin configuration area |
| pluginConfigJson.httpMethod | Enum | Required | N/A | GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH | See [HTTP Method Type Enum Code](./enum-code/#http-method-type)  |
| pluginConfigJson.url | String | Required | N/A | URL format | Enter the URL of the pre-call API. |
| pluginConfigJson.cacheTtl | Integer | Optional | 0 | 0~86400 | Set the cache period of the response status code of the pre-call API. <br/>The code is cached for the configured amount of time only if the response status code is 200 OK. If it is cached, the pre-call API is not called. |


### Request Number Limit 
* Limits the number of requests per second. 
* It can be set in the root (/) resource path and the resource method. 
* By setting the request limit key, you can set a limit on the number of requests per IP, header, and path variable values.

```json
{
  "pluginType": "RATE_LIMIT",
  "pluginConfigJson": {
    "requestPerSec": 100,
    "keyType": "DEFAULT",
    "extraKeyValue": null
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | RATE_LIMIT | See RATE_LIMIT in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A | N/A | Request number limit plugin configuration area |
| pluginConfigJson.keyType | Enum | Required | N/A | DEFAULT, IP, HEADER, PATH_VARIABLE | See [Request Number Limit > Limit Key Enum Code](./enum-code/#request-number-limit-limit-key)  |
| pluginConfigJson.extraKeyValue | String | Conditionally required | N/A | N/A | If keyType is HEADER, the header name must be set.<br/> If the keyType is PATH_VARIABLE, you must set a path variable of the format ${request.path.variable-name}. |
| pluginConfigJson.requestPerSec | Integer | Required | N/A | 1~5000 | Set the maximum number of requests per second. |


### API Key

* Validates that the API Key is valid when calling the API, and verify whether the usage of the specified usage plan has been exceeded. 
* It can be set in the root (/) resource path and the resource method. 


```json
{
  "pluginType": "API_KEY",
  "pluginConfigJson": {
    "isActive": true
  }
}
```

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| pluginType | Enum | Required | N/A | API_KEY | See API_KEY in [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type) |
| pluginConfigJson | Object | Required | N/A | N/A | API Key plugin configuration area |
| pluginConfigJson.isActive | Boolean | Required | N/A | true | Set whether to verify the API key. Must be set to true. |

## Deploy Stage


### Deploy Stage
- Deploys the current stage resources and configurations to the API Gateway service. 
- If there is no changed configuration, the stage deployment request will fail.
- If the stage deployment fails, it is restored to the previous successful stage deployment configuration.
- After requesting stage deployment, you can check whether stage deployment was successful in [Query Result of Recent Stage Deployment](./api-guide-v1.0/#query-result-of-recent-stage-deployment). 

#### Request

[URI]

| Method    | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[Request Body]
```json
{
  "deployDescription": "deploy description"
}
```
| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| deployDescription | String | Optional | N/A | Max. 200 characters | Deployment description |


#### Response

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### Query Result of Recent Stage Deployment 
- You can query the result of [Deploy Stage](./api-guide-v1.0/#deploy-stage_1). 
- After a stage deployment request, it can take up to a minute for the deployment results to be updated. 


#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/latest |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |


#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "latestStageDeployResult": {
    "deployId": "{deployId}",
    "stageId": "{stageId}",
    "deployStatus": "COMPLETE",
    "deployDescription": "",
    "stageResourceList": [
        {
        "stageResourceId": "{stageResourceId}",
        "stageId": "{stageId}",
        "path": "/",
        "parentPath": null,
        "methodType": null,
        "methodName": null,
        "methodDescription": null,
        "customBackendEndpointUrl": null,
        "createdAt": "2021-10-22T04:43:14.000Z",
        "updatedAt": "2021-10-22T04:44:42.000Z",
        "stageResourcePluginList": [
            {
            "stageResourcePluginId": "{stageResourcePluginId}",
            "stageResourceId": "{stageResourceId}",
            "pluginType": "HMAC",
            "pluginConfigJson": {
                "secretKey": "hmac-secret-key",
                "clockSkewSeconds": 10,
                "enforceHeaders": []
            },
            "createdAt": "2021-10-22T04:44:42.000Z",
            "updatedAt": "2021-10-22T04:44:42.000Z"
            },
            {
            "stageResourcePluginId": "{stageResourcePluginId}",
            "stageResourceId": "{stageResourceId}",
            "pluginType": "RATE_LIMIT",
            "pluginConfigJson": {
                "requestPerSec": 10,
                "defaultKey": "kr1-{apigwServiceId}.api.nhncloudservice.com/:",
                "keyType": "DEFAULT",
                "extraKeyValue": null
            },
            "createdAt": "2021-10-22T04:44:42.000Z",
            "updatedAt": "2021-10-22T04:44:42.000Z"
            }
        ]
        }
    ],
    "isBase": false,
    "deployedAt": "2021-10-25T01:40:13.000Z",
    "rollbackAt": null
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|latestStageDeployResult              |Object  | Stage deployment result area                                        |
|latestStageDeployResult.deployId       |String    | Deployment ID |
|latestStageDeployResult.stageId   |String  | Stage ID  |
|latestStageDeployResult.deployDescription        |String  | Deployment description  |
|latestStageDeployResult.deployStatus        |Enum  | See [Stage Deployment > Deployment Status Enum Code](./enum-code/#stage-deployment-deployment-status) |
|latestStageDeployResult.isBase         |String  | Whether the deployment history is the base for the current stage configuration. |
|latestStageDeployResult.deployedAt          |DateTime  | Deployment request date and time |
|latestStageDeployResult.rollbackAt   |DateTime  | Stage rollback request date and time |
|latestStageDeployResult.stageResourceList      |List    |Stage resource list area                             |
|latestStageDeployResult.stageResourceList[0]      |Object    |Stage resource area                             |
|latestStageDeployResult.stageResourceList[0].stageResourceId        |String  |Stage resource ID                                |
|latestStageDeployResult.stageResourceList[0].path                   |String  |Stage resource path                                |
|latestStageDeployResult.stageResourceList[0].parentPath             |String  |Parent resource path of the stage (parentPath for root (/) path is null)|
|latestStageDeployResult.stageResourceList[0].stageId                |String  |Stage ID                                    |
|latestStageDeployResult.stageResourceList[0].customBackendEndpointUrl      |String  |Backend endpoint override URL                          |
|latestStageDeployResult.stageResourceList[0].methodType             |Enum    |See [HTTP Method Type Enum Code](./enum-code/#http-method-type)               |
|latestStageDeployResult.stageResourceList[0].methodName             |String  |Method name                                     |
|latestStageDeployResult.stageResourceList[0].methodDescription      |String  |Method description                                     |
|latestStageDeployResult.stageResourceList[0].createdAt              |DateTime|Stage resource creation date and time                              |
|latestStageDeployResult.stageResourceList[0].updatedAt              |DateTime|Stage resource modification date and time                              |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList|List    |Stage resource's plugin list area                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0]|Object    |Stage resource's plugin area                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |Stage resource's plugin ID                           |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |Stage resource ID                                |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type), [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)                       |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |See configuration JSON by [Resource Plugin Type](./api-guide-v1.0/#resource-plugin), [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)          |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|Stage resource plugin creation date and time                         |
|latestStageDeployResult.stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|Stage resource plugin modification date and time                         |

### Delete Stage Deployment History
- Deletes stage deployment history.
- You cannot delete the current stage's base deployment history (if isBase is true) and the current API Gateway service's deployment history.

#### Request

[URI]

| Method    | URI                                 |
| ------ | ------------------------------------ |
| DELETE | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |
| deployId | String | Required | N/A | N/A | Deployment ID to delete |

#### Response

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### Query Stage Deployment History 
- Retrieves the history of stage deployment in deployment success status. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "stageDeployHistoryList": [
    {
      "deployId": "{deployId}",
      "stageId": "{stageId}",
      "deployedAt": "2021-10-25T01:58:34.000Z",
      "deployDescription": "",
      "isBase": true,
      "rollbackAt": null
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | Paging area                                        |
|paging.page                          |Integer | Current page                                        |
|paging.limit                         |Integer | Count per page                                  |
|paging.totalCount                    |Integer | Total count                                        |
|stageDeployHistoryList        |List    | Stage deployment history list area |
|stageDeployHistoryList[0]        |Object    | Stage deployment history area |
|stageDeployHistoryList[0].deployId       |String    | Deployment ID |
|stageDeployHistoryList[0].stageId   |String  | Stage ID  |
|stageDeployHistoryList[0].deployDescription        |String  | Deployment description  |
|stageDeployHistoryList[0].isBase         |Boolean  | Whether the deployment history is the base for the current stage configuration. |
|stageDeployHistoryList[0].deployedAt          |DateTime  | Deployment request date and time |
|stageDeployHistoryList[0].rollbackAt   |DateTime  | Stage rollback request date and time |


### Rollback Stage
- Rollbacks the current stage configuration to the deployed stage configuration history.  
- Note that all current stage configurations will be deleted when performing the stage rollback.  
- To apply the rolled back stage configurations to the API Gateway service, you must deploy the stage.
- You cannot perform rollback with the deployment history in deployment failure state.

#### Request

[URI]

| Method    | URI                                 |
| ------ | ------------------------------------ |
| POST | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/deploys/{deployId}/rollback |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |
| deployId | String | Required | N/A | N/A | Deployment ID to rollback |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "stageResourceList": [
    {
      "resourceMethod": false,
      "resourcePath": true,
      "parentPath": null,
      "pathKey": "/",
      "rootPath": true,
      "stageResourceId": "{stageResourceId}",
      "stageId": "{stageId}",
      "path": "/",
      "methodType": null,
      "methodName": null,
      "methodDescription": null,
      "customEndpointUrl": null,
      "createdAt": "2021-10-25T08:23:41.139Z",
      "updatedAt": "2021-10-25T08:23:41.139Z",
      "stageResourcePluginList": []
    }
  ]
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|stageResourceList      |List    |Stage resource list area                             |
|stageResourceList[0]      |Object    |Stage resource area                             |
|stageResourceList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].path                   |String  |Stage resource path                                |
|stageResourceList[0].parentPath             |String  |Parent resource path of the stage (parentPath for root (/) path is null)|
|stageResourceList[0].stageId                |String  |Stage ID                                    |
|stageResourceList[0].customBackendEndpointUrl      |String  |Backend endpoint override URL                          |
|stageResourceList[0].methodType             |Enum    |See [HTTP Method Type Enum Code](./enum-code/#http-method-type)               |
|stageResourceList[0].methodName             |String  |Method name                                     |
|stageResourceList[0].methodDescription      |String  |Method description                                     |
|stageResourceList[0].createdAt              |DateTime|Stage resource creation date and time                              |
|stageResourceList[0].updatedAt              |DateTime|Stage resource modification date and time                              |
|stageResourceList[0].stageResourcePluginList|List    |Stage resource's plugin list area                       |
|stageResourceList[0].stageResourcePluginList[0]|Object    |Stage resource's plugin area                       |
|stageResourceList[0].stageResourcePluginList[0].stageResourcePluginId  |String  |Stage resource's plugin ID                           |
|stageResourceList[0].stageResourcePluginList[0].stageResourceId        |String  |Stage resource ID                                |
|stageResourceList[0].stageResourcePluginList[0].pluginType             |Enum    |See [Resource Plugin Type Enum Code](./enum-code/#resource-plugin-type), [Stage Resource > Plugin Type Enum Code](./enum-code/#stage-resource-plugin-type)                       |
|stageResourceList[0].stageResourcePluginList[0].pluginConfigJson       |Object  |See configuration JSON by [Resource Plugin Type](./api-guide-v1.0/#resource-plugin), [Stage Resource Plugin](./api-guide-v1.0/#stage-resource-plugin)         |
|stageResourceList[0].stageResourcePluginList[0].createdAt              |DateTime|Stage resource plugin creation date and time                         |
|stageResourceList[0].stageResourcePluginList[0].updatedAt              |DateTime|Stage resource plugin modification date and time                         |


## API Document

### Query API Document
- Retrieves API document based on the deployed stage configuration. 
- The API document is returned as a JSON object that follows the [Swagger v2.0](https://swagger.io/specification/v2/) specification.
- API document cannot be queried for undeployed stages, and a 404 Not Found response is returned.


#### Request

[URI]

| Method    | URI                                 |
| ------ | ------------------------------------ |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/documents/swagger |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

#### Response

[Response]

```json
{
  "swagger": "2.0",
  "info": {
    "version": "2021-10-26T15:21:22.163+09:00",
    "title": "alpha"
  },
  "host": "kr1-{apigwServiceId}-alpha.api.nhncloudservice.com",
  "schemes": [
    "https",
    "http"
  ],
  "paths": {
    "/members/{proxy+}": {
      "get": {
        "summary": "Member API",
        "description": "",
        "consumes": [
          "application/json"
        ],
        "produces": [
          "application/xml",
          "application/json"
        ],
        "parameters": [
          {
            "name": "proxy+",
            "in": "path",
            "description": "proxy+",
            "required": true,
            "type": "string"
          },
          {
            "name": "memberId",
            "in": "query",
            "description": "member id",
            "required": false,
            "type": "string"
          },
          {
            "name": "x-request-id",
            "in": "header",
            "description": "Request ID",
            "required": false,
            "type": "string"
          },
          {
            "in": "body",
            "name": "Member",
            "description": "Member object",
            "required": false,
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Query success response",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "Response ID"
              }
            },
            "schema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "#/definitions/MemberModel"
            },
            "responseSchema": {
              "$ref": "#/definitions/MemberModel",
              "originalRef": "MemberModel"
            }
          },
          "404": {
            "description": "Unavailable member",
            "headers": {
              "x-response-id": {
                "type": "string",
                "description": "Response ID"
              }
            }
          }
        },
        "security": [
          {
            "x-nhncloud-jwt": [

            ],
            "x-nhncloud-apikey": [

            ]
          }
        ],
        "x-nhncloud-apigateway": {
          "plugins": {
            "HTTP": {
              "frontendEndpointPath": "/members/{proxy+}",
              "backendEndpointPath": "/anything/${request.path.proxy+}"
            }
          }
        }
      },
      "post": {
        "summary": "Member API",
        "description": "",
        "parameters": [
          {
            "name": "proxy+",
            "in": "path",
            "description": "proxy+",
            "required": true,
            "type": "string"
          }
        ],
        "responses": {
          "200": {
            "description": "default response"
          }
        },
        "security": [
          {
            "x-nhncloud-jwt": [

            ],
            "x-nhncloud-apikey": [

            ]
          }
        ],
        "x-nhncloud-apigateway": {
          "plugins": {
            "HTTP": {
              "frontendEndpointPath": "/members/{proxy+}",
              "backendEndpointPath": "/api/${request.path.proxy+}"
            }
          }
        }
      }
    }
  },
  "securityDefinitions": {
    "x-nhncloud-jwt": {
      "type": "apiKey",
      "name": "Authorization",
      "in": "header"
    },
    "x-nhncloud-apikey": {
      "type": "apiKey",
      "name": "x-nhn-apikey",
      "in": "header"
    }
  },
  "definitions": {
    "MemberModel": {
      "type": "object",
      "required": [
        "name"
      ],
      "properties": {
        "name": {
          "type": "string"
        },
        "description": {
          "type": "string",
          "description": "member description",
          "maxLength": 128
        }
      }
    }
  }
}
```

|Field                                   |Type      |Description                                            |
|-------------------------------------|--------|----------------------------------------------|
|swagger                     |String    | Swagger specification version. See [Swagger Object](https://swagger.io/specification/v2/#swagger-object)|
|info         | Object   | The metadata area of the API. See [Info Object](https://swagger.io/specification/v2/#swagger-object)|
|info.version   |String  | The version information of the API, where the date and time of the stage deployment request is set. See [Info Object](https://swagger.io/specification/v2/#info-object)|
|info.title      |String  | The title of the API, where the stage name is set. See [Info Object](https://swagger.io/specification/v2/#info-object)|
|host|String    |The host that provides the API, where the stage URL is set. See [Swagger Object](https://swagger.io/specification/v2/#swagger-object)|
|schemes              |Array  | Supported transport protocol of the API, where [http, https] is set. See [Swagger Object > schemes](https://swagger.io/specification/v2/#swagger-object)|
|paths         | Object  | Paths of APIs, where paths of resource methods are set. See [Paths Object](https://swagger.io/specification/v2/#pathsObject)|
|paths.{path} | Object | {path} is the path of the API, where the path to the resource method is set. See [Paths Object](https://swagger.io/specification/v2/#pathsObject)|
|paths.{path}.{operation}         |Object  | {operation} is an operation on the API path, which is set as a resource method. See [Path Item Object](https://swagger.io/specification/v2/#path-item-object)|
|paths.{path}.{operation}.consumes         | Array  | A list of MIME types that operation on the API path can use. |
|paths.{path}.{operation}.consumes[0]         | String  | MIME types that operation of the API path can use. |
|paths.{path}.{operation}.produces         | Array  | A list of MIME types that operation on the API path can generate. |
|paths.{path}.{operation}.produces[0]         | String  | The MIME types that operation on the API path can generate. |
|paths.{path}.{operation}.summary                |String  | API summary, where the name of the resource is set. See [Operation Object](https://swagger.io/specification/v2/#operation-object)|
|paths.{path}.{operation}.description                |String  |API description, where the description of the resource is set. See [Operation Object](https://swagger.io/specification/v2/#operation-object)|
|paths.{path}.{operation}.parameters                | Object  | API parameter, where the path variable and request parameters of the resource are set. See [Parameter Object](https://swagger.io/specification/v2/#parameter-object)|
|paths.{path}.{operation}.responses                | Object  | API response, where resource response is set. See [Responses Object](https://swagger.io/specification/v2/#responses-object)|
|paths.{path}.{operation}.security     | Array  | A security definition used for the task of an API operation. When setting API Key and authentication (HMAC, JWT), custom settings of API Gateway are included. |
|paths.{path}.{operation}.x-nhncloud-apigateway     | Object  | NHN Cloud API Gateway definition setting area |
|paths.{path}.{operation}.x-nhncloud-apigateway.plugins     | Object  | This is the custom plugin information area for API Gateway. This includes settings in Resources > Plugins and backend endpoint paths mapped to resources. |
|securityDefinitions          |Object    | A security definition object. When setting API Key and authentication (HMAC, JWT), custom settings of API Gateway are included. See [Security Definitions Object](https://swagger.io/specification/v2/#securityDefinitionsObject)|
|definitions | Object | An area for data types used in requests and responses. The model referenced in the request parameter/response is defined. See [Definitions Object](https://swagger.io/specification/v2/#definitionsObject)| 

## API Key

### List API Keys 
- Retrieves the list of API keys.
- If there are multiple request query parameters, a list that satisfies all conditions is returned.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |
| apiKey | String | Optional | N/A | N/A | Primary or Secondary API Key filter condition |
| apiKeyId | String | Optional | N/A | N/A | API Key ID filter condition |
| apiKeyName | String | Optional | N/A | N/A | API Key name filter condition. The starting string of the API Key name must match. |
| apiKeyStatus | Enum | Optional | N/A | ACTIVE, INACTIVE | API Key status filter condition. See [API Key Status Enum Code](./enum-code/#api-key-status) |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiKeyList": [
    {
      "appKey": "{appkey}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "apiKeyDescription": "For User1",
      "primaryApiKey": "{primaryApiKey}",
      "secondaryApiKey": "{secondaryApiKey}",
      "apiKeyStatus": "ACTIVE",
      "createdAt": "2021-06-10T03:06:52.000Z",
      "updatedAt": "2021-06-10T03:06:52.000Z"
    }
  ]
}
```

| Field                              | Type       | Description                                                |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | Paging area                                            |
| paging.page                     | Integer  | Current page                                            |
| paging.limit                    | Integer  | Count per page                                         |
| paging.totalCount               | Integer  | Total count                                            |
| apiKeyList                      | List     | API Key list area                                     |
| apiKeyList[0]                   | Object   | API Key area                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key name                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key description                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key value                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key value                               |
| apiKeyList[0].apiKeyStatus      | Enum     | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| apiKeyList[0].createdAt         | DateTime | API Key creation date and time                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key modification date and time                                      |

### Create API Key
- Generates an API Key. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/apikeys |

[Request Body]
```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE",
  "primaryApiKey": null,
  "secondaryApiKey": null
}
```

| Name                | Type     | Required | Default value | Valid range            | Description                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | Required    | N/A  | Max. 50 characters           | API Key name                                        |
| apiKeyDescription | String | Optional    | N/A  | Max. 200 characters          | API Key description                                        |
| apiKeyStatus      | Enum   | Required    | N/A  | ACTIVE, INACTIVE | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| primaryApiKey     | String   | Optional    | N/A  | Min. 10 characters, Max. 40 characters, English letters, and numbers | Primary API key value, automatically issued when null |
| secondaryApiKey   | String   | Optional    | N/A  | Min. 10 characters, Max. 40 characters, English letters, and numbers | Secondary API key value, automatically issued when null |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

| Field                       | Type       | Description                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key area                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key name                                        |
| apiKey.apiKeyDescription | String   | API Key description                                        |
| apiKey.primaryApiKey     | String   | Primary API Key value                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key value                               |
| apiKey.apiKeyStatus      | Enum     | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| apiKey.createdAt         | DateTime | API Key creation date and time                                      |
| apiKey.updatedAt         | DateTime | API Key modification date and time                                      |


### Modify API Key
- Modifies the name, description, and status of the API key.
- If the API Key status is changed to INACTIVE, the API Key is deactivated and API calls are disabled.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | Required | N/A | N/A | API Key ID |

[Request Body]
```json
{
  "apiKeyName": "User1 API Key",
  "apiKeyDescription": "For User1",
  "apiKeyStatus": "ACTIVE"
}
```

| Name                | Type     | Required | Default value | Valid range            | Description                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyName        | String | Required    | N/A  | Max. 50 characters           | API Key name                                        |
| apiKeyDescription | String | Optional    | N/A  | Max. 200 characters          | API Key description                                        |
| apiKeyStatus      | Enum   | Required    | N/A  | ACTIVE, INACTIVE | See [API Key Status Enum Code](./enum-code/#api-key-status) |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

| Field                       | Type       | Description                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key area                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key name                                        |
| apiKey.apiKeyDescription | String   | API Key description                                        |
| apiKey.primaryApiKey     | String   | Primary API Key value                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key value                               |
| apiKey.apiKeyStatus      | Enum     | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| apiKey.createdAt         | DateTime | API Key creation date and time                                      |
| apiKey.updatedAt         | DateTime | API Key modification date and time                                      |


### Delete API Key
- Deletes the API key. A deleted API key cannot be recovered.
- If you have an API Key connected to a stage in your usage plan, you cannot delete the API Key. To delete it, you need to disconnect the API Key.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/apikeys/{apiKeyId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | Required | N/A | N/A | API Key ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### Reissue API Key
- Primary API Key and Secondary API Key used as API Key values can be reissued respectively.
- In case of reissuance, API calls cannot be made with the old API Key. It is not possible to recover the API Key used before reissuance.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/regenerate |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | Required | N/A | N/A | API Key ID |

[Request Body]
```json
{
  "apiKeyType": "PRIMARY",
  "apiKeyValue": null
}
```

| Name                | Type     | Required | Default value | Valid range            | Description                                                |
| ----------------- | ------ | ----- | --- | ---------------- | ------------------------------------------------- |
| apiKeyType      | Enum   | Required    | N/A  | PRIMARY, SECONDARY | The API Key type you want to change. See [API Key Type Enum Code](./enum-code/#api-key-type) |
| apiKeyValue     | String   | Optional    | N/A  | Min. 10 characters, Max. 40 characters, English letters, and numbers | API key value, automatically issued when null |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiKey": {
    "appKey": "{appKey}",
    "apiKeyId": "{apiKeyId}",
    "apiKeyName": "User1 API Key",
    "apiKeyDescription": "For User1",
    "primaryApiKey": "{primaryApiKey}",
    "secondaryApiKey": "{secondaryApiKey}",
    "apiKeyStatus": "ACTIVE",
    "createdAt": "2021-11-02T07:43:06.458Z",
    "updatedAt": "2021-11-02T07:43:06.458Z"
  }
}
```

| Field                       | Type       | Description                                                |
| ------------------------ | -------- | ------------------------------------------------- |
| apiKey                   | Object   | API Key area                                        |
| apiKey.appKey            | String   | AppKey                                            |
| apiKey.apiKeyId          | String   | API Key ID                                        |
| apiKey.apiKeyName        | String   | API Key name                                        |
| apiKey.apiKeyDescription | String   | API Key description                                        |
| apiKey.primaryApiKey     | String   | Primary API Key value                                 |
| apiKey.secondaryApiKey   | String   | Secondary API Key value                               |
| apiKey.apiKeyStatus      | Enum     | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| apiKey.createdAt         | DateTime | API Key creation date and time                                      |
| apiKey.updatedAt         | DateTime | API Key modification date and time                                      |

### List API Keys that can be connected to stage
- Retrieves the list of API keys that can be connected to the stage.
- If there are multiple request query parameters, a list that satisfies all conditions is returned.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/stages/{stageId}/apikeys/connectable |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| stageId | String | Required | N/A | N/A | Stage ID |


[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |
| apiKey | String | Optional | N/A | N/A | Primary or secondary API key value |
| apiKeyId | String | Optional | N/A | N/A | API Key ID |
| apiKeyName | String | Optional | N/A | N/A | API Key name start string |
| apiKeyStatus | Enum | Optional | N/A | ACTIVE, INACTIVE | See [API Key Status Enum Code](./enum-code/#api-key-status) |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiKeyList": [
    {
      "appKey": "{appkey}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "apiKeyDescription": "For User1",
      "primaryApiKey": "{primaryApiKey}",
      "secondaryApiKey": "{secondaryApiKey}",
      "apiKeyStatus": "ACTIVE",
      "createdAt": "2021-06-10T03:06:52.000Z",
      "updatedAt": "2021-06-10T03:06:52.000Z"
    }
  ]
}
```

| Field                              | Type       | Description                                                |
| ------------------------------- | -------- | ------------------------------------------------- |
| paging                          | Object   | Paging area                                            |
| paging.page                     | Integer  | Current page                                            |
| paging.limit                    | Integer  | Count per page                                         |
| paging.totalCount               | Integer  | Total count                                            |
| apiKeyList                      | List     | API Key list area                                     |
| apiKeyList[0]                   | Object   | API Key area                                        |
| apiKeyList[0].appKey            | String   | AppKey                                            |
| apiKeyList[0].apiKeyId          | String   | API Key ID                                        |
| apiKeyList[0].apiKeyName        | String   | API Key name                                        |
| apiKeyList[0].apiKeyDescription | String   | API Key description                                        |
| apiKeyList[0].primaryApiKey     | String   | Primary API Key value                                 |
| apiKeyList[0].secondaryApiKey   | String   | Secondary API Key value                               |
| apiKeyList[0].apiKeyStatus      | Enum     | See [API Key Status Enum Code](./enum-code/#api-key-status) |
| apiKeyList[0].createdAt         | DateTime | API Key creation date and time                                      |
| apiKeyList[0].updatedAt         | DateTime | API Key modification date and time                                      |


## Usage Plan

### List Usage Plans 
- Retrieves a list of usage plans.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanList": [
    {
      "appKey": "{appKey}",
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic",
      "usagePlanDescription": "It's for Basic User",
      "rateLimitRequestPerSecond": 10,
      "quotaLimitPeriodUnitCode": "DAY",
      "quotaLimit": 100,
      "createdAt": "2021-09-09T05:04:37.000Z",
      "updatedAt": "2021-09-09T05:04:37.000Z"
    }
  ]
}
```

| Field                                         | Type       | Description                                                |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | Paging area                                            |
| paging.page                                | Integer  | Current page                                            |
| paging.limit                               | Integer  | Count per page                                         |
| paging.totalCount                          | Integer  | Total count                                            |
| usagePlanList                              | List     | Usage plan list area                                      |
| usagePlanList[0]                           | Object   | Usage plan area                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | Usage plan ID                                         |
| usagePlanList[0].usagePlanName             | String   | Usage plan name                                         |
| usagePlanList[0].usagePlanDescription      | String   | Usage plan description                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | Limit on the number of requests per second                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| usagePlanList[0].quotaLimit                | Integer  | Request quota per quota period unit                                |
| usagePlanList[0].createdAt                 | DateTime | Usage plan creation date and time                                       |
| usagePlanList[0].updatedAt                 | DateTime | Usage plan modification date and time                                       |



### Get Usage Plan
- Retrieves a single usage plan.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |

#### Response

[Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "usagePlan": {
        "appKey": "{appKey}",
        "usagePlanId": "{usagePlanId}",
        "usagePlanName": "Basic",
        "usagePlanDescription": "It's for Basic User",
        "rateLimitRequestPerSecond": 10,
        "quotaLimitPeriodUnitCode": "MONTH",
        "quotaLimit": 2147483647,
        "createdAt": "2021-11-02T02:26:44.000Z",
        "updatedAt": "2021-11-02T02:26:44.000Z"
    }
}
```

| Field                                  | Type       | Description                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | Usage plan area                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | Usage plan ID                                         |
| usagePlan.usagePlanName             | String   | Usage plan name                                         |
| usagePlan.usagePlanDescription      | String   | Usage plan description                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | Limit on the number of requests per second                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| usagePlan.quotaLimit                | Integer  | Request quota per quota period unit                                |
| usagePlan.createdAt                 | DateTime | Usage plan creation date and time                                       |
| usagePlan.updatedAt                 | DateTime | Usage plan modification date and time                                       |

### Create Usage Plan
- Creates a usage plan.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans |

[Request Body]
```json
{
  "usagePlanName": "string",
  "usagePlanDescription": "string",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

| Name                        | Type      | Required | Default value | Valid range        | Description                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | Required    | N/A  | Max. 50 characters       | Usage plan name                                         |
| usagePlanDescription      | String  | Optional    | N/A  | Max. 200 characters      | Usage plan description                                         |
| rateLimitRequestPerSecond | Integer | Optional    | N/A  | 1~5000       | Limit on the number of requests per second                                        |
| quotaLimitPeriodUnitCode  | Enum    | Optional    | N/A  | DAY, MONTH   | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| quotaLimit                | Integer | Conditionally required | N/A  | 1~2147483647 | Required if quotaLimitPeriodUnitCode is set. Request quota per quota period unit                                |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "usagePlan": {
    "appKey": "{appKey}",
    "usagePlanId": "{usagePlanId}",
    "usagePlanName": "Basic",
    "usagePlanDescription": "It's for Basic User",
    "rateLimitRequestPerSecond": 10,
    "quotaLimitPeriodUnitCode": "MONTH",
    "quotaLimit": 2147483647,
    "createdAt": "2021-11-02T02:26:44.087Z",
    "updatedAt": "2021-11-02T02:26:44.087Z"
  }
}
```

| Field                                  | Type       | Description                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | Usage plan area                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | Usage plan ID                                         |
| usagePlan.usagePlanName             | String   | Usage plan name                                         |
| usagePlan.usagePlanDescription      | String   | Usage plan description                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | Limit on the number of requests per second                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| usagePlan.quotaLimit                | Integer  | Request quota per quota period unit                                |
| usagePlan.createdAt                 | DateTime | Usage plan creation date and time                                       |
| usagePlan.updatedAt                 | DateTime | Usage plan modification date and time                                       |


### Modify Usage Plan
- Modifies a usage plan. 
- If you modify the quota period unit to 'None', the request quota usage of the connected API keys is initialized.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| PUT |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |

[Request Body]
```json
{
  "usagePlanName": "Basic",
  "usagePlanDescription": "It's for Basic User",
  "rateLimitRequestPerSecond": 10,
  "quotaLimitPeriodUnitCode": "DAY",
  "quotaLimit": 100
}
```

| Name                        | Type      | Required | Default value | Valid range        | Description                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| usagePlanName             | String  | Required    | N/A  | Max. 50 characters       | Usage plan name                                         |
| usagePlanName             | String  | Optional    | N/A  | Max. 200 characters      | Usage plan description                                         |
| rateLimitRequestPerSecond | Integer | Optional    | N/A  | 1~5000       | Limit on the number of requests per second                                        |
| quotaLimitPeriodUnitCode  | Enum    | Optional    | N/A  | DAY, MONTH   | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| quotaLimit                | Integer | Conditionally required | N/A  | 1~2147483647 | Required if quotaLimitPeriodUnitCode is set. Request quota per quota period unit                                |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "usagePlan": {
    "appKey": "{appKey}",
    "usagePlanId": "{usagePlanId}",
    "usagePlanName": "Basic",
    "usagePlanDescription": "It's for Basic User",
    "rateLimitRequestPerSecond": 10,
    "quotaLimitPeriodUnitCode": "DAY",
    "quotaLimit": 100,
    "createdAt": "2021-11-02T02:26:44.087Z",
    "updatedAt": "2021-11-02T02:26:44.087Z"
  }
}
```

| Field                                  | Type       | Description                                                |
| ----------------------------------- | -------- | ------------------------------------------------- |
| usagePlan                           | Object   | Usage plan area                                         |
| usagePlan.appKey                    | String   | AppKey                                            |
| usagePlan.usagePlanId               | String   | Usage plan ID                                         |
| usagePlan.usagePlanName             | String   | Usage plan name                                         |
| usagePlan.usagePlanDescription      | String   | Usage plan description                                         |
| usagePlan.rateLimitRequestPerSecond | Integer  | Limit on the number of requests per second                                        |
| usagePlan.quotaLimitPeriodUnitCode  | Enum     | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| usagePlan.quotaLimit                | Integer  | Request quota per quota period unit                                |
| usagePlan.createdAt                 | DateTime | Usage plan creation date and time                                       |
| usagePlan.updatedAt                 | DateTime | Usage plan modification date and time                                       |


### Delete Usage Plan
- Deletes a usage plan.
- You can delete a usage plan after releasing all stages associated with the usage plan.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |

#### Response

[Response]

```json
{
    "header" : {
        "resultCode" :  0,
        "resultMessage" :  "SUCCESS",
        "isSuccessful" :  true
    }
}
```


### List Stages Associated with Usage Plan
- Retrieves a list of stages associated with the usage plan.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanStageList": [
    {
      "regionCode": "KR1",
      "apigwServiceId": "{apigwServiceId}",
      "apigwServiceName": "APIGW Example",
      "stageId": "{stageId}",
      "stageName": "custom",
      "stageUrl": "kr1-example-custom.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic"
    }
  ]
}
```

| Field                                    | Type      | Description                     |
| ------------------------------------- | ------- | ---------------------- |
| paging                                | Object  | Paging area                 |
| paging.page                           | Integer | Current page                 |
| paging.limit                          | Integer | Count per page              |
| paging.totalCount                     | Integer | Total count                 |
| usagePlanStageList                    | List    | Stage list area associated with the usage plan |
| usagePlanStageList[0]                | Object  | Stage area associated with the usage plan    |
| usagePlanStageList[0].regionCode | Enum    | See [API Gateway Region Enum Code](./enum-code/#api-gateway-region) |
| usagePlanStageList[0].apigwServiceId | String  | API Gateway service ID     |
| usagePlanStageList[0].apigwServiceName      | String  | API Gateway service name     |
| usagePlanStageList[0].stageId        | String  | Stage ID                |
| usagePlanStageList[0].stageName      | String  | Stage name                |
| usagePlanStageList[0].stageUrl       | String  | Stage URL               |
| usagePlanStageList[0].stageCustomDomainList   |List  |Area for the list of stage custom domain   |
| usagePlanStageList[0].stageCustomDomainList[0].customDomain   |String  |Custom domain   |
| usagePlanStageList[0].stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
| usagePlanStageList[0].usagePlanId    | String  | Usage plan ID              |
| usagePlanStageList[0].usagePlanName  | String  | Usage plan name              |


### Connect Stage to Usage Plan
- Associates a stage with the usage plan.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### Disconnect Stage from Usage Plan
- Disassociates the stage associated with the usage plan.
- If an API Key connected to the stage exists, the stage cannot be disassociated.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| DELETE |  /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId} |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

### List Usage Plans Associated with Stage
- Retrieves the list of usage plans associated with the stage.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET |  /v1.0/appkeys/{appKey}/usage-plans/stages/{stageId} |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "usagePlanList": [
    {
      "appKey": "{appKey}",
      "usagePlanId": "{usagePlanId}",
      "usagePlanName": "Basic",
      "usagePlanDescription": "It's for Basic User",
      "rateLimitRequestPerSecond": 10,
      "quotaLimitPeriodUnitCode": "DAY",
      "quotaLimit": 100,
      "createdAt": "2021-11-02T02:26:44.087Z",
      "updatedAt": "2021-11-02T02:26:44.087Z"
    }
  ]
}
```

| Field                                         | Type       | Description                                                |
| ------------------------------------------ | -------- | ------------------------------------------------- |
| paging                                     | Object   | Paging area                                            |
| paging.page                                | Integer  | Current page                                            |
| paging.limit                               | Integer  | Count per page                                         |
| paging.totalCount                          | Integer  | Total count                                            |
| usagePlanList                              | List     | Usage plan list area                                      |
| usagePlanList[0]                           | Object   | Usage plan area                                         |
| usagePlanList[0].appKey                    | String   | AppKey                                            |
| usagePlanList[0].usagePlanId               | String   | Usage plan ID                                         |
| usagePlanList[0].usagePlanName             | String   | Usage plan name                                         |
| usagePlanList[0].usagePlanDescription      | String   | Usage plan description                                         |
| usagePlanList[0].rateLimitRequestPerSecond | Integer  | Limit on the number of requests per second                                        |
| usagePlanList[0].quotaLimitPeriodUnitCode  | Enum     | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| usagePlanList[0].quotaLimit                | Integer  | Request quota per quota period unit                                |
| usagePlanList[0].createdAt                 | DateTime | Usage plan creation date and time                                       |
| usagePlanList[0].updatedAt                 | DateTime | Usage plan modification date and time                                       |

## API Key Subscription

### List API Key Subscriptions
- Retrieves the list of stage and usage plan connected with API Key.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/subscriptions |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apiKeyId | String | Required | N/A | N/A | API Key ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |
| stageUrl | String | Optional | N/A | N/A | Stage URL filter condition |

#### Response

[Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "paging": {
        "limit": 10,
        "page": 1,
        "totalCount": 1
    },
    "subscribedStageAndUsagePlanList": [
        {
            "subscriptionId": "{subscriptionId}",
            "subscriptionStatus": "APPROVAL",
            "apiKeyId": "{apiKeyId}",
            "apigwServiceName": "test api gateway",
            "stageId": "{stageId}",
            "stageName": null,
            "stageUrl": "kr1-example.api.nhncloudservice.com",
            "stageCustomDomainList": [],
            "usagePlanId": "{usagePlanId}",
            "usagePlanName": "Basic",
            "usagePlanDescription": "It's for Basic User",
            "rateLimitRequestPerSecond": 10,
            "quotaLimitPeriodUnitCode": "DAY",
            "quotaLimit": 100
        }
    ]
}
```

| Field                                                           | Type      | Description                                                |
| ------------------------------------------------------------ | ------- | ------------------------------------------------- |
| paging                                                       | Object  | Paging area                                            |
| paging.page                                                  | Integer | Current page                                            |
| paging.limit                                                 | Integer | Count per page                                         |
| paging.totalCount                                            | Integer | Total count                                            |
| subscribedStageAndUsagePlanList                              | List    | Area for the list of the stage and the usage plan connected with API key                |
| subscribedStageAndUsagePlanList[0]                           | Object    | Area for the stage and the usage plan connected with API key                |
| subscribedStageAndUsagePlanList[0].subscriptionId            | String  | Subscription ID                                     |
| subscribedStageAndUsagePlanList[0].subscriptionStatus        | Enum    | See [API Key Subscription Status Enum Code](./enum-code/#api-key-subscription-status)              |
| subscribedStageAndUsagePlanList[0].apiKeyId                  | String  | API Key ID                                        |
| subscribedStageAndUsagePlanList[0].apigwServiceName          | String  | API Gateway service name                                |
| subscribedStageAndUsagePlanList[0].stageId                   | String  | Stage ID                                           |
| subscribedStageAndUsagePlanList[0].stageName                 | String  | Stage name                                           |
| subscribedStageAndUsagePlanList[0].stageUrl                  | String  | Stage URL                                          |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList   |List  |Area for the list of stage custom domain   |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].customDomain   |String  |Custom domain   |
| subscribedStageAndUsagePlanList[0].stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
| subscribedStageAndUsagePlanList[0].usagePlanId               | String  | Usage plan ID                                         |
| subscribedStageAndUsagePlanList[0].usagePlanName             | String  | Usage plan name                                         |
| subscribedStageAndUsagePlanList[0].usagePlanDescription      | String  | Usage plan description                                         |
| subscribedStageAndUsagePlanList[0].rateLimitRequestPerSecond | Integer | Limit on the number of requests per second                                        |
| subscribedStageAndUsagePlanList[0].quotaLimitPeriodUnitCode  | Enum    | See [Usage Plan > Quota Period Unit Enum Code](./enum-code/#usage-plan-quota-period-unit) |
| subscribedStageAndUsagePlanList[0].quotaLimit                | Integer | Request quota per quota period unit                                |


### List API Keys Subscribing to a Stage in the Usage Plan
- Retrieves the list of API Keys connected to the stage of the usage plan.
- If there are multiple request query parameters, a list that satisfies all conditions is returned.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |
| apiKey | String | Optional | N/A | N/A | Primary or Secondary API Key filter condition |
| apiKeyId | String | Optional | N/A | N/A | API Key ID filter condition |
| apiKeyName | String | Optional | N/A | N/A | API Key name filter condition. The starting string of the API Key name must match.  |
| apiSubscriptionStatus | Enum | Optional | N/A | APPROVAL | See [API Key Subscription Status Enum Code](./enum-code/#api-key-subscription-status) |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 1
  },
  "apiSubscriptionList": [
    {
      "subscriptionId": "{subscriptionId}",
      "subscriptionStatus": "APPROVAL",
      "subscriptionDescription": null,
      "stageId": "{stageId}",
      "usagePlanId": "{usagePlanId}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "createdAt": "2021-08-27T04:53:57.000Z",
      "updatedAt": "2021-09-10T00:26:03.000Z"
    }
  ]
}
```

| Field                                             | Type       | Description                                   |
| ---------------------------------------------- | -------- | ------------------------------------ |
| paging                                         | Object   | Paging area                               |
| paging.page                                    | Integer  | Current page                               |
| paging.limit                                   | Integer  | Count per page                            |
| paging.totalCount                              | Integer  | Total count                               |
| apiSubscriptionList                            | List     | Subscription information list area      |
| apiSubscriptionList[0]                         | Object   | Subscription information area      |
| apiSubscriptionList[0].subscriptionId          | String   | Subscription ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | See [API Key Subscription Status Enum Code](./enum-code/#api-key-subscription-status) |
| apiSubscriptionList[0].subscriptionDescription | String   | Subscription description                                |
| apiSubscriptionList[0].stageId                 | String   | Stage ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | Usage plan ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key name                           |
| apiSubscriptionList[0].createdAt               | DateTime | Subscription creation date and time                              |
| apiSubscriptionList[0].updatedAt               | DateTime | Subscription modification date and time                              |


### Subscribe to API Key (Connect API Key)
- Connects the requested API Key list to the stage of your usage plan.
- Only the connected API Key will succeed in API Key authentication, and the usage limit of the usage plan will be applied.
- API Keys connected to the same stage in different usage plans cannot be connected.

#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[Request Body]
```json
{
  "apiKeyIdList": [
    "{apiKeyId}"
  ]
}
```

| Name                        | Type      | Required | Default value | Valid range        | Description                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiKeyIdList              | List  | Required    | N/A  | Max. 100 items       | API Key ID list area                                        |
| apiKeyIdList[0]           | String  | Required    | N/A  | N/A       | API Key ID                                        |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "apiSubscriptionList": [
    {
      "subscriptionId": "{subscriptionId}",
      "subscriptionStatus": "APPROVAL",
      "subscriptionDescription": null,
      "stageId": "{stageId}",
      "usagePlanId": "{usagePlanId}",
      "apiKeyId": "{apiKeyId}",
      "apiKeyName": "User1 API Key",
      "createdAt": "2021-11-03T02:53:21.775Z",
      "updatedAt": "2021-11-03T02:53:21.775Z"
    }
  ]
}
```

| Field                                             | Type       | Description                                   |
| ---------------------------------------------- | -------- | ------------------------------------ |
| apiSubscriptionList                            | List     | Subscription information list area                          |
| apiSubscriptionList[0]                         | Object   | Subscription information area                        |
| apiSubscriptionList[0].subscriptionId          | String   | Subscription ID                                |
| apiSubscriptionList[0].subscriptionStatus      | Enum     | See [API Key Subscription Status Enum Code](./enum-code/#api-key-subscription-status) |
| apiSubscriptionList[0].subscriptionDescription | String   | Subscription description                                |
| apiSubscriptionList[0].stageId                 | String   | Stage ID                              |
| apiSubscriptionList[0].usagePlanId             | String   | Usage plan ID                            |
| apiSubscriptionList[0].apiKeyId                | String   | API Key ID                           |
| apiSubscriptionList[0].apiKeyName              | String   | API Key name                           |
| apiSubscriptionList[0].createdAt               | DateTime | Subscription creation date and time                              |
| apiSubscriptionList[0].updatedAt               | DateTime | Subscription modification date and time                              |


### Unsubscribe from API Key (Disconnect API Key)
- Disconnects the requested API Key list from the stage of your usage plan.
- Disconnected API Key fails API Key authentication, causing API calls to fail. 

#### Request

[URI]

| Method  | URI |
| --- | --- |
| DELETE | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[Request Body]
```json
{
  "apiSubscriptionIdList": [
    "{apiKeyId}"
  ]
}
```

| Name                        | Type      | Required | Default value | Valid range        | Description                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| apiSubscriptionIdList             | List  | Required    | N/A  | Max. 100 items       | Subscription ID list area                                        |
| apiSubscriptionIdList[0]             | String  | Required    | N/A  | N/A       | Subscription ID                                        |

#### Response

[Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```


### Change Usage Plan of API Key
- You can only change to a different usage plan associated with the selected stage.
- When the usage plan is changed, the usage of the API Key request quota is initialized.
    - If you change to a usage plan with a quota period unit of 'day' or 'month', the usage of the connected API Key request quota is maintained. If you change to a usage plan with a lower request quota limit, your usage may be exceeded. 
    - If you change to a usage plan with a quota period unit of 'None', the usage of the connected API Key request quota is initialized.
  
#### Request

[URI]

| Method  | URI |
| --- | --- |
| POST | /v1.0/appkeys/{appKey}/usage-plans/{usagePlanId}/stages/{stageId}/subscriptions/{subscriptionId}/change-usage-plan |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| usagePlanId | String | Required | N/A | N/A | Usage plan ID |
| stageId | String | Required | N/A | N/A | Stage ID |
| subscriptionId | String | Required | N/A | N/A | Subscription ID |

[Request Body]
```json
{
  "changeUsagePlanId": "{usagePlanId}"
}
```

| Name                        | Type      | Required | Default value | Valid range        | Description                                                |
| ------------------------- | ------- | ----- | --- | ------------ | ------------------------------------------------- |
| changeUsagePlanId            | String  | Required    | N/A  | N/A       | ID of the usage plan to change                                        |

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

## Statistics

### Query by Stage Resource
- Retrieves statistics data for each resource during the query period.


#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/services/{apigwServiceId}/stages/{stageId}/metrics |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| stageId | String | Required | N/A | N/A | Stage ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | Required | N/A | N/A | Statistics query start date and time |
| endTime | DateTime | Required | N/A | N/A | Statistics query end date and time |
| page | Integer | Optional | 1 | N/A | Page |
| limit | Integer | Optional | 10 | Max. 1000 | Count per page |

* The search period set by the startTime and endTime fields must be within the last 90 days.
* Enter the stageTime, endTime fields in ISO8601 format date string format. 
    * UTC notation: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC-based time offset notation: yyyy-MM-dd'T'HH:mm:ss±hh:mm


#### Response

[Response]
```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "paging": {
    "limit": 10,
    "page": 1,
    "totalCount": 2
  },
  "data": [
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "GET",
      "successCount": 31,
      "failCount": 18,
      "status2xxCount": 29,
      "status3xxCount": 2,
      "status4xxCount": 18,
      "status5xxCount": 0,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 35,
      "networkOutboundByte": 26059
    },
    {
      "uriPattern": "/members/{memberId}",
      "httpMethodType": "POST",
      "successCount": 20,
      "failCount": 2,
      "status2xxCount": 18,
      "status3xxCount": 0,
      "status4xxCount": 0,
      "status5xxCount": 2,
      "statusEtcCount": 0,
      "avgResponseTimeMs": 129,
      "networkOutboundByte": 3032
    }
  ],
  "metricsLatestUpdatedAt": "2021-11-29T08:50:57.000Z"
}
```

|Field                                   |Type      |Description                                         |
|-------------------------------------|--------|----------------------------------------------|
|paging                               |Object  | Paging area                                     |
|paging.page                          |Integer | Current page                                    |
|paging.limit                         |Integer | Count per page                                 |
|paging.totalCount                    |Integer | Total count                                     |
|data                                 |List    | Area for statistics data list by resource                      |
|data[0]                              |Object    | Area for statistics data by resource                      |
|data[0].uriPattern                   |String  | Resource path or path pattern                         |
|data[0].httpMethodType               |Enum  | See [HTTP Method Type Enum Code](./enum-code/#http-method-type)                             |
|data[0].successCount                 |Long    | Number of API call successes (response HTTP status code is 2xx, 3xx) |
|data[0].failCount               |Long    | Number of API call failures (response HTTP status code is 4xx, 5xx) |
|data[0].status2xxCount               |Long    | Number of API calls with response HTTP status code 2xx |
|data[0].status3xxCount               |Long    | Number of API calls with response HTTP status code 3xx |
|data[0].status4xxCount               |Long    | Number of API calls with response HTTP status code 4xx |
|data[0].status5xxCount               |Long    | Number of API calls with response HTTP status code 5xx |
|data[0].statusEtcCount               |Long    | Number of API calls with response HTTP status code other than 2xx, 3xx, 4xx, 5xx |
|data[0].avgResponseTimeMs            |Long    | Average API response time (ms) |
|data[0].networkOutboundByte          |Long    | Total outbound network bytes (bytes) |
|metricsLatestUpdatedAt         | DateTime | Statistics data last updated date                             |


### Query by API Key
- Retrieves daily statistics by API Key.


#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/apikeys/{apiKeyId}/metrics |

[Path Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| apigwServiceId | String | Required | N/A | N/A | API Gateway service ID |
| apiKeyId | String | Required | N/A | N/A | API Key ID |

[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| startTime | DateTime | Required | N/A | N/A | Statistics query start date and time |
| endTime | DateTime | Required | N/A | N/A | Statistics query end date and time |

* The search period set by the startTime and endTime fields must be within the last 90 days.
* Enter the stageTime, endTime fields in ISO8601 format date string format.
    * UTC notation: yyyy-MM-dd'T'HH:mm:ssZ
    * UTC-based time offset notation: yyyy-MM-dd'T'HH:mm:ss±hh:mm

#### Response

[Response]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "data": {
    "kr1-{apigwServiceId}-member.api.nhncloudservice.com": {
      "stageName": "member",
      "stageUrl": "kr1-{apigwServiceId1}-member.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 8
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    },
    "kr1-{apigwServiceId}-billing.api.nhncloudservice.com": {
      "stageName": "billing",
      "stageUrl": "kr1-{apigwServiceId}-billing.api.nhncloudservice.com",
      "stageCustomDomainList": [],
      "apiKeyMetricsTimeSeries": {
        "callCount": [
          {
            "dateTime": 1635346800000,
            "count": 13
          },
          {
            "dateTime": 1635433200000,
            "count": 0
          }
        ]
      }
    }
  },
  "metricsLatestUpdatedAt": "2021-11-29T08:50:57.000Z",
  "timeUnit": "ONE_DAYS"
}
```

|Field                                   |Type      |Description                                         |
|-------------------------------------|--------|----------------------------------------------|
|data                                 |Object  | API Key statistics data area                         |
|data.{requestApigwEndpoint}          |Object  | Area for statistics by API call endpoint                |
|data.{requestApigwEndpoint}.stageName                    |String    | Stage name            |
|data.{requestApigwEndpoint}.stageUrl                     |String    | Stage URL |
|data.{requestApigwEndpoint}.stageCustomDomainList   |List  |Area for the list of stage custom domain   |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].customDomain   |String  |Custom domain   |
|data.{requestApigwEndpoint}.stageCustomDomainList[0].createdAt   |DateTime  |When custom domain is connected    |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries      |Object    | Area for API Key statistics by aggregation time unit|
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount               |List    | API call count statistics list area |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0]               |Object    | API call count statistics area |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].dateTime   |Long    | Statistics time (Unix time format) |
|data.{requestApigwEndpoint}.apiKeyMetricsTimeSeries.callCount[0].count      |Long    | Total number of API calls during statistics time |
|metricsLatestUpdatedAt         | DateTime | Statistics data last updated date                             |
|timeUnit          |Enum    | [Statistics Data Time Unit Enum Code](./enum-code/#statistics-data-time-unit) See ONE_DAYS |


* Daily statistics data is aggregated into time data at 00:00:00 for each day.


### Query Top 10 Services
- You can view a list of the top 10 API Gateway services and their cumulative statistics based on the number of total API calls, number of failed API calls, and average response time.


#### Request

[URI]

| Method  | URI |
| --- | --- |
| GET | /v1.0/appkeys/{appKey}/metrics/top-services |


[QueryString Parameter]

| Name | Type | Required | Default value | Valid range | Description |
| --- | --- | --- | --- | --- | --- |
| lastDays | Integer | Optional | 7 | 1~30 | Days in query period (current day included)  |
| order | Enum | Optional | CALL_COUNT | CALL_COUNT,FAIL_CALL_COUNT,AVG_RESPONSE_TIME | [Statistics > Sort Top10 Services by](./enum-code/#statistics-sort-top-10-services-by)|


#### Response

[Response]

```json
{
        "header": {
            "isSuccessful": true,
            "resultCode": 0,
            "resultMessage": "SUCCESS"
        },
        "data": [
            {
                "rank": 1,
                "apigwServiceId": "{apigwServiceId1}",
                "apigwServiceName": "apigwservice-1",
                "status2xxCount": 100,
                "status3xxCount": 0,
                "status4xxCount": 0,
                "status5xxCount": 0,
                "statusEtcCount": 0,
                "callCount": 100,
                "failCallCount": 0,
                "successCallCount": 100,
                "avgResponseTimeMs": 6,
                "networkOutboundByte": 31202
            },
            {
                "rank": 2,
                "apigwServiceId": "apigwServiceId2",
                "apigwServiceName": "apigwservice-2",
                "status2xxCount": 50,
                "status3xxCount": 0,
                "status4xxCount": 0,
                "status5xxCount": 0,
                "statusEtcCount": 0,
                "callCount": 50,
                "failCallCount": 0,
                "successCallCount": 50,
                "avgResponseTimeMs": 8,
                "networkOutboundByte": 19220
            }
            ... 
        ],
        "metricsLatestUpdatedAt": "2023-07-19T02:21:08.000Z"
    }
```

| Field | Type | Description |
| --- | --- | --- |
|data | Object | Top 10 service statistics data area |
|data[0].rank | Integer  | Rank number |
|data[0].apigwServiceId | String | API Gateway service ID |
|data[0].apigwServiceName | String | API Gateway service name |
|data[0].successCount | Long | Number of API call successes (response HTTP status code is 2xx, 3xx) |
|data[0].failCount | Long | Number of API call failures (response HTTP status code is 4xx, 5xx) |
|data[0].status2xxCount | Long | Number of API calls with response HTTP status code 2xx |
|data[0].status3xxCount | Long | Number of API calls with response HTTP status code 3xx |
|data[0].status4xxCount | Long | Number of API calls with response HTTP status code 4xx |
|data[0].status5xxCount | Long | Number of API calls with response HTTP status code 5xx |
|data[0].statusEtcCount | Long | Number of API calls with response HTTP status code other than 2xx, 3xx, 4xx, 5xx |
|data[0].avgResponseTimeMs | Long | Average API response time (ms) |
|data[0].networkOutboundByte | Long | Total outbound network bytes (bytes) |
|metricsLatestUpdatedAt | DateTime | Statistics data last updated date |