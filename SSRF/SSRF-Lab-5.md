**SSRF || Lab#5 : SSRF with filter bypass via open redirection vulnerability**

<img width="852" height="432" alt="image" src="https://github.com/user-attachments/assets/b779dde8-3a78-4a69-890d-446e00178f1e" />

Vulnerable parameter → Stock Check functionality.

Goal of the lab is to change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos

Lets open the Lab

<img width="892" height="637" alt="image" src="https://github.com/user-attachments/assets/7b6368ee-f015-463b-92c8-0c1830b9c374" />

When we click on Check stock, it will display how many units are available in that particular store for example, 700 units are available in London store.

Also there is a new feature to see Next product.

Lets intercept these traffic in Burp suite

<img width="1100" height="312" alt="image" src="https://github.com/user-attachments/assets/69a41e16-dfa2-434d-812e-fc63682bf4dc" />

<img width="1100" height="323" alt="image" src="https://github.com/user-attachments/assets/7a17a81e-efb7-4417-8d2b-5d88a7015dbe" />

Lets move these traffic to Repeater

<img width="1100" height="413" alt="image" src="https://github.com/user-attachments/assets/b61205ba-cb2c-40df-860d-74a226c5cf7c" />

This is URL encoded. Lets decode it.

stockApi=/product/stock/check?productId=1&storeId=1

So this is not a URL. Its using path through the application to get the stock result.

Lets see if we can access localhost

<img width="1100" height="451" alt="image" src="https://github.com/user-attachments/assets/6f227346-6580-4be1-992a-74404eed3cf6" />

We got an error.

Lets check the other traffic

<img width="1100" height="294" alt="image" src="https://github.com/user-attachments/assets/ecfe8afd-0a7e-4ce1-a114-1be0e43eca52" />

Here we can see that there is a path variable which redirect to a different path. Lets Follow Redirection

<img width="1100" height="466" alt="image" src="https://github.com/user-attachments/assets/c681d5b8-4d6c-46ef-a51e-c28455d465b6" />

So this path variable is redirecting to productId parameter.

Lets check if the path variable is vulnerable to open redirection vulnerability.

Lets try to visit www.google.com page with the help of path parameter.

<img width="1097" height="467" alt="image" src="https://github.com/user-attachments/assets/0f63fefe-94d3-4f9b-b56c-9256271759e0" />

Lets go to Follow Redirection

<img width="1100" height="422" alt="image" src="https://github.com/user-attachments/assets/5fe2323c-4a30-45ba-915b-3c3e5599e840" />

And we are at the google page.

So this path variable is definitely vulnerable to Open redirection

Now, from the lab description we know that path of admin is http://192.168.0.12:8080/admin

We will use this path variable to get to the admin account

stockApi=/product/nextProduct?currentProductId=1&path=http://192.168.0.12:8080/admin

<img width="1100" height="590" alt="image" src="https://github.com/user-attachments/assets/60f0c391-c6f3-4d98-80f3-1dcbf3733e70" />

We need to URL encode it.

<img width="1100" height="493" alt="image" src="https://github.com/user-attachments/assets/30f9c238-2f42-4b00-86ec-18ca3d61d935" />

And we got the admin page.

To solve the lab, we need to delete carlos user.

Lets find the user carlos

<img width="1100" height="534" alt="image" src="https://github.com/user-attachments/assets/4a670ac1-ec02-41ed-b3a0-2676d3a71c0c" />

http://192.168.0.12:8080/admin/delete?username=carlos

Lets use this path to delete the user

stockApi=/product/nextProduct?currentProductId=1&path=http://192.168.0.12:8080/admin/delete?username=carlos

<img width="1100" height="485" alt="image" src="https://github.com/user-attachments/assets/c9fcf7f5-2389-4e9e-b439-2aa00805ce02" />

We got a 200 OK response and there is no user carlos. Lets validate

<img width="1100" height="531" alt="image" src="https://github.com/user-attachments/assets/04bb0de0-3057-41e5-ab4c-220229d18537" />

And lab is solved

<img width="927" height="301" alt="image" src="https://github.com/user-attachments/assets/44da711c-439c-4208-b02b-3ba5eaf94fcc" />
