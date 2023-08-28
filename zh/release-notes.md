## Application Service > API Gateway > Release Note

### August 29, 2023
#### Feature Updates 
* Added the request restriction policy 
    * This is a feature that lets you set IP ACL and request number limit for each request path variable or request header value.
    * For more information, see [Console Guide > Request Restriction Policy](./console-guide/#request-restriction-policy_1).
* Added the custom domain feature
    * This is a feature that lets you specify a domain by setting the prefix of the stage domain to a value specified by the user.
    * For more information, see [Console Guide > Custom Domain](./console-guide/#custom-domain).
    * Custom domain-related field names in API responses have been changed from stageAliasDomainList to stageCustomDomainList.
* Added the API Key import/export feature 
    * You can import an API Key or export a registered API Key via a CSV file.
    * For more information, see [Console Guide > Import API Key](./console-guide/#import-api-key) and [Console Guide > Export API Key](./console-guide/#export-api-key).
* Create an API Key with a custom Primary/Secondary API Key 
    * You can create API key with a custom Primary/Sencodary API key.
    * For more information, see [Console Guide > Create API Key](./console-guide/#create-api-key).
* Added Top 10 Service Query Statistics API 
    * You can view a list of the top 10 API Gateway services and their cumulative statistics based on the number of total API calls, number of failed API calls, and average response time.
    * For more information, see [API v1.0 Guide > Top 10 Service Query](./api-guide-v1.0/#query-top-10-services).

### July 26, 2022
#### Feature Updates
* New region opened in Korea (Pyeongchon)
* Changed the range of ports available for backend endpoints.
    * Previous: 80, 443, 5000~12000
    * Current: 80, 443, 10000~12000

### May 24, 2022
#### Feature Updates 
* Added the access log feature
    * This is a feature that lets you store API Gateway's access logs in the Log & Crash Search service. For more information, refer to [Access Log](./console-guide/#access-log).


### January 25, 2022
#### Feature Updates
* Made modifications so that, if there is a plugin set in the resource path, the plugin set in the resource path is added when a child method is created.
* Added Public APIs related to resource creation and modification.
    * [Create Resource Paths and Methods API](./api-guide-v1.0/#create-resource-paths-and-methods)
    * [Create Resource Methods API](./api-guide-v1.0/#create-resource-methods)
    * [Modify/Delete Resource Path Plugins API](./api-guide-v1.0/#modifydelete-resource-path-plugins)
    * [Modify/Delete Resource Method Information and Plugins API](./api-guide-v1.0/#modifydelete-resource-method-information-and-plugins)
* Added statistics API response fields
    * Added the metricsLatestUpdatedAt field to the response of the statistics API, which indicates the last updated date and time of statistics data.
    * Added the timeUnit field to the response of the Query by API Key API, which indicates the time unit of statistics data.
    * For more information, see [API v1.0 Guide > Statistics > Query by Stage Resource](./api-guide-v1.0/#query-by-stage-resource), [API v1.0 Guide > Statistics > Query by API Key](./api-guide-v1.0/#query-by-api-key).
* Added restriction on the range of ports available for pre-call API's endpoints and backend endpoints.
    * Available port numbers: 80, 443, 5000-12000


### November 23, 2021
#### Feature Updates 
* API Gateway Public API support
    * You can use the API Gateway service through the API. For more information, refer to the [API v1.0 Guide](./api-guide-v1.0/).

### August 24, 2021
#### Feature Updates 
* Added API document
    * Refer to [Console Guide > API Document](./console-guide/#api-document_1) for details.

### July 6, 2021
#### Feature Updates  
* Added a plugin that adds request query string parameter
    * For more details, see [Console Guide > Plugin > Add Request Query String Parameter](./console-guide/#add-request-query-string-parameter).

### June 29, 2021
#### Feature Updates
* Added API key feature and usage plan
    * For more information, see [Console Guide > Usage Plan](./console-guide/#usage-plan), [Console Guide > API Key](./console-guide/#api-key_1), [Console Guide > Stage > API Key](./console-guide/#api-key).

### May 25, 2021
#### Feature Updates
* In the stage path, the function of backend endpoint URL redefinition was added
    * For more details, refer to [Console Guide> Backend Endpoint URL Override](./console-guide/#backend-endpoint-url-override).
* Added the function of revising the current Stage setup with verification of deployment history and deployment history Stage setup
    * For more details, refer to [Console Guide > Stage Deployment History](./console-guide/#stage-deployment-history).
* Changed the statistical data generation cycle
    * For more details, refer to [Console Guide > Note on Statistical Data](./console-guide/#note-on-statistical-data)'s explanation on  statistical data generation cycle.
* Added Import Resource and Export Stage functions with Swagger file
    * With Swagger file, you can import resource.
    * You can export Stage Resource with Swagger file.
    * For more details, refer to [Console Guide > Resource > Import Resource](./console-guide/#import-resource)and [Console Guide > Export Stage](./console-guide/#export-stage).
* Supports the JSON Web Key Set URI of JWT plug-in
    * For more details, refer to [Console Guide > Authentication > JWT](./console-guide/#authentication-jwt).

### March 23, 2021
#### Feature Updates
* Pre-call API plugin feature added
    * See [Console Guide > Pre-Call API](./console-guide/#pre-call-api) for more details.
* Request number limit plugin feature added
    * See [Console Guide > Request Number Limit ](./console-guide/#request-number-limit) for more details.
* Authentication > JWT plugin feature added
    * See [Console Guide > Authentication > JWT](./console-guide/#authentication-jwt) for more details.
* Context Variables ${request.clientIp} added
    * See [Console Guide > Context Variables](./console-guide/#context-variables) for more details.

### February 23, 2021
#### New service release 
* API Gateway is a product that allows easy integration and management of APIs.
* Additional functions can be added without changing/deploying the code of the service.
* You can view the API statistical indexes through the dashboard and utilize them as the index for monitoring and API quality.
