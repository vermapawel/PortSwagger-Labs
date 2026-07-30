**Authentication Vulnerabilities - Lab #11 Password reset poisoning via middleware**

<img width="862" height="372" alt="image" src="https://github.com/user-attachments/assets/186e9589-0fe8-44ba-a3f2-b7ec309d3257" />

We have a valid credentials wiener:peter

Lets start the lab

<img width="892" height="502" alt="image" src="https://github.com/user-attachments/assets/e24dc24c-a1a7-49bd-82ec-b3fa07de462c" />

Lets understand how password functionality works

<img width="772" height="360" alt="image" src="https://github.com/user-attachments/assets/1c3be34e-5d22-4f12-95f2-780a26d7a947" />

Click on Forgot password link

<img width="757" height="202" alt="image" src="https://github.com/user-attachments/assets/01556e61-d614-463e-b79c-ee1b665ab6e9" />

Lets move this traffic to Repeater (Traffic 1)

<img width="900" height="338" alt="image" src="https://github.com/user-attachments/assets/7833748e-d671-4a7b-8902-076c0acf2a75" />

A link has been sent to the email address. Go to the exploit server

<img width="900" height="301" alt="image" src="https://github.com/user-attachments/assets/3ba188e4-3986-4e1c-bc0e-9a13dc71b80d" />

<img width="900" height="298" alt="image" src="https://github.com/user-attachments/assets/d9561c68-24db-4903-be44-97bdbaa8f282" />

<img width="900" height="289" alt="image" src="https://github.com/user-attachments/assets/e9b2ed58-0847-4874-89a7-3ff14573e25a" />

Here we got a link to reset the password. Lets click on the link and move this traffic to Repeater

<img width="900" height="257" alt="image" src="https://github.com/user-attachments/assets/3fd7c581-b5a4-48df-9d01-4980e4dc68e0" />

Lets check the password.

<img width="772" height="296" alt="image" src="https://github.com/user-attachments/assets/e83ef22d-a74a-4fb9-9914-085f1172b945" />

Lets move this traffic to Repeater

<img width="900" height="230" alt="image" src="https://github.com/user-attachments/assets/423df375-b641-427a-9273-087d5655147b" />

Now, we have three traffic to look at. 

The first traffic is where we have submitted username for changing the password.

<img width="752" height="537" alt="image" src="https://github.com/user-attachments/assets/5f2a5cec-605a-418d-9a2e-a904f244cf67" />

We can see that the Origin is same.

<img width="900" height="242" alt="image" src="https://github.com/user-attachments/assets/2aa38613-c3b5-4a0d-929f-c7562938096c" />

Lets check if we can add X-Forwarded-Host header on the request or not. 

We will add attacker's host in the X-Forwarded-Host.

<img width="900" height="275" alt="image" src="https://github.com/user-attachments/assets/4ebaa0a2-5b78-4545-9e1f-b748d619952e" />

exploit-0ae6000704b5f6c181de16f3012b009b.exploit-server.net

So, when we add attacker's host in the X-Forwarded-Host, the application will trust that this is the host and it will send email addresses here to reset the password. 

We will change the username to carlos and forward the traffic

<img width="900" height="424" alt="image" src="https://github.com/user-attachments/assets/3e98d47d-026a-49e9-9122-946d29d6b7cc" />

We got a 200 OK response.

So the application sends an email to carlos the change the password and in that email there will be our exploit server link. When carlos will click on the link, we get a log that someone has clicked on this link. 

Lets check

<img width="900" height="591" alt="image" src="https://github.com/user-attachments/assets/8cb5c6aa-81ed-40d9-8e7f-4dd95c6eeed3" />

<img width="900" height="205" alt="image" src="https://github.com/user-attachments/assets/f8378312-87b6-4013-8ccd-9f8f7699aa14" />

We can see that someone from IP 10.0.4.246 clicked the link and we got his forgot-password-token which is 5jghktwubxowmjt0l8n1ohdezxyagifs

Now, we will put this token on the 2nd traffic that we have captured

<img width="900" height="459" alt="image" src="https://github.com/user-attachments/assets/c789dbc9-87f8-4cc0-9a5a-55a6f83b4f9d" />

Its asking us to change the password for carlos. Now we have to set a new password for carlos

Lets put this token on the 3rd traffic that we have captured.

<img width="900" height="452" alt="image" src="https://github.com/user-attachments/assets/856bfa2e-3b26-4232-be1c-6f3dac2dc5ac" />

We have set the carlos password as password. We got a 302 responce. Lets redirect

<img width="900" height="409" alt="image" src="https://github.com/user-attachments/assets/83550a86-dee6-4ffd-9b2c-9b179ae43b14" />

Forward this traffic traffic. We got a 200 response.

As we have set the new password for carlos, lets try to login

<img width="900" height="422" alt="image" src="https://github.com/user-attachments/assets/f0ea0fa9-4668-47b1-851f-1e63a893ed1b" />

We are able to login and lab is solved

<img width="802" height="322" alt="image" src="https://github.com/user-attachments/assets/3cf2c158-0a29-41c9-8c2c-cfff3e96104e" />

