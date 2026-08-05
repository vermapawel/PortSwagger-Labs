**Cross-Origin Resource Sharing (CORS) | Complete Guide**

<img width="1000" height="549" alt="image" src="https://github.com/user-attachments/assets/d8b84c86-fa3e-4885-a335-527b0b370735" />

**Same Origin Policy (SOP)**

Its a security mechanism that is enforced by browser to control data between web applications. 

If there is a banking application and a shopping application, by default the interaction between these two applications is limited. 

The banking application is able to make request to the shopping application but cannot read the response from the application. It is implemented by default in all browsers. So we cannot read data from an another application by default.

<img width="1000" height="463" alt="image" src="https://github.com/user-attachments/assets/d0419988-e1fc-4a20-9b27-b0b8f075e5e4" />

Lets say a user is visiting a shopping application for the 1st time. The shopping application contains a script that automatically makes a request to the banking application which we have logged in with the same browser and ask for the banking information such as account number, balance or personal information.

If there is no such thing like Same Origin Policy, the banking website will handover these application to the script.

So if there is no SOP, all the applications can attack each other and ask for the data. To prevent that all the browser has this policy built-in.

SOP does not prevent writing between web applications, it prevent reading between web applications.

So the script in the shopping application can still make request to the banking application for personal details, however when the browser sees that request, it will check the origin of the request.

It will check from where the request is originated from. In this case the request is originated from a domain, lets say shopping.com and that domain is different from the banking application domain, lets say bank.com. So browser will reject that request because these two application has different domains.

<img width="1000" height="384" alt="image" src="https://github.com/user-attachments/assets/f450f31d-5f76-4899-bf7b-12c4d7e00dc2" />

Now, two URLs will have same origin when the protocol (scheme), hostname (domain) and ports are same.

<img width="1000" height="406" alt="image" src="https://github.com/user-attachments/assets/8c114193-2956-4ebf-9228-c86dc176aad0" />

<img width="1000" height="261" alt="image" src="https://github.com/user-attachments/assets/a27276b3-55e6-47f5-a0f4-2003c36eadce" />

**Cross-Origin Resource Sharing (CORS)**

Its a mechanism that allows resources on a server to be requested from an another domain.

In some cases we want to allow Cross Origin Interaction. Many web applications need to communicate with its sub-domain or 3rd party websites. So to make this communication happen, these website use CORS protocol.

Lets say there are two domains. domain-a is a shopping application and domain-b is analytic application.

domain-a need to access some resources from domain-b. To let that happen, domain-b have to configure CORS rules in its web application.

<img width="1000" height="466" alt="image" src="https://github.com/user-attachments/assets/9bf4a75f-ee8d-4b0e-9bbd-dfd694cd70c3" />

CORS uses HTTP header to define origins that are allowed to access the website.

<img width="1000" height="200" alt="image" src="https://github.com/user-attachments/assets/fb127f85-f2db-429d-a6e0-b313ca141c50" />

**Access-Control-Allow-Origin**

<img width="1000" height="507" alt="image" src="https://github.com/user-attachments/assets/a0cb5a21-1269-4832-84d2-afefa8b2ef0a" />

This response header identify the browser if the origin has permission to access the resources of a specific website

Lets say there are two domains. domain-a is a shopping application and domain-b is analytic application.

Shopping application needs to read data from analytic application. It will send a request. In the request, origin domain is mentioned domain-a.com. Host will be domain-b.com as we need data from this domain.

Now, if domain-b has CORS rules configured to allow domain-a.com to fetch data, it will respond with Access-Control-Allow-Origin header indicating browser that the application is allowed to read the request. So Access-Control-Allow-Origin header will have domain-a.com.

How to configure Access-Control-Allow-Origin

<img width="962" height="215" alt="image" src="https://github.com/user-attachments/assets/b4c43185-b20b-41bf-a2ee-9678e0b908f8" />

1. Access-Control-Allow-Origin: * → It will allow any site on the internet to access the resources. 

