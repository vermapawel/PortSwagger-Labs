**JWT || Lab#5 || JWT authentication bypass via jku header injection**

<img width="790" height="592" alt="image" src="https://github.com/user-attachments/assets/9a998641-8d92-45d1-a722-f62838a0528f" />

Goal of this lab is to forge a JWT that gives you access to the admin panel at /admin, then delete the user carlos.

Credentials → wiener:peter

Lets start the lab and login

<img width="732" height="322" alt="image" src="https://github.com/user-attachments/assets/fe9062f0-ee96-4c3d-bf4b-cec34aae0a52" />

Lets check this traffic in Burpsuite

<img width="1000" height="429" alt="image" src="https://github.com/user-attachments/assets/6a4f7edd-3cf8-443c-a266-7b9031cb26f8" />

Lets move this traffic to Repeater

<img width="1000" height="524" alt="image" src="https://github.com/user-attachments/assets/90e41b4f-df91-4ed1-836c-7c1725aa18b6" />

In JSON Web Token tab we have Header, Payload and Signature. In Payload we have regular user (wiener) in Subject. We need to find a way where we can change Administrator user in Subject.

Lets check if the application accepts any arbitrary JKU parameter.

JKU stands for JSON Web-key set URL. It includes a URL from which the server fetch a key to verify the signature.

If the application allows us to enter any JKU parameter and it accepts it without any verification, we can add a URL in the parameter which includes our own key set, and use that key set to sign the token.

Now, this attack will only work if the application is using a symmetric algorithm (HS256, HS384, HS512)

**Step 1:- Generate our RSA key**

<img width="1000" height="680" alt="image" src="https://github.com/user-attachments/assets/82716e4a-8777-4363-a621-a7b8deff46fe" />

<img width="1000" height="205" alt="image" src="https://github.com/user-attachments/assets/539ec9eb-3e87-4d03-b407-e0790917f468" />

**Step 2:- Add the Public key in the exploit server**

Lets copy the Public key

<img width="935" height="347" alt="image" src="https://github.com/user-attachments/assets/5f527c55-d743-45fc-b6b1-032168fa3099" />

Lets go to the exploit sever

<img width="922" height="400" alt="image" src="https://github.com/user-attachments/assets/c9f5b6e2-ed2a-4749-a83c-5df6bb163e95" />

```
{
"keys":[key]
}
```

<img width="1000" height="304" alt="image" src="https://github.com/user-attachments/assets/922bd02d-061c-400a-91b3-3e8f09bd61c9" />

**Step 3:- Modify the JWT to include JKU parameter and the subject administrator.**

Lets go to Repeater, JSON Web Token

<img width="982" height="467" alt="image" src="https://github.com/user-attachments/assets/c0844354-1ba9-4376-a6ba-4f4af89f007a" />

We need to replace the "kid" with our newly created token

<img width="1000" height="302" alt="image" src="https://github.com/user-attachments/assets/05d5435a-8486-4cef-9ee3-89ee3b856a4e" />

Also we have added jku in the Header and put our exploit server address.

<img width="762" height="317" alt="image" src="https://github.com/user-attachments/assets/7f20d08a-ae7a-4dde-a242-24441c7a33da" />

We have also changed the subject to administrator.

**Step 4:- Sign the token**

<img width="902" height="477" alt="image" src="https://github.com/user-attachments/assets/a4bcaddd-3ac7-4e94-8561-e26c1a8d928a" />

<img width="752" height="456" alt="image" src="https://github.com/user-attachments/assets/6b7f44c0-2cb0-4e46-9e44-59dc8ecef899" />

Now, lets change the endpoint to /admin and forward the traffic

<img width="1000" height="536" alt="image" src="https://github.com/user-attachments/assets/e312ccde-c8cc-4b44-8c49-dc5f5f6624d7" />

We got a 200 OK response. It seems we have access to admin portal.

To solve the lab, we have to delete carlos user.

Lets put the path in the endpoint to delete the user carlos.

<img width="1000" height="416" alt="image" src="https://github.com/user-attachments/assets/6324df53-99dd-4ec4-ae42-98905d2bd32e" />

We got a 320 response. Lets follow redirection

<img width="1000" height="447" alt="image" src="https://github.com/user-attachments/assets/30b04838-bb05-4815-b6d1-edecb525a7c0" />

Carlos user is deleted

<img width="1000" height="329" alt="image" src="https://github.com/user-attachments/assets/ef883049-7f1e-4d98-8e4d-f39fc996acf7" />

Lab is solved !!!
