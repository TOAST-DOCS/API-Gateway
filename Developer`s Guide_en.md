Upcoming Products &gt; API Gateway &gt; Developer's Guide
---------------------------------------------------------

> ※ This document contains information on alpha development in process. For those who are interested in use, please contact **support@cloud.toast.com**.

This document describes API Gateway structure, functions and instruction.

Service Structure
-----------------

<img src="http://static.toastoven.net/prod_apigateway/img_11.png" />

Plug-in Motion Structure
------------------------

<img src="http://static.toastoven.net/prod_apigateway/img_12.png" />

Plug-in added to Domain will operate to all API included in Domain. Likewise, plug-in added to Endpoint will operate when API call for Endpoint is conducted.

Functions
---------

#### Domain management

One Domain reacts to one Domain URL pointing at the target server. Domain can be created, edited and deleted. Also, plug-in for Domain can be set up.

<img src="http://static.toastoven.net/prod_apigateway/img_13.png" width="560" height="345" />

Click \[API Gateway\] &gt; \[API Setting\] in the web console to access Domain management screen.

<img src="http://static.toastoven.net/prod_apigateway/img_14.png" />

#### Endpoint management

Endpoint means Endpoint that can access API. Therefore, one Endpoint reacts to one API. Endpoint can be created, edited and deleted. Also, plug-in for Endpoint can be added, edited and deleted.

<img src="http://static.toastoven.net/prod_apigateway/img_15.png" />

In Domain list, click \[Setting\] &gt; \[Endpoint\] in the far right side of Domain to be managed, and access Endpoint management screen.

<img src="http://static.toastoven.net/prod_apigateway/img_16.png" />

    Even if URI is same, if HTTP Method is different, it is different Endpoint.

#### API statistics

API statistics show usage of API call and average response time occurred in Domain the user registered. If you click one from Domain list, you can check statistics on certain Domain in more detail through a chart and statistics per Endpoint.

<img src="http://static.toastoven.net/prod_apigateway/img_17.png" />

<img src="http://static.toastoven.net/prod_apigateway/img_18.png" />

Click \[API Gateway\] &gt; \[Dashboard\] in the web console to access statistics screen.

<img src="http://static.toastoven.net/prod_apigateway/img_19.png" />

### Instructions

#### Create Domain

1. Click on \[New Domain\] button and move to Domain creation screen.

<img src="http://static.toastoven.net/prod_apigateway/img_20.png" />

2.Fill in Domain setting form and click on \[Save\] button to create Domain.

<img src="http://static.toastoven.net/prod_apigateway/img_21.png" />

#### Edit Domain

1. From Domain list, click on \[Setting\] &gt; \[Domain\] button in the right side of Domain to be edited, and move to Domain editing screen.

<img src="http://static.toastoven.net/prod_apigateway/img_22.png" />

2. Change Domain setting and click on \[Save\] button to save.

<img src="http://static.toastoven.net/prod_apigateway/img_23.png" />

#### Delete Domain

1. From Domain list, click on \[Setting\] &gt; \[Delete\] button in the right side of Domain to be deleted, and Domain delete popup will appear.

<img src="http://static.toastoven.net/prod_apigateway/img_24.png" />

2. Confirm Domain to be deleted once more time, and delete by inserting Domain name.

<img src="http://static.toastoven.net/prod_apigateway/img_25.png" />

> Notice : Deleted Domain cannot be restored. When trying to delete, the user confirms by inserting the name of Domain.

#### Create Endpoint

1.From Endpoint list, click on \[New Endpoint\] button, and add new Endpoint.

<img src="http://static.toastoven.net/prod_apigateway/img_26.png" />

2. Fill in the blanks then click on \[Save\] button in the right to create Endpoint.

<img src="http://static.toastoven.net/prod_apigateway/img_27.png" />

#### Edit Endpoint

1. From Endpoint list, click on \[Edit\] button in the right side of Endpoint to be edited, and start editing.

<img src=""http://static.toastoven.net/prod_apigateway/img_28.png" />

2. Edit the setting then click on \[Save\] button in the right to save.

<img src=""http://static.toastoven.net/prod_apigateway/img_29.png"/>

#### Delete Endpoint

1.From Endpoint list, click on \[Delete\] button in the right side of Endpoint to be deleted, and delete.

<img src=""http://static.toastoven.net/prod_apigateway/img_30.png"/>

#### Add Endpoint Plugin

1. Click on \[+\] button in the right side of Endpoint to add Plugin then click on Plugin you want from the Plugin list appeared.

<img src="http://static.toastoven.net/prod_apigateway/img_31.png" />

2. Fill in the Plugin setting form then click on \[Save\] button in the right to save.

<img src="http://static.toastoven.net/prod_apigateway/img_32.png" />

#### Edit Endpoint Plugin

1. Click on Plugin for edit and open editing screen.

<img src="http://static.toastoven.net/prod_apigateway/img_33.png" />

2. Edit the setting and click on \[Save\] button in the right to save.

<img src="http://static.toastoven.net/prod_apigateway/img_34.png" />

#### Delete Endpoint Plugin

1. Click on Plugin for delete and open editing screen.

<img src="http://static.toastoven.net/prod_apigateway/img_35.png" />

2. Click on \[Delete\] button in the right to delete.

<img src="http://static.toastoven.net/prod_apigateway/img_36.png" />

### Domain Plugin

#### Access Control

-   IP ACL : IP based Access Control

#### Authentification

-   HMAC

-   JWT (JSON Web Token)

#### Quota Limit

-   Usage Quota : API use limit per hour

### Endpoint Plugin

-   Mock : Response Mock

-   Cache : API result Cache


