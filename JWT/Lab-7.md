**JWT || Lab#7 || JWT authentication bypass via algorithm confusion**

<img width="790" height="647" alt="image" src="https://github.com/user-attachments/assets/5bfd6962-1f0f-4b98-aa5a-724856d006ab" />

Goal of this lab is to get access to admin panel and delete user carlos

Credentials → wiener : peter

Lets start the lab and login

<img width="861" height="365" alt="image" src="https://github.com/user-attachments/assets/5d1cc7b2-4616-4ab4-b787-6667ac439de3" />

Lets check this traffic in Burpsuite

<img width="1000" height="441" alt="image" src="https://github.com/user-attachments/assets/bb0248a7-f1ee-4ee2-a761-fd88a9dc4907" />

Lets move this traffic to Repeater

<img width="777" height="756" alt="image" src="https://github.com/user-attachments/assets/0114f787-d512-43e0-bcc8-29c3980fadd2" />

In JSON Web Token tab we have Header, Payload and Signature. In Payload we have regular user (wiener) in Subject. We need to find a way where we can change Administrator user in Subject. Also the algorithm that is used here is RS256

Lets check if the application is vulnerable to algorithm confusion.

We identified that the application is using RSA algorithm to sign and verify the JWT. 

We will force the server to use a different algorithm to sign the JWT.

Types of algorithms that we can use to sign the JWT token

1. Symmetric algorithms (also called as private key encryption or signing algorithm) :- Here one key is used for both Signing and verifying the signature of the token.
   
2. Asymmetric algorithms (Public key algorithm):- Here we have two keys. One is used to sign the token (know as the private key) and it should not be accessible to anyone in the public. Other key is used to verify the signature of the token (Public key). It is not meant to be a secret.

Algorithm confusion attacks arises when the application is using a symmetric algorithm (HS256, HS384, HS512)

For this attack to work, there needs to be an implementation flaw where the developer does not properly check if the algorithm that is given in the Header is actually the one that is used by the backend to sign the token. 

So we will confuse the server to use a symmetric algorithm where public key is used for signing and verifying the token. This public key is available for everyone.

Lets change the subject to administrator because we are trying to access the admin panel. Also we will change the algorithm to HS256. 

This is a private key algorithm where one key is used to sign and verify the token.

<img width="767" height="806" alt="image" src="https://github.com/user-attachments/assets/b9811f24-c122-46ea-b37b-f8ec7fb90c41" />

Now we need to find the public key before we sign the token. Some servers expose the public key on standard endpoint like jwks.json endpoint. 

Lets check if we have access to jwks.json endpoint.

<img width="1000" height="457" alt="image" src="https://github.com/user-attachments/assets/772b03c0-2d87-4807-99d3-fbd4f1bfbb2d" />

We have access to jwks.json endpoint and got the public key. 

We can do this in the browser as well.

<img width="995" height="230" alt="image" src="https://github.com/user-attachments/assets/cd7289fd-2f89-4372-bccb-bcfbaeb5fbcd" />

Lets copy the key.

Now we need to sign our token. Go to JWT Editor and create a new RSA key.

<img width="1000" height="728" alt="image" src="https://github.com/user-attachments/assets/37d89c07-5af0-4269-9b4d-2acd7c352dde" />

We will put the public key here.

<img width="1000" height="289" alt="image" src="https://github.com/user-attachments/assets/1070706c-132a-4b71-844c-9798c97e87ed" />

Lets go to the decoder and encode key to base64

<img width="1000" height="262" alt="image" src="https://github.com/user-attachments/assets/6eba2bec-1198-4e3a-b959-c162946305e3" />

This base64 will be used as our symmetric ket. 

Generate a new symmetric key.

Paste the key in "k"

<img width="1000" height="668" alt="image" src="https://github.com/user-attachments/assets/42476181-c8c9-4362-b231-89d01586a77e" />

<img width="1000" height="170" alt="image" src="https://github.com/user-attachments/assets/5e1dc70c-535c-49dd-944d-14a0027db699" />

Now, go back to Repeater

Here we have changed the alg to HS256 and sub to administrator.

Now we have to sign the token with the public key.

<img width="1000" height="696" alt="image" src="https://github.com/user-attachments/assets/827422ea-70a3-4cce-b30a-952bd2125725" />

Now, lets change the endpoint to /admin and forward the traffic.

<img width="1000" height="447" alt="image" src="https://github.com/user-attachments/assets/442d5876-0d3c-4430-8178-696a0ce75970" />

We have access to Admin panel. 

To solve the lab we need to delete carlos user. 

Lets find the path to delete carlos user

<img width="1000" height="543" alt="image" src="https://github.com/user-attachments/assets/f66bf9de-5c11-440a-a52b-3d2dc4773c73" />

Lets add this path to the endpoint.

<img width="1000" height="487" alt="image" src="https://github.com/user-attachments/assets/f2537500-905f-454e-9dc5-f7886e784389" />

We got a 302 response. Follow redirection

<img width="1000" height="509" alt="image" src="https://github.com/user-attachments/assets/c13573fb-17a8-4ccf-804a-f0b078d2168c" />

Carlos user is deleted

<img width="980" height="312" alt="image" src="https://github.com/user-attachments/assets/af78accb-fb1a-4e53-ae7a-df448a5b8b6a" />

And lab is solved !!!
