**Server Side Request Forgery**

Lets say there is a user who is accessing a shopping application. The application is hosted in an internal network that is protected by a Firewall. The application itself is public facing so that anyone on the internet can access the application. 

This application take use of other services to work. These services can be internal to the organization or external to the organization (3rd party).

<img width="1000" height="509" alt="image" src="https://github.com/user-attachments/assets/3fa4565b-7f29-45fa-b156-2ad2ec09328b" />

For security reasons, the only software that is allowed to communicate with these services is this application. So if the user will try to communicate directly with 3rd Party system or the servers inside the Internal network, will be denied.

There is a Trust relationship between Application and any of the Internal Services and there trust relationship between Application and 3rd Party System. 

Lets say there is a user who want to buy an item on the Application. User click on Check Stock button to check if the item is in stock or not. 

This initiates a request to the service that is responsible to check it items are in stock or not. 

Now this request if a POST request and the service that is responsible to check it items are in stock or not is called stock.shop.net work on port 8080 and has a parameter called productID. 

Now, the server check and replied to the request that there are 58 Units left.

<img width="1000" height="461" alt="image" src="https://github.com/user-attachments/assets/d1266436-dd2f-4f84-8369-fa897e1ef3a9" />

Now, the user clicks on the Buy button which initiates which initiates a request to the 3rd party system which is responsible for the sales of the product.

Lets say 3rd Party System is AWS services and it has a parameter productID which takes the product id of the item that user wants to buy. It processes the request and send back to the shopping application of successful purchase.

<img width="1000" height="439" alt="image" src="https://github.com/user-attachments/assets/0cd70415-c749-4a8d-9a27-8e6585975b66" />

Now, if these URLs that are responsible to take the request are user controllable and not properly validated there could be risk.

User controllable means the user has the ability to change the URL sent to the servers.

<img width="1000" height="482" alt="image" src="https://github.com/user-attachments/assets/4d00cb61-d9a1-41ee-b9e3-7b3648aa29dd" />

Now, an attacker can intercept the request that was for Stock check and modify it to request Admin page of the server. 

As there is a trust relationship between the application and the server, the Admin page of the internal server get displayed.

<img width="1000" height="455" alt="image" src="https://github.com/user-attachments/assets/4758525f-641c-4b97-9048-639b35fde2ff" />

So, SSFR is a vulnerability that occurs when an application is fetching a remote resource without first validating the user supplied URL.

This allows an attacker to force server to make connections on behalf of the attacker and target systems that are behind Firewalls. 

So if any parameter is sending an IP address and a URL in the parameter, it should be checked for SSRF vulnerability.

**Types of SSRF**

1. **Regular / In Band** :- In this, the attacker can temper the URL and the response to the URL is displayed back to the Application. In last example where we have altered the URL for Stock check to get Admin page. That Admin page get displayed on the Application itself.

2. **Blind / Out-of-Band** :- Here the application does not  reply to the request directly. Lets say we have requested for the Admin page, application is vulnerable to SSRF and exploit was successful, but the respond will not displayed back directly on the Application.







