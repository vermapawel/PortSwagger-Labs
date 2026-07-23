**SQL Injection -- Lab #15 Blind SQL injection with out-of-band interaction**

<img width="720" height="538" alt="image" src="https://github.com/user-attachments/assets/be817c98-ac7b-4479-a26c-70d5b8115c49" />

In this Lab the vulnerable parameter is Tracking cookie.

As per Lab description, we can trigger out-of-band interactions with external domains. It means we send an attack payload that causes an interaction with an external system on which we have full control.

Lets understand better with the help of Copilot.

<img width="640" height="247" alt="image" src="https://github.com/user-attachments/assets/6f339f33-9794-4931-9bf8-81eab3739fb9" />

<img width="640" height="326" alt="image" src="https://github.com/user-attachments/assets/c3c92bfc-7fc5-4619-b82a-dcc2849fa386" />

So, we understand that when the Database don't throw any error, and also there is not delay in the response, we can perform Out of Band SQLi. One important condition is the Database server can make outbound network connections.

Lets inspect the traffic is Burp suite

<img width="640" height="312" alt="image" src="https://github.com/user-attachments/assets/ad2bec21-96fe-4598-9245-3321b1841bb7" />

Now, to solve this Lab we need to have Burp Suite Professional. Since I don’t have Burp Suite Professional, I am putting the screen shots.

<img width="598" height="570" alt="image" src="https://github.com/user-attachments/assets/ea1c9c6a-7412-4d60-a9b7-4c7563a4dafe" />

<img width="630" height="562" alt="image" src="https://github.com/user-attachments/assets/b5a3ebaa-45d9-46d8-ae4c-8d6ca7af006e" />

<img width="400" height="28" alt="image" src="https://github.com/user-attachments/assets/e3090745-95e9-4dd4-810d-c0199654cf02" />

So this is our collaborator client where we will perform DNS lookup.

Now we need to perform Blind based SQLi.

Lets check the SQLi cheat sheet.

<img width="613" height="321" alt="image" src="https://github.com/user-attachments/assets/7c68e742-1210-4767-837c-07d756ffc698" />

1st we need to know what database is running on the backend. We have different payload for each Database.

Lets check Oracle first

For Oracle there are two types of payload. For unpatched version and fully patched version.

First we will try unpatched version of Oracle payload

Lets create the payload

<img width="600" height="93" alt="image" src="https://github.com/user-attachments/assets/8fd2b163-4265-4af8-ae74-60f207df6f85" />

Lets put this payload in the Burp and send the request.

<img width="640" height="293" alt="image" src="https://github.com/user-attachments/assets/c06258a7-27ea-4bc8-bde8-72ab4c7a22f4" />

Now on Burp collaborator client, click on Poll now

<img width="640" height="363" alt="image" src="https://github.com/user-attachments/assets/5cc47679-6437-40b2-83a9-cd7d48f75fb1" />

We got a DNS lookup. The IP address of the Application is also shown below.

And we have solved the Lab

<img width="640" height="369" alt="image" src="https://github.com/user-attachments/assets/c13765d2-4d2c-483e-899f-77e34503f8ab" />



