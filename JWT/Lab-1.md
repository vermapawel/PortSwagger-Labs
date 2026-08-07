**JWT || Lab#1 || JWT authentication bypass via unverified signature**

<img width="782" height="565" alt="image" src="https://github.com/user-attachments/assets/be47ba8b-3b1a-44a0-89e4-ed3f3dd8ca7f" />

Goal of this lab is to modify the session token to gain access to /admin panel and delete carlos user. 

Credentials → Wiener : peter

Lets install JWT Editor extension from BApp Store in the Burpsuite

<img width="1000" height="276" alt="image" src="https://github.com/user-attachments/assets/5f772a87-90bc-4bb7-9311-7911bef63ad0" />

After installing go to Installed tab and make sure JWT Editor is checked.

<img width="856" height="515" alt="image" src="https://github.com/user-attachments/assets/7f2bc6fe-a106-4e8e-bb60-23528af45cc2" />

Lets open the lab and login

<img width="807" height="332" alt="image" src="https://github.com/user-attachments/assets/d3e1d320-2a0c-4075-be7c-e20d0dbf269e" />

Lets check this traffic in Burp suite

<img width="1000" height="398" alt="image" src="https://github.com/user-attachments/assets/7aa5f74e-bea6-4102-8c0b-e8e86e66a891" />

Any traffic that contains JWT token is highlighted in Green.

We can see that this traffic contains a csrf token, user credentials on the request. In the response it has JWT token under session cookie.

Lets move my-account traffic to Repeater

<img width="1000" height="524" alt="image" src="https://github.com/user-attachments/assets/c9d0800a-7810-4677-ad92-cdc6cdd5dc51" />

Testing for JWT Vulnerability

1. Check if the JWT signature is verified

Lets alter the JWT token and check

<img width="1000" height="418" alt="image" src="https://github.com/user-attachments/assets/64829f81-e6bb-4560-996f-95496b31936e" />

We have added few characters in the token and still we got 200 OK 

Now, we will try to identify more privileged user.

Lets check if there is an admin panel

<img width="1000" height="455" alt="image" src="https://github.com/user-attachments/assets/11d77496-c873-4c1c-bda1-5a85501cd047" />

Admin panel is there but only available to Administrator

Now, In the Payload of the JWT, lets change the username to administrator

<img width="1000" height="624" alt="image" src="https://github.com/user-attachments/assets/a74427c4-8165-46c4-890a-9805f905f5a4" />

Lets send this traffic

<img width="1000" height="474" alt="image" src="https://github.com/user-attachments/assets/4ce4c620-2fa9-4660-9e08-9cd55b3e90fc" />

And we got the Admin panel. Lets copy the entire token and put in session cookie in the browser

<img width="1000" height="655" alt="image" src="https://github.com/user-attachments/assets/2868a43c-be69-4bd0-af26-7737da124c08" />

And we got access of Admin panel. 

To solve the lab we have to delete carlos user

<img width="1000" height="343" alt="image" src="https://github.com/user-attachments/assets/8ca26d06-c3ec-4522-847d-dca92c93de24" />

Lab is solved !!!
