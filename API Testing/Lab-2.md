**API Testing || Lab#2 || Exploiting server-side parameter pollution in a query string**

<img width="785" height="552" alt="image" src="https://github.com/user-attachments/assets/5ef59065-13c6-4de3-8ce1-96f438e8f355" />

Goal of this lab is to login as administrator and delete user carlos.

Lets start the lab

<img width="1000" height="460" alt="image" src="https://github.com/user-attachments/assets/ce183b2e-a325-4a2d-a486-c7296641cfdc" />

This is a login page. However we don't have credentials given this time. But we know that one of the usernames is administrator. 

Lets check

<img width="512" height="252" alt="image" src="https://github.com/user-attachments/assets/4042f0b7-7159-4ba5-9c32-5ce4718c090d" />

It seems a password reset link is sent to the email address. Lets check this traffic in Burpsuite

<img width="1000" height="459" alt="image" src="https://github.com/user-attachments/assets/fa554e6f-5f15-43aa-b7c0-ead5a9d92c9c" />

Lets move this traffic to Repeater

<img width="1000" height="469" alt="image" src="https://github.com/user-attachments/assets/07b65d62-1c0d-416e-ac00-976f190e1c50" />

Now, lets put a wrong username and check

<img width="1000" height="470" alt="image" src="https://github.com/user-attachments/assets/22d16dc8-fd3c-40c2-a7a1-a44e956b04de" />

We got an error invalid username.

Lets put # after administrator. URL encode the # and forward the traffic.

<img width="1000" height="470" alt="image" src="https://github.com/user-attachments/assets/33c53781-4ede-4c3a-a36c-3e658cd9ccc4" />

We got error Field not specified. 

Lets put filed and put some random value and check

<img width="1000" height="473" alt="image" src="https://github.com/user-attachments/assets/fbeb607a-8fbd-40fd-832e-2f42aa9f77ce" />

Again we got same error. 

Lets put # after aaa. URL encode this as well

<img width="1000" height="505" alt="image" src="https://github.com/user-attachments/assets/e2b5ffb2-8814-43fb-a239-237198945452" />

Again we got same error

Now, there must be some parameter which we are not able to find. Lets brute force it. Move this traffic to Intruder

Add aaa in the position. In the payload section, drop down Add from list and select Server-side variable name.

<img width="1000" height="335" alt="image" src="https://github.com/user-attachments/assets/c84ab444-f224-41f8-a70a-207e1214477b" />

Start attack

<img width="1000" height="402" alt="image" src="https://github.com/user-attachments/assets/4766543c-0a3a-401d-a4a6-fb3f1fc599e7" />

We are looking for 200 status code.

<img width="1000" height="274" alt="image" src="https://github.com/user-attachments/assets/fbdcd346-f5bb-44f2-a3eb-c4d7825510b2" />

However we dont get any 200 status code.

Lets change # to & after administrator. URL encode it start the attack again

<img width="1000" height="427" alt="image" src="https://github.com/user-attachments/assets/4a65c5ee-7b15-4ad6-8f1a-1875b1b6f83b" />

And this time we get two 200 Status code for email and username.

<img width="1000" height="224" alt="image" src="https://github.com/user-attachments/assets/4710442a-763d-4e6c-99cf-decaad2ce304" />

Lets go to Repeater and put email in the parameter and check

<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/1e674b3d-a873-41ed-93dc-5532c065651d" />

Now, lets check the reset password request

<img width="1000" height="350" alt="image" src="https://github.com/user-attachments/assets/72313f2e-3165-444b-99c4-1d9d242d7043" />

This is a javascript file. Here we can see that there is a variable reset_token which hold the reset token value. Its path is also mentioned.

/forgot-password?reset_token=&lt;token&gt;

Lets use reset_token in the parameter and check 

<img width="1000" height="434" alt="image" src="https://github.com/user-attachments/assets/7e1375bb-3fe9-48bb-814f-2852a57824c9" />

And we got a reset token. 

As per the password reset javascript file, there was a path mentioned 

/forgot-password?reset_token=qxu2vpqum92ct336i21qyyhjs2jbl6oo

Lets put this path in the URL

<img width="1000" height="374" alt="image" src="https://github.com/user-attachments/assets/629c6ae5-54b1-40e4-a800-5951022941f3" />

Its giving me to change the password of the administrator. Lets change it and login as administrator

<img width="1000" height="325" alt="image" src="https://github.com/user-attachments/assets/0a5cfa48-bf13-4467-936a-974a4016bc36" />

We have logged in as administrate and have access to admin panel

To solve the lab we have to delete carlos user

<img width="1000" height="236" alt="image" src="https://github.com/user-attachments/assets/c466333e-4a50-4664-9d4d-6c9c2da01700" />

And lab is solved !!!

<img width="1000" height="348" alt="image" src="https://github.com/user-attachments/assets/0c624fca-cc32-409c-84d2-3f36d7c05b16" />
