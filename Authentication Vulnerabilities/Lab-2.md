**Authentication Vulnerabilities || Lab #2 || 2FA simple bypass**

<img width="852" height="559" alt="image" src="https://github.com/user-attachments/assets/cb86e023-9ba0-4bd1-8c4d-7befbeaa3ab1" />

In this Lab we have our credentials and victim’s credentials.

Goal of this Lab is to login as Carlos bypassing 2FA.

Lets start the Lab

<img width="1100" height="624" alt="image" src="https://github.com/user-attachments/assets/8ba563c4-3ae5-4b50-b7be-f476cd6e2cc2" />

Lets login with our credentials and see how 2FA is implemented.

<img width="942" height="582" alt="image" src="https://github.com/user-attachments/assets/5aa5148c-1086-444d-b106-61227f210510" />

We need to put 4 digit OTP. Lets check the Email client

<img width="1021" height="408" alt="image" src="https://github.com/user-attachments/assets/a5efdde8-afda-48f2-b676-5c6f4fce9a4b" />

<img width="1100" height="342" alt="image" src="https://github.com/user-attachments/assets/25526a19-5f51-4fd1-9a26-a1d4702915a5" />

The OTP is 0561

<img width="969" height="409" alt="image" src="https://github.com/user-attachments/assets/9a6c8bc7-ceb8-4de4-9b43-62c2e7903ee8" />

And we are logged in

<img width="1100" height="451" alt="image" src="https://github.com/user-attachments/assets/ffa5d6d7-6616-4cc9-bb98-1dfc5b3450fd" />

Lets check this traffic in Burp suite

<img width="1100" height="457" alt="image" src="https://github.com/user-attachments/assets/300af7c7-392e-4383-8518-837633ff2ea5" />

Here we can see that mfa-code is 0561.

Lets try to login with victims credentials

<img width="985" height="372" alt="image" src="https://github.com/user-attachments/assets/f0208447-7f81-4286-9588-de5786942bf2" />

Lets check this traffic in Burp suit

<img width="1100" height="449" alt="image" src="https://github.com/user-attachments/assets/722dd133-a6bb-4812-955c-aeaee3394b36" />

This is a **POST /login** request. Let forward this traffic.

<img width="1100" height="625" alt="image" src="https://github.com/user-attachments/assets/c80c5a3c-e034-493b-8392-25120807679c" />

Now, this is **GET /login2** request which is looking for OTP. Lets drop this request.

<img width="1100" height="251" alt="image" src="https://github.com/user-attachments/assets/f1437210-651e-4822-83ae-b9a9937e25d3" />

Now lets check if it still allows us to login in the account.

<img width="1100" height="715" alt="image" src="https://github.com/user-attachments/assets/eb6a608a-dac5-40e0-b41f-1010a1741574" />

And we are able to login.

It means 2FA authentication is not properly implemented.