2. Access-Control-Allow-Origin: <origin> → It will allow only a single origin to access the resources.
   
3. Access-Control-Allow-Origin: null → Some application wants to whitelist the Null origin

Access-Control-Allow-Origin header allows us to access only public pages in the application.

In order to access authenticated pages we have to use Access-Control-Allow-Credentials header

**Access-Control-Allow-Credentials**

This response header allows credentials such as cookies, authorization headers, TLS client certificate to be included in cross origin request.

<img width="1000" height="521" alt="image" src="https://github.com/user-attachments/assets/39bfd026-1a93-4743-a128-d2957f8e1c2d" />

Lets say domain-a wants to access account details of domain-b. Account details is an authenticated page. domain-a sends a request to domain-b. In the request, origin domain is mentioned domain-a.com. Host will be domain-b.com as we need data from this domain.

In order to access this page, in the response, Access-Control-Allow-Origin header must have domain-a and Access-Control-Allow-Credentials header should be true.

<img width="1000" height="259" alt="image" src="https://github.com/user-attachments/assets/b111f3bf-e2b0-4a09-93bf-93e3b2b56fa4" />

Access-Control-Allow-Credentials: true → Its allowed to pass the credentials in the request.

If Access-Control-Allow-Origin: * (wildcard), then we cannot set Access-Control-Allow-Credentials: true.

<img width="1000" height="473" alt="image" src="https://github.com/user-attachments/assets/63a919e3-dc9c-4cdf-b701-b9ab5a4c7aac" />

Lets say there is a user who logged in to the banking application and stays logged-in. On the other tab he is browsing any other web page, cat-pics.com. 

Now, cat-pics.com is a malicious web site. In the background, it requests account details from the bank.com. 

Bank website has misconfigured CORS rules. It will allow the malicious website to access the account details.

Here the misconfiguration is that, in the response Access-Control-Allow-Origin header has cat-pics.com domain and Access-Control-Allow-Credentials: true. 

CORS Vulnerability is just configuration issue.

<img width="1000" height="404" alt="image" src="https://github.com/user-attachments/assets/f635ba4f-ca7a-4f1e-80bf-8eef748e0939" />

In Access-Control-Allow-Origin: <origin> header we can whitelist one and only one origin. It dose not allow us to whitelist multiple origin. So the only option we have is either whitelist all the origin (*) or whitelist only one origin. 

So we need to find a way to pass these rules and whitelist only selected numbers domains. That's where dynamic generation is used. 

So if we want to trust multiple origins, we have to dynamically inspecting the origin header from the request and deciding if we trust it. Misconfiguration occurs in the logic of the code that decide how we can determine if an origin is trusted by the application.

<img width="1000" height="556" alt="image" src="https://github.com/user-attachments/assets/192eef3a-d61b-4979-afcd-2a2e506e703c" />

1. Simply extracting the origin header from client side input and reflecting it back to the user.

   Lets say domain-a is making a request to domain-b. When domain-b sees the request, it extracts the origin of the request, which is lets say shopping.com and it inserts into Access-Control-Allow-Origin header thereby allowing domain-a to access resources of domain-b.
   
This is equivalent to wildcard character (*) as it will allow all the origin to access the resources. This is because all its doing is the extracting the origin and reflecting it back to the user.

2. Errors parsing Origin headers:-

   Lets say a website bank.com would like to trust all it sub-domain. The code at the backend is inspecting all the request and it give access to those domain that ends with string bank.com. This type of implementation has security issue because an attacker can register a domain that ends with string bank.com for example maliciousbank.com and it will be allowed.
   
So, the vulnerability depends how the developer has put the logic on the application that makes a decision whether an origin is trusted or not.

3. Whitelisting the Null origin value.

   Again, this is equivalent to wildcard character (*) because it an attacker make a malicious script and make it run in sandbox iframe, it will appear as its coming from the origin null and it will be allowed to access the resources.










