**Information disclosure || Lab#4 || Authentication bypass via information disclosure**

<img width="792" height="415" alt="image" src="https://github.com/user-attachments/assets/b9072d56-c554-42ff-a884-90260ea52230" />

Goal of this lab is to delete the user carlos. We have our credentials provided.

Lets start the lab and check some products.

<img width="997" height="477" alt="image" src="https://github.com/user-attachments/assets/24175318-829f-4013-9fb7-c1fb47427ad0" />

Lets check this traffic in Burp suite

<img width="1000" height="384" alt="image" src="https://github.com/user-attachments/assets/15df6e4d-ad1c-4394-9c0f-b02a3ed47ddb" />

Lets move this traffic to Repeater

<img width="1000" height="456" alt="image" src="https://github.com/user-attachments/assets/7d167af4-3ce9-4702-8164-a108f3867004" />

Lets user TRACE HTTP method and check.

TRACE method is used for debugging purposes. TRACE method should never be enabled in the production as this contain sensitive information.

<img width="1000" height="546" alt="image" src="https://github.com/user-attachments/assets/204a9a66-660f-4d36-ae6b-7dbad8b826a9" />

We can see X-Custom-IP-Authorization is a custom header and it looks like it picks the IP address of the user. Lets copy this header and send this traffic to repeater.

We will add this custom header in the request and add local host. Also we will use GET method

<img width="1000" height="506" alt="image" src="https://github.com/user-attachments/assets/59fbd5cf-b056-4cc0-9420-e2dd762277d3" />

We got a 200 OK response. We can see the path of the admin page.

The application is giving access to the admin page because it thinks that traffic is coming locally from the server.

Lets visit the /admin page

<img width="1000" height="466" alt="image" src="https://github.com/user-attachments/assets/59d15a12-a0fd-4434-87e1-439cc579400e" />

We are at the admin page and we have access to delete the user.

To solve the lab we need to delete the carlos user.

Lets copy the path **/admin/delete?username=carlos**

<img width="1000" height="576" alt="image" src="https://github.com/user-attachments/assets/1dc78a04-f63c-41f9-8dae-9b8fb99072e6" />

We got a 302 response. Lets follow redirection

And this time we don't see carlos user

<img width="1000" height="631" alt="image" src="https://github.com/user-attachments/assets/828699eb-2d17-491d-9fed-9baeefd4a684" />

And lab is solved

<img width="956" height="325" alt="image" src="https://github.com/user-attachments/assets/0580204b-429b-423b-ab70-9f4bfec6bb53" />

