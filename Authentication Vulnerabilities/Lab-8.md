**Authentication Vulnerabilities — Lab #8 2FA broken logic**

<img width="870" height="397" alt="image" src="https://github.com/user-attachments/assets/eb30fc38-6a3e-4321-a003-9a4970afad87" />

We have our credential wiener:peter and victim’s username carlos.

Lets start the lab and login with valid credentials to understand how application behaves

<img width="797" height="346" alt="image" src="https://github.com/user-attachments/assets/2f0682ed-8ac3-4829-9ab8-4b232fdf6671" />

<img width="930" height="420" alt="image" src="https://github.com/user-attachments/assets/67ff8136-794b-4149-a92a-25b674473421" />

Application is asking for a 4 digit code to login. Lets go to the email client and put the code.

<img width="1100" height="341" alt="image" src="https://github.com/user-attachments/assets/b5933fe2-5a1f-471c-89df-bbfa6c2b68cb" />

And we are logged in

<img width="815" height="322" alt="image" src="https://github.com/user-attachments/assets/637b65ad-e15b-471b-ac85-04741b471717" />

Lets capture all the traffic.

<img width="1100" height="71" alt="image" src="https://github.com/user-attachments/assets/e36b04a2-230d-4c94-a64c-bc2359d17d69" />

We can see there are two requests for login. One is POST and one is GET.

After that there is on POST request for putting the code.

<img width="1100" height="437" alt="image" src="https://github.com/user-attachments/assets/f7440e62-8685-4a32-b582-677ba43b9671" />

Lets move these three traffic to Repeater

<img width="835" height="586" alt="image" src="https://github.com/user-attachments/assets/89667327-ed84-4053-b92f-acaf8fb39855" />

The 2nd traffic i.e login2 where it sends a code to the email, we can see two cookie values. First is verify that takes the username and other is session that generates the session ID.

Now, if we change the username to carlos and remove the session ID, the application sends a code to carlos email address. Howver we dont have access to carlos email so we cant see the code.

<img width="1100" height="469" alt="image" src="https://github.com/user-attachments/assets/d6536f80-b8b0-4639-8099-3f290709a491" />

Lets check the other traffic which sends the code.

<img width="897" height="592" alt="image" src="https://github.com/user-attachments/assets/66b398eb-c0c5-4a01-80e8-03171c005718" />

This traffic also contains two cookie and mfa-code.

Lets remove the session cookie and forward the traffic

This traffic also contains two cookie and mfa-code.

Lets remove the session cookie and forward the traffic

<img width="1100" height="522" alt="image" src="https://github.com/user-attachments/assets/c0ba6ff8-a91c-41b2-b512-8c46c5af1a12" />

Still we got redirected to a my-account page. It means we dont need a session cookie, all we need is a correct code that is linked with the username to login.

So it means username and password is not required actually. No we need to guess carlos code and we can login.

Lets change the username to carlos and check

<img width="1100" height="499" alt="image" src="https://github.com/user-attachments/assets/254908a4-c220-4037-a22c-bca322bc9c96" />

We got a message, incorrect security code

Now, we need to brute force the mfa-code. Lets move this traffic to intruder

<img width="1100" height="609" alt="image" src="https://github.com/user-attachments/assets/68c1537b-c933-49c6-b1ce-819f044ef2a2" />

There will be 10000 payload that will be tested. We are looking for a response code 302 for redirection.

We can see a session is created for carlos q7GDFRw9LHZNn2iycIKpdEIBdgwqk7Cr

Lets copy this cookie ID

We will go to the authentication page and change the wiener cookie value to this one. Also we will delete the other verify cookie and refresh the page

<img width="1100" height="332" alt="image" src="https://github.com/user-attachments/assets/a467bfbe-8b3b-4ec7-9616-bd3a7f4cc18a" />

We are logged in as Carlos and lab is solved

<img width="887" height="522" alt="image" src="https://github.com/user-attachments/assets/94a845af-5d01-4599-965d-d762612f7dc9" />
