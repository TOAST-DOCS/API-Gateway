## Application Service > API Gateway > Firewall Policy Settings for API Gateway Clients 

### Firewall Policy Settings for API Gateway Clients 

If you use a firewall (Network ACL) when clients call the APIs provided through API Gateway, you must set up a firewall policy for the API Gateway VIP for normal communication. 
If firewall policy settings are missing for the API Gateway VIP, API calls might fail based on the results of the domain query. 
API Gateway is available without any processing if clients do not separately manage firewalls.

#### API Gateway VIP Information

| VIP | Port | 
| --- | --- | 
| 180.210.64.24<br>180.210.65.24<br>180.210.64.224<br>180.210.65.224<br>117.52.123.41 | 80, 443 |

Refer to the API Gateway VIP information to set up the following firewall (Network ACL).

* Departure: Client IP calling APIs provided through API Gateway 
* Destination: Full List of API Gateway VIPs
* Port: 80, 443 
* Communication policy: Allow 

> **[Note]** Changing the API Gateway VIP 
> * The API Gateway VIP list is subject to change after prior notice. 
> * You must read the announcement when you make the change and then set the firewall policy for the changed VIP.