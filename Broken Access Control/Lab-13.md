**Broken Access Control ||Lab # 13 Referer-based access control**

<img width="842" height="366" alt="image" src="https://github.com/user-attachments/assets/183abba4-5e0c-4ee8-8451-36fd2da47d5c" />

Goal of this lab is to become administrator user.

Lets start the lab and login with admin account

<img width="900" height="209" alt="image" src="https://github.com/user-attachments/assets/92cd9182-d61e-45cf-8661-87ff9579b285" />

We can see that we are a normal user. 

Let upgrade the other user as admin to check the functionality of the application.

<img width="562" height="232" alt="image" src="https://github.com/user-attachments/assets/f244a0b6-8285-4076-a51c-189c31cd7f4c" />

And user became admin. There is a one step proess. 

Lets check the traffic on Burp suite

<img width="900" height="401" alt="image" src="https://github.com/user-attachments/assets/13e6272d-bc40-4ed7-b255-205d277c03ef" />

Lets move this traffic to Repeater

<img width="900" height="454" alt="image" src="https://github.com/user-attachments/assets/286be4ea-fd30-46c2-b71b-b17d7c5f0449" />

It takes username and action to upgrade. 

Now, lets login with normal user

<img width="900" height="493" alt="image" src="https://github.com/user-attachments/assets/85959a01-d8a2-4a6f-8773-6e2a4dc54e62" />

This is the cookie of the normal user 0RnMmU3xipw5v4sM1O5ey9qWf2WeHADs

Lets use this session cookie in the previous traffic


