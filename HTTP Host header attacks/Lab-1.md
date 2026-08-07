**HTTP Host header attacks || Lab#1 || Basic password reset poisoning**

<img width="775" height="427" alt="image" src="https://github.com/user-attachments/assets/4983f4ea-69c3-419d-93d0-45f7a386ff34" />

Goal of this lab is to login as Carlos account. 

Credentials: wiener : peter

Lets start the lab

<img width="780" height="336" alt="image" src="https://github.com/user-attachments/assets/4df245de-88b5-4a1d-aa2e-dafb1ac34a98" />

There is a Forgot password functionality. Lets check how it work

Its asking for username or email address. Let put username

<img width="887" height="242" alt="image" src="https://github.com/user-attachments/assets/d573ced2-6165-4650-ad02-673807342da2" />

<img width="881" height="297" alt="image" src="https://github.com/user-attachments/assets/8e996609-e9e2-494e-bd39-4b3e8d52dc33" />

A password reset link has been sent to email address. Lets check

<img width="1000" height="330" alt="image" src="https://github.com/user-attachments/assets/bb4b28f8-8dad-4baa-963c-7f65dfb096bc" />

Go to Email client. 

We can see there is a password reset link

<img width="1000" height="330" alt="image" src="https://github.com/user-attachments/assets/c818e3a3-a8c5-4be9-bcf5-91caa55a42ab" />

Now, lets try again with user carlos

Lets go to Forgot Password functionality and put username as carlos

<img width="857" height="281" alt="image" src="https://github.com/user-attachments/assets/5a90e16b-7345-47e6-b269-30f43a968e91" />

<img width="842" height="252" alt="image" src="https://github.com/user-attachments/assets/80572184-2977-40a7-bf0f-f3e13cbd8f00" />

A password reset link is sent to carlos email address that we dont have access. 

Lets check this traffic in Burpsuite

<img width="1000" height="387" alt="image" src="https://github.com/user-attachments/assets/99626052-cb42-4b27-abf1-196b0abad0b9" />

This is a POST request. It has username parameter and csrf token. 

Lets move this traffic to Repeater

<img width="850" height="747" alt="image" src="https://github.com/user-attachments/assets/a375e7c8-3685-4067-865c-cfe565f88c52" />

Now, what we can do here is, we can send a password reset link to carlos, but instead the link having the hostname of the application, we can change the hostname to attacker controlled server. 

Lets go to our exploit server

<img width="1000" height="319" alt="image" src="https://github.com/user-attachments/assets/b58e1436-765e-4730-ba64-4b2d89b77bd3" />

Copy the hostname without https, and replace it with the Host of the request

<img width="1000" height="551" alt="image" src="https://github.com/user-attachments/assets/28f4a503-5780-4845-9a7b-dc2bdc1c8b07" />

A reset password link is sent to the carlos email address. However if this application link is vulnerable to Host header injection attack, the password reset link will be 

exploit-0aed006e031f231a82b6a091017d00ad.exploit-server.net/forgot-password/password-reset-token

Now, in the lab description, its mentioned that carlos will check any random link in his email. Here we have replaced the genuine password reset link to our exploit sever.

<img width="780" height="322" alt="image" src="https://github.com/user-attachments/assets/bb5141de-0f73-4a45-94ad-0965ca4663e3" />

Go to access log

<img width="1000" height="179" alt="image" src="https://github.com/user-attachments/assets/bf19612d-4793-46c9-947c-520c15cdd2bb" />

We can see that there is a log where we get the forget password token. We will use this token to reset the password for carlos.

https://0aab001f03f623868229a1430034002a.web-security-academy.net/forgot-password?temp-forgot-password-token=7rqe9pbfq2v57m1d1fiu4sc0n2b64ozh

<img width="1000" height="347" alt="image" src="https://github.com/user-attachments/assets/c8331068-c716-4d7d-a0a1-88cb888ee219" />

We have changed the password. Lets login

<img width="1000" height="470" alt="image" src="https://github.com/user-attachments/assets/8d43ce3d-fe95-4eb9-b168-67ae29df8743" />

And lab is solved !!!

This is the Host Header Injection attack. It can occur if the website can blindly trust the Host header that is given in the request and uses it to generate the password link. This attack is called password reset poisoning.








