## Application Service > API Gateway > Release Note

### January 25, 2022
#### Feature Updates 
* Changed so that, if there is a plugin set in the resource path, the plugin set in the resource path is added when a sub-method is created.
* Added Public APIs related to resource creation and modification.
  * [Create Resource Paths and Methods API]()
  * [Create Resource Methods API]()
  * [Modify Plugins in Resource Path API]()
  * [Modify Resource Method Information and Plugins API]()
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
    * For more details, refer to [the Console Guide> Backend Endpoint URL Override](./console-guide/#backend-endpoint-url-override).
* Added the function of revising the current Stage setup with verification of deployment history and deployment history Stage setup
    * For more details, refer to [the Console Guide > Stage Deployment History](./console-guide/#stage-deployment-history).
* Changed the statistical data generation cycle
    * For more details, refer to [the Console Guide > Note on Statistical Data](./console-guide/#note-on-statistical-data)'s explanation on  statistical data generation cycle.
* Added Import Resource and Export Stage functions with Swagger file
    * With Swagger file, you can import resource.
    * You can export Stage Resource with Swagger file.
    * For more details, refer to [the Console Guide > Resource > Import Resource](./console-guide/#import-resource)and [the Console Guide > Export Stage](./console-guide/#export-stage).
* Supports the JSON Web Key Set URI of JWT plug-in
    * For more details, refer to [the Console Guide > Authentication > JWT](./console-guide/#authentication-jwt).

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
