**Broken Access Control ||Lab #9 User ID controlled by request parameter with data leakage in redirect**

<img width="872" height="417" alt="image" src="https://github.com/user-attachments/assets/1b7b18e5-19c3-44c2-944b-79f27e7240e6" />

To solve the lab we have to get carlos user API key. 

Lets start the lab and login with the credentials provided.

<img width="900" height="490" alt="image" src="https://github.com/user-attachments/assets/a0c0443a-9a09-437a-8181-d18cd0223755" />

In the URL, there is a parameter id which takes the userame. Lets put carlos in the id parameter and check

<img width="900" height="472" alt="image" src="https://github.com/user-attachments/assets/4cb7783e-7f8c-403c-8b07-46581a477af5" />

It will redirect to the login page. Lets check this traffic in the burp suite

<img width="900" height="355" alt="image" src="https://github.com/user-attachments/assets/8f93a706-d1d3-4ac8-a3de-84c618fb7d34" />

In the burp suite, we can see 302 response code. Its redirecting to the login page. However its showing all the page content of the URL.

<img width="711" height="201" alt="image" src="https://github.com/user-attachments/assets/7d05af6e-3836-4840-8dcc-836c420736d3" />

And we got the API key for carlos.

<img width="900" height="310" alt="image" src="https://github.com/user-attachments/assets/5f0420fd-6767-4c91-9460-cfdcb1093627" />

And lab is solved

<img width="900" height="270" alt="image" src="https://github.com/user-attachments/assets/a54cb6cc-3898-458e-a95c-06f4a9e4e8a9" />
