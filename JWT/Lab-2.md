**JWT || Lab#2 || JWT authentication bypass via flawed signature verification**

<img width="777" height="562" alt="image" src="https://github.com/user-attachments/assets/1f784290-dd40-42d2-a0d8-ee04d1e782ba" />

Goal of this lab is to modify your session token to gain access to the admin panel at /admin, then delete the user carlos.

Credentials → Wiener : peter

Lets start the lab and login with the credentials provided.

<img width="907" height="352" alt="image" src="https://github.com/user-attachments/assets/1fab7257-3eb6-47ba-860a-9ceba58fd0ee" />

Lets check traffic in Burpsuite

<img width="1000" height="416" alt="image" src="https://github.com/user-attachments/assets/78fbe5aa-6ef8-4116-adc9-c8adda047c45" />

Lets move this traffic to Repeater

<img width="1000" height="451" alt="image" src="https://github.com/user-attachments/assets/a88308ef-fc60-4ac9-8123-d0697800c736" />

<img width="1000" height="652" alt="image" src="https://github.com/user-attachments/assets/f5def165-46b2-4992-8199-7006ef0110f0" />

Lets go to the JSON Tab in the Request. In the Header we can see that RS256 algorithm is set. 

For debugging purposes, the library has an option to set algorithm as none. So the application does not have to verify the signature every time it receives a request. It was only for debugging purposes and never intended to use in production. However sometime this configuration is in production. 

Lets change the algorithm as none

<img width="737" height="497" alt="image" src="https://github.com/user-attachments/assets/3b524f9c-6680-43c0-a42d-05bcc38e59fa" />

We will also change the username as Administrator in the JWT

<img width="737" height="595" alt="image" src="https://github.com/user-attachments/assets/b52d3b7a-e759-4aed-8b84-19d6b7a9d98c" />

Now, we have to remove the Signature component from the JWT.

We have change the endpoint to admin and removed the signature from JWT. Lets forward this traffic.

<img width="1000" height="460" alt="image" src="https://github.com/user-attachments/assets/fb61738d-0bdd-43f3-9cde-4fd2c58062e8" />

And we are at Admin panel. We have options to delete users.

To complete the lab we have to delete carlos user.

Lets fine where is the path for deleting carlos user on the response

<img width="1000" height="505" alt="image" src="https://github.com/user-attachments/assets/d05cb439-0c09-4df2-97a9-206d593385b8" />

Lets put this path in the request

<img width="1000" height="513" alt="image" src="https://github.com/user-attachments/assets/74dab018-9f0e-42e7-92a1-04de24b9540f" />

We got a 302 respond. Lets follow redirection.

<img width="1000" height="497" alt="image" src="https://github.com/user-attachments/assets/e3f3423c-09a4-47a7-a836-4411db559a2a" />

And we can see there is not carlos user.

<img width="1000" height="311" alt="image" src="https://github.com/user-attachments/assets/d866f606-6d1b-4275-91cc-846a0b3240cf" />

Lab is solved !!!
