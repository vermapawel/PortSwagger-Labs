**JWT || Lab#3 || JWT authentication bypass via weak signing key**

<img width="780" height="585" alt="image" src="https://github.com/user-attachments/assets/cab23c56-373e-41d5-8374-21efcf945504" />

Goal of the lab is to brute force website secret key. Using this key we have to delete user carlos

Credentials → wiener : peter

Lets start the lab and login

<img width="732" height="342" alt="image" src="https://github.com/user-attachments/assets/ea82c7e7-1344-4d1c-b766-d3c071d9547b" />

Lets check this traffic in Burp suite

<img width="1000" height="390" alt="image" src="https://github.com/user-attachments/assets/32943d42-0d70-46e6-b542-b07a2cb55117" />

We can see a JWT is assigned. Lets move his traffic to Repeater

<img width="1000" height="590" alt="image" src="https://github.com/user-attachments/assets/87a08e1d-162d-443e-ad46-787521f111d8" />

We can see that under Payload component of JWT, subject is wiener which is a normal user.

Now, lets check for week signing key / brute forcable secret key. 

This attack vector only works for symmetric algorithms. In JWT alg is HS256 which is a symmetric algorithms. So it generates only one key to generate and validate the Signature.

Lets copy the JSON Web token. We will try to crack it using hashcat. 

In the lab description, we have a word list provided. Download the wordlist in the local machine. We will use that word list.

<img width="1000" height="361" alt="image" src="https://github.com/user-attachments/assets/11fa4d9d-6fcd-44fb-b8ab-2b6cfd797e2f" />

<img width="895" height="322" alt="image" src="https://github.com/user-attachments/assets/7659275a-af73-4e62-a640-7162ad87b0d4" />

hashcat has cracked the secret key.

<img width="1000" height="265" alt="image" src="https://github.com/user-attachments/assets/eea1218c-70b7-4889-adf5-b6d3aeee5c60" />

So the secret key is secret1. This is our secret key which is used to signing the token.

Now, first we need to encode secret1 as base64

<img width="912" height="402" alt="image" src="https://github.com/user-attachments/assets/9e627778-bcd0-4cec-b2b6-492785768890" />

Lets generate a Symmetric Key

<img width="892" height="687" alt="image" src="https://github.com/user-attachments/assets/d3613756-07bb-4747-83c0-5a2e45d46f66" />

We will put base64 of secret1 in K

<img width="1000" height="202" alt="image" src="https://github.com/user-attachments/assets/a19dd5e6-e9c5-460d-b659-ba536f257b88" />

We have a key generated.

Now, go back to JSON Web Token in Repeater.

Lets change the subject to administrator.

We need to sign the JWT

<img width="912" height="645" alt="image" src="https://github.com/user-attachments/assets/e1f2c53c-95c7-4b33-b091-c69153d21e7b" />

Now, we will change the endpoint to admin and forward the traffic.

We got a 200 OK response. It seems we are logged in as administrator.

To solve the lab, we have to delete carlos user. Lets find the path to delete the user.

<img width="1000" height="510" alt="image" src="https://github.com/user-attachments/assets/b669a771-6e15-4981-8b01-39fe28fe8f74" />

Lets put this path to the endpoint and forward the traffic.

<img width="1000" height="450" alt="image" src="https://github.com/user-attachments/assets/a150426a-0f40-40da-910f-480ce54b17fe" />

We got a 320 response. Lets follow redirection

<img width="1000" height="486" alt="image" src="https://github.com/user-attachments/assets/91eee7ee-9688-438f-95f4-85e94df40a5e" />

User carlos is deleted

<img width="1000" height="282" alt="image" src="https://github.com/user-attachments/assets/a3d82ff3-c129-4ad1-8969-07024d5bc30c" />

And lab is solved !!!!
