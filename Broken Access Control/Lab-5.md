**Broken Access Control ||Lab #5 URL-based access control can be circumvented**

<img width="892" height="377" alt="image" src="https://github.com/user-attachments/assets/46755025-c6c9-430d-941d-6badd009a463" />

Goal of this lab is to delete user carlos

Lets start the lab

<img width="900" height="439" alt="image" src="https://github.com/user-attachments/assets/24612535-825e-4a88-a495-02a57107e602" />

Lets try to access Admin panel.

<img width="900" height="207" alt="image" src="https://github.com/user-attachments/assets/1a0cd309-bd89-413f-8e59-623052e65b41" />

Access is denied.

Lets intercept this traffic in Burp suite.

<img width="900" height="421" alt="image" src="https://github.com/user-attachments/assets/7fb9a288-229c-421e-942c-d319828e7b3a" />

We got a 403 Forbidden response. Lets move this traffic to Repeater

<img width="900" height="465" alt="image" src="https://github.com/user-attachments/assets/1830c22a-2cde-4e3f-a26d-38cbb9f493ee" />

Lets add a non standard header X-Original-URL in the request body

X-Original-URL is a non standard HTTP header that can be used to over-ride the URL in the original request.

<img width="900" height="347" alt="image" src="https://github.com/user-attachments/assets/7aad8b40-b307-4a91-82c0-c5a013691ca1" />

Lets remove /admin from the GET request as we are trying this on the main page.

We have added the header X-Original-URL and put an obvious folder location that doesn't exists on the application.

So this header will override the original location and try to find this directory.

We have got a 404 Not found response, which is a good sign. It means the application supports non standard URL X-Original-URL.

We will put /admin in X-Original-URL forward the request. So it will try to access admin panel.

<img width="900" height="452" alt="image" src="https://github.com/user-attachments/assets/2e93710d-e0c5-439c-8eed-3f8451c90376" />

And we got the admin panel. Right click on Response and select Show response in browser.

<img width="766" height="631" alt="image" src="https://github.com/user-attachments/assets/1e162c87-8a15-444d-b55f-5e2300aa291c" />

Copy the URL and put in the browser.

<img width="900" height="244" alt="image" src="https://github.com/user-attachments/assets/27fa5049-d5d8-4442-9c17-4675ff4c3924" />

Lets delete the user carlos.

<img width="900" height="122" alt="image" src="https://github.com/user-attachments/assets/fea0e157-ea40-48da-87f0-8bf612fe7253" />

We dont have permission to delete any user as we are not admin user. We have just found the admin page but we are still a low privileged user. 

Now, in the last traffic we found /admin/delete?username=carlos

<img width="900" height="448" alt="image" src="https://github.com/user-attachments/assets/ed66138c-d516-4ffd-97ce-c12f4d7c6469" />

Lets put this location in X-Original-URL

<img width="726" height="467" alt="image" src="https://github.com/user-attachments/assets/5786a519-6ddf-4834-ad80-8cd5f035ce33" />

We have put the /admin/delete in the body and as we cannot use parameter here, we will put ?username=carlos in the GET method.

Lets forward this traffic

<img width="900" height="437" alt="image" src="https://github.com/user-attachments/assets/7b73e682-aed6-4e9e-b98b-590ff1b2471c" />

We got a 302 response, Follow redirection.

<img width="900" height="286" alt="image" src="https://github.com/user-attachments/assets/fe604680-ed27-46fa-b2a9-7a6628006af7" />

We got access denied. 

However if we refresh the page we can see that lab is solved

<img width="900" height="270" alt="image" src="https://github.com/user-attachments/assets/311ee604-7d5f-46c2-a231-b1408a1af9c0" />

To confirm lets visit admin page again

<img width="900" height="452" alt="image" src="https://github.com/user-attachments/assets/5884b944-7b36-4a74-b49d-cd50977907c4" />

We don't find anything from keyword carlos.

Lets visit the URL and we don't see carlos user

<img width="900" height="328" alt="image" src="https://github.com/user-attachments/assets/cc2ee4a0-5d36-4d47-b425-105d9063d4c6" />



