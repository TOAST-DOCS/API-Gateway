## Application Service > API Gateway > Overview


## API Gateway Overview

- This service integrates the API endpoints into one by taking up the gateway role for a number of backend endpoint services.
-  Various features including HTTPS communication, authentication, CORS, and request/response processing can be added without changing/deploying any backend endpoint services by utilizing the plugins provided by API Gateway.
- Using the dashboard, you can view different indexes such as the number of API entry requests, average response time, number of responses per HTTP status code group (2xx, 5xx).


## Key Features

1. Flexible API design
    - APIs can be *designed* in API Gateway without changing the backend endpoint service.
    - APIs can be registered in a tree structure for easy *management* of API path and method.
    - Path Variables can be declared and you can utilize them in the path connection and plugin settings of the backend endpoint service.
2. Plugin
    - Plugin lets you add features without changing or deploying the backend endpoint service.
    - You can add plugins flexibly for each API path or for HTTP method.
3. Stage
    - API can be deployed per stage.
    - Backend endpoint services can be set for each stage.
    - Stage lets you configure the API endpoint domain per service and profile, and you can also use them for a number of different purposes.
        - e.g. Dividing stages per service
        - Stage for payment service: kr1-api-billing.apigw.nhncloudservice.com
        - Stage for member service: kr1-api-member.apigw.nhncloudservice.com
        - e.g. Dividing stages per environment
        - Alpha environment stage: kr1-api-alpha.apigw.nhncloudservice.com
        - Service environment stage: kr1-api.apigw.nhncloudservice.com
        
4. Dashboard (stats)
    - Provides statistical indexes including API calls, responses per HTTP status code group (2xx, 3xx, 4xx, 5xx..), and average response time (ms).


## How API Gateway Works

![[Figure 1] How API Gateway works](https://static.toastoven.net/prod_apigateway/v2/apigw-v2-flow.png)
1. Gateway client makes a request by integrating all requests through API Gateway. API Gateway looks for the request and mapped resources.
2. Apply the plugin to the request.
3. Pass the request to the backend endpoint.
4. Pass it to API Gateway of the backend endpoint.
5. Apply the plugin to the response of the backend endpoint. 
6. Pass the response to the gateway client.

## Service Terms 

| Term | Description |
| --- | --- |
| API Gateway Service |  A unit for managing API resources and  stages. |
| Resource | Resources comprise API designs between the  front end (EndUser) and API Gateway services. Resources consist of paths and  HTTP methods. |
| Backend endpoint | Refers to the service to users who are  forwarded with requests received by API Gateway. |
| Stage | A stage of deploying resources. APIs can be deployed per service/environment. |
| Plugin | Additional functions provided by API  Gateway, such as authentication and ACL. |
