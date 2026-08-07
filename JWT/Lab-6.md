**JWT || Lab#6 || JWT authentication bypass via kid header path traversal**

<img width="762" height="560" alt="image" src="https://github.com/user-attachments/assets/bf464653-d560-4efb-81ce-3cf071376242" />

Goal of this lab is to forge a JWT that gives you access to the admin panel at /admin, then delete the user carlos.

Credentials → wiener:peter

Lets open the lab and login

<img width="852" height="380" alt="image" src="https://github.com/user-attachments/assets/2b8e4112-ac38-421c-8fcb-cb6f74d28dc9" />

Lets check this traffic in Burpsuite

<img width="1000" height="412" alt="image" src="https://github.com/user-attachments/assets/0e5f04c0-d450-4fa8-a365-1a7c0d7e82d3" />

Lets move this traffic to Repeater

Lets check if this user can access admin panel or not

<img width="1000" height="377" alt="image" src="https://github.com/user-attachments/assets/0300d55c-729d-44db-8276-158490021ffe" />

It seems admin panel is there but it is accessible by administrator only.

Lets check JWT

<img width="1000" height="492" alt="image" src="https://github.com/user-attachments/assets/68522545-ee46-415d-8daf-09149412a0dd" />

In JSON Web Token tab we have Header, Payload and Signature. In Payload we have regular user (wiener) in Subject. We need to find a way where we can change Administrator user in Subject.

Lets check it kid parameter is vulnerable to path traversal

The Header of the JWT may contain a kid parameter which stands for Key-ID. This parameter helps the sever to identify which key is used to verify the signature. 

Now, the JWT does not define a structure of kid. So it could be any arbitrary string.

Now if kid parameter is vulnerable to path traversal, an attacker can get the server to use any arbitrary file on the server's file system as the key to sign the token.

So if we could get the server to use a file that we already know as the signing key, then we could alter the token as much as we want and sign it with the key that is equal to the content of the file. 

Now, this attack will only work if the application is using a symmetric algorithm (HS256, HS384, HS512)

Lets change the subject to administrator

<img width="735" height="602" alt="image" src="https://github.com/user-attachments/assets/a56aec58-a5e9-4d65-8e4b-83c2b4a62c50" />

Now we will try to sign the token with /dev/null file. 

/dev/null is called the null device file and its present in most linux system. It is an empty file that returns an empty string. 

So we are going to try to get the application to use the content of this file as a key which is an empty string. 

Now we don't know where this file is located in the server.

<img width="732" height="762" alt="image" src="https://github.com/user-attachments/assets/dc5263a1-651c-4ef2-8fa8-60d3461a6bd1" />

Now we need to sign the JSON web token with the empty string. We can use a base64 encoded null byte. 

AA== is the base64 encoded version of a null byte.

<img width="1000" height="545" alt="image" src="https://github.com/user-attachments/assets/41dc0baf-2554-43b3-8bdc-d2b4a119094f" />

Lets go to JWT Editor

<img width="1000" height="673" alt="image" src="https://github.com/user-attachments/assets/975ed0f5-b757-4ba7-86f8-6780ceca1193" />

We will replace AA== with the "K" value

<img width="1000" height="204" alt="image" src="https://github.com/user-attachments/assets/b1cad9db-467b-4575-949d-c7e367693eda" />

We will use this key to sign out token.

<img width="1000" height="665" alt="image" src="https://github.com/user-attachments/assets/bd60c284-5fe4-4a87-9154-db6f92f8ed2b" />

Now, when we forward this traffic and try to access the admin panel, if the KID parameter is vulnerable to LFI, it will fetch the content of this file /dev/null which is null byte and then it will use it to sign the token. 

Once it sign the token, it will compare the signature that is generated in the backend with the signature that is in JWT token which we have used to sign using null byte.

Both signatures are going to match and it will allow us to access the admin panel.

Now, lets change the endpoint to /admin and forward the traffic

<img width="1000" height="459" alt="image" src="https://github.com/user-attachments/assets/6384f792-4159-4e99-9451-9ef07b41c089" />

We got a 200 OK response. It seems we have access to admin portal.

To solve the lab, we have to delete carlos user.

Lets put the path in the endpoint to delete the user carlos.

<img width="1000" height="457" alt="image" src="https://github.com/user-attachments/assets/746408e8-bf70-4bf6-b1df-f08d579213d5" />

We got a 320 response. Lets follow redirection

<img width="1000" height="449" alt="image" src="https://github.com/user-attachments/assets/46645425-0316-47cd-ae22-e5b771f58199" />

Carlos user is deleted

<img width="957" height="382" alt="image" src="https://github.com/user-attachments/assets/ef7aa7ee-25d4-4978-9773-5aa0a9be39c5" />

And lab is solved !!!!
