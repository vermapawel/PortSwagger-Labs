**Information disclosure || Lab#2 || Information disclosure on debug page**

<img width="770" height="412" alt="image" src="https://github.com/user-attachments/assets/073af14c-bcb7-4d9d-a0a0-5bd1a88024ae" />

Goal of this lab is to get the SECRET_KEY environment variable.

Lets start the lab and check some products

<img width="1000" height="772" alt="image" src="https://github.com/user-attachments/assets/64eb58df-ef15-4210-86dc-303abfd56f12" />

In Burp suite, we will go the site map and find the target URL

<img width="995" height="892" alt="image" src="https://github.com/user-attachments/assets/15708028-ae85-4125-8aca-ca11c495824e" />

Here we can see cgi-bin. Lets check this

<img width="941" height="347" alt="image" src="https://github.com/user-attachments/assets/866b4a1f-3abb-4468-ba6a-e2aded2d7a09" />

We got a php page. Right click and copy the URL.

It display all the php setting of the page.

<img width="1000" height="239" alt="image" src="https://github.com/user-attachments/assets/ee8ee00b-a7eb-4c4d-9a78-b475932b2290" />

We got the secret key. Lets submit it

<img width="936" height="360" alt="image" src="https://github.com/user-attachments/assets/831b46de-5a52-42bf-9026-fb887c72d57e" />

And Lab is solved.

<img width="1000" height="346" alt="image" src="https://github.com/user-attachments/assets/80a23de0-1149-4623-a74b-e987207face0" />
