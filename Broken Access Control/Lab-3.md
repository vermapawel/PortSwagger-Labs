**Broken Access Control ||Lab #3 User role controlled by request parameter**

<img width="857" height="360" alt="image" src="https://github.com/user-attachments/assets/c7b07d99-fe8c-4323-967d-ceca81fa6f0d" />

We have our credential wiener:peter

Goal of this lab is to delete user carlos.

Lets start the lab and login with our credentials.

<img width="900" height="373" alt="image" src="https://github.com/user-attachments/assets/2a921f3a-9ffe-40ba-9d92-9642aa55cf91" />

Lets capture this traffic in Burp suite

<img width="900" height="428" alt="image" src="https://github.com/user-attachments/assets/e9b81751-860c-473e-8b19-fd597813a42d" />

We can see its a POST request and 302 response. 

Also, there are two cookies, one is Admin with is set as false and other is session cookie.

This is the traffic where we have put credentials and my-account page has opened.










