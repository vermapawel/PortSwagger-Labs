**Authentication Vulnerabilities - Lab #12 Password brute-force via password change**

<img width="862" height="422" alt="image" src="https://github.com/user-attachments/assets/9178e61f-91e2-4679-9011-53135b4f053d" />

We have a valid credentials wiener:peter and victim's username carlos.

We also have a list of passwords that we can use to brutr force the account. 

Lets start the lab

<img width="725" height="592" alt="image" src="https://github.com/user-attachments/assets/9d06dbfc-9315-46cb-8c33-62950d46ba93" />

Lets login via the credentials that we have.

Lets change the password

<img width="746" height="182" alt="image" src="https://github.com/user-attachments/assets/fd0c01df-a06d-49f9-b1c4-6fdc0c1141a2" />

Lets intercept this traffic in Burp suite

<img width="900" height="343" alt="image" src="https://github.com/user-attachments/assets/6d5c6748-a186-4f6b-8844-1a13eb9321a1" />

Move this traffic to Repeater

Lets login at weiner account with new password

<img width="820" height="352" alt="image" src="https://github.com/user-attachments/assets/8217d494-b08e-4e4b-8beb-145d78c36384" />

However we are not able to login, we are locked for 1 min.

If we put a wrong password in change password functionality, application will lock us for a minute.

Now we need to find some vulnerability in the application that allows me to brute force the application.

Lets login again

<img width="845" height="590" alt="image" src="https://github.com/user-attachments/assets/65bfb98d-14e6-415b-99db-96a61c558ecb" />

Now, this time lets put a wrong password in Current password filed and put two different passwords in below fields.

<img width="895" height="270" alt="image" src="https://github.com/user-attachments/assets/5831dba7-353e-4a57-a946-73fe3f7de521" />

lets check this traffic in Burp

<img width="900" height="258" alt="image" src="https://github.com/user-attachments/assets/0af8d402-d676-4c99-9dc4-dd30135ca838" />

We have put a wrong password i.e peter and put different passwords. 

This time we are not locked for 1 min. So, it means if new passwords does not match, there is no brute force mechanism. 

Lets move this traffic to Repeater

<img width="900" height="364" alt="image" src="https://github.com/user-attachments/assets/eeff2f8c-d9d4-4da0-b201-64bf59636a1e" />

Now, lets put the correct password and check

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/fd0b841e-0364-4da5-b81b-a74f6813db47" />

This time we got different error message. 

Lets summarize what's happening

When current password is incorrect and both passwords are different, error is Current password is incorrect.

When current password is correct and both passwords are different, error is New password do not match. 

Lets move this traffic in Intruder

<img width="900" height="377" alt="image" src="https://github.com/user-attachments/assets/384b130c-a82b-4fa4-8ed8-5e8c6ab08a11" />

We will change the username to carlos and keep both passwords different so that we are not logged out of the account. 

We will brute force the current password. We will use the list of passwords that is provided.

<img width="900" height="308" alt="image" src="https://github.com/user-attachments/assets/44d52ace-ad8d-4b8b-bb49-94bad71d1534" />

Only one request have different Length. Lets try this password i.e abc123

And we are logged in. Lab is solved.

<img width="786" height="276" alt="image" src="https://github.com/user-attachments/assets/2389de8a-fb2d-4af0-bb42-2b8ac90f5917" />

