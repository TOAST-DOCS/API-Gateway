## Application Service > API Gateway > Overview

## Overview of API Gateway 

API Gateway makes it easy to create and deploy user APIs. 
Useful plugins are provided to restrict access, control traffic, and prevent message falsification.  


## Main Features  

#### Create, Deploy, and Manage APIs  
- It gets easier to manage and deploy resources and methods of user APIs. 
- User APIs are exposed via front-end points. 
- Not every user API server requires API gateway, which is cost-effective.  

#### Plugins of Various Kinds  
- A variety of plugin functions are provided, including restricted access (IP ACL), prevention of message falsification (HMAC, JWT), and traffic control (throttling). 
- With API Gateway plugins, developers can focus mainly on developing business logics.  

#### Various Statistical Data  
- Data regarding API call counts, statistics on each HTTP response code, average speed of response, and traffic volume of network, are provided.     

## Service Flow of API Gateway  

![[Figure1] Structure of Service](http://static.toastoven.net/prod_apigateway/overview/service_flow.png)

Clients can call URL of user's endpoint API server via URL of API Gateway domain. 

It only takes plugin configuration on API gateway console to add such features as control of access and authentication.  
