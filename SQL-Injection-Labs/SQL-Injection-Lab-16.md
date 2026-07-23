**SQL Injection -- Lab #16 Blind SQL injection with out of band data exfiltration**

<img width="720" height="560" alt="image" src="https://github.com/user-attachments/assets/d9a623b8-b5fd-439b-a51f-ce1439d7ad1b" />

In this Lab the vulnerable parameter is Tracking cookie.

As per Lab description, we can trigger out-of-band interactions with external domains. It means we send an attack payload that causes an interaction with an external system on which we have full control.

Goal of this Lab is to find the password of the user administrator and login at the application.

Lets start the Lab

<img width="640" height="384" alt="image" src="https://github.com/user-attachments/assets/84dab232-f4cb-481a-b639-e41dbc002349" />

Lets intercept the traffic using Burp.

Now, to solve this Lab we need to have Burp Suite Professional. Since I don’t have Burp Suite Professional, I am putting the screen shots.

<img width="640" height="584" alt="image" src="https://github.com/user-attachments/assets/4eab0c39-6c62-4c80-ab33-23e07f896613" />

Lets go to Burp Collaborator Client

<img width="640" height="408" alt="image" src="https://github.com/user-attachments/assets/d222ede9-435f-4ca9-be4e-6f02ec49536c" />

Click on Copy the cilpboard

This is our collaborator client

<img width="620" height="34" alt="image" src="https://github.com/user-attachments/assets/a0915b0e-3f2d-4b52-beb0-036d610cdc4a" />

Now we need to perform Blind based SQLi. We will display the password of the administrator user here.

Lets check the Cheat sheet

<img width="640" height="549" alt="image" src="https://github.com/user-attachments/assets/7c5fd115-cbee-47b5-b244-02bef363935e" />

From the last lab (Lab 15) we got to know that Oracle Database is running in the backend.

Lets create the payload

<img width="640" height="86" alt="image" src="https://github.com/user-attachments/assets/1b41ad01-375a-453a-bc4c-9451985462e4" />

Now put this payload in the tracking ID and forward the traffic.

<img width="640" height="281" alt="image" src="https://github.com/user-attachments/assets/ed2a3e16-5e04-4561-bb9b-cbe43b225f8f" />

We can see that DNS lookup was performed. Also there is the password for the Administrator user (highlighted in green)

Lets try to login now

<img width="640" height="356" alt="image" src="https://github.com/user-attachments/assets/146d0366-02b7-4ab8-8a35-cedd7e7966bf" />

We are able to login and lab is solved !!!

