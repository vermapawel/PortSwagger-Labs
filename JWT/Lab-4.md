**JWT || Lab#4 || JWT authentication bypass via jwk header injection**

<img width="787" height="592" alt="image" src="https://github.com/user-attachments/assets/dce67401-9ebb-4a01-88d3-8d0ef5747bea" />

Goal of this lab is to forge a JWT that gives you access to the admin panel at /admin, then delete the user carlos.

Credentials → wiener : peter

Lets start the lab and login

<img width="750" height="302" alt="image" src="https://github.com/user-attachments/assets/b8e11e7b-f899-4b8b-82ea-f7c14b00187d" />

Lets check this traffic in Burp suite

<img width="1000" height="404" alt="image" src="https://github.com/user-attachments/assets/8392e800-862b-4d0a-ba05-e2bc1e83f7ed" />

Lets move this traffic to Repeater

<img width="1000" height="489" alt="image" src="https://github.com/user-attachments/assets/4bf71587-5e38-4ee0-b356-969bab3b2877" />

Lets try to access the admin panel.

<img width="1000" height="384" alt="image" src="https://github.com/user-attachments/assets/4af49f7b-98e3-4be6-9636-4e4c4778d67c" />

It seems admin panel is allowed only for administrator. 

Now, lets check if the application accepts an arbitrary JWK header / JWK Injection (Public-key)

JWK stands for JSON Web Key. Its a JSON object that represents Cryptographic key. It is in the header of the JWT

First we need to generate a public key pair.

<img width="1000" height="705" alt="image" src="https://github.com/user-attachments/assets/600b3a85-6296-4b42-ab94-7527c2ce54f7" />

<img width="1000" height="145" alt="image" src="https://github.com/user-attachments/assets/03febd58-0b98-42dd-9742-299741e5b47e" />

New key is generated.

Next, in the Repeater, we will replace weiner with administrator in JSON Web Token tab.

<img width="761" height="812" alt="image" src="https://github.com/user-attachments/assets/54ac0f79-6e26-4ea5-a37b-e3ccd0487521" />

<img width="757" height="817" alt="image" src="https://github.com/user-attachments/assets/9d2c6b1f-ba28-4797-b514-0dca4454ec8d" />

<img width="817" height="316" alt="image" src="https://github.com/user-attachments/assets/076404ba-e1da-436d-acc1-f1660acb078e" />

It will add the JWK parameter in the Header. It also contains Public key in JWK parameter.

<img width="912" height="762" alt="image" src="https://github.com/user-attachments/assets/56ffead0-8743-45b0-84eb-48b52e25e60e" />

It will use the equivalent private key in order to sign this token. So when the application receive this token, it will use the Public key to check if the signature is valid. 

Now, we will change the endpoint to admin and forward the traffic.

<img width="1000" height="507" alt="image" src="https://github.com/user-attachments/assets/6beda3aa-60ae-42cf-a199-dd9140ef059c" />

We got a 200 OK response. It seems we are logged in as administrator.

To solve the lab, we have to delete carlos user.

Lets put the path in the endpoint to delete the user carlos.

<img width="1000" height="518" alt="image" src="https://github.com/user-attachments/assets/3ba98e43-3b72-4a38-8f7e-fe6df1b3cad0" />

We got a 320 response. Lets follow redirection

<img width="1000" height="390" alt="image" src="https://github.com/user-attachments/assets/e43fae67-fb6d-4c81-a2eb-cc17266eab96" />

Carlos user is deleted

<img width="1000" height="285" alt="image" src="https://github.com/user-attachments/assets/f9495b60-d14c-4f38-9074-2425309d4cb4" />

Lab is solved !!!
