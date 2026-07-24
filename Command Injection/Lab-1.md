**Command Injection || Lab#1 ||OS command injection, simple case**

<img width="787" height="357" alt="image" src="https://github.com/user-attachments/assets/e878785c-499f-4eba-a8ef-98cc162acf6c" />

The Goal of this lab is to execute the whoami command to determine the name of the current user.

Lets start the lab

<img width="1100" height="594" alt="image" src="https://github.com/user-attachments/assets/0b8a91c0-0bdf-45b4-8214-39815d055a1c" />

As per lab description, command injection vulnerability in the product stock checker.

Lets open any product and check its stock

<img width="1100" height="739" alt="image" src="https://github.com/user-attachments/assets/6ce38762-24ab-4f7c-9a6d-1e48baeb0ad7" />

Lets intercept the traffic in Burpsuite

<img width="1100" height="352" alt="image" src="https://github.com/user-attachments/assets/be73cffa-acb6-4f09-bb2e-a758fe7decde" />

We have POST request to check the stock. Lets move one of the traffic to repeater

<img width="1100" height="515" alt="image" src="https://github.com/user-attachments/assets/59faae81-b5a3-4365-8ef7-256df23a43e9" />

There are two parameters, productId and storeId. Lets put our command in between & and check

<img width="1035" height="537" alt="image" src="https://github.com/user-attachments/assets/b8a90dc8-1ac3-42a9-8f28-39ff7655322e" />

We dont get any output. Lets URL encode the command

Select &whoami and press ctrl+U

<img width="1100" height="493" alt="image" src="https://github.com/user-attachments/assets/36cf3f08-db14-42db-b4e3-6d48bc5623c6" />

And we got the user details. User is peter

We can add # to ignore the storeId parameter

<img width="417" height="56" alt="image" src="https://github.com/user-attachments/assets/215180b2-682a-44bf-90e7-2091892fdd64" />

Add a space and #. URL encode it and try again

<img width="1100" height="530" alt="image" src="https://github.com/user-attachments/assets/872df7e3-d8f2-4d07-9bed-1783f4ce5a99" />

Now, lets check it storeId parameter is vulnerable as well

productId=2&storeId=1&whoami&

URL encode the payload and try

<img width="1100" height="504" alt="image" src="https://github.com/user-attachments/assets/dbf572dd-c307-4d98-8529-f8f1f941da1e" />

And we got the username. It means both parameters are vulnerable to command injection.

Lab is solved.

<img width="1100" height="295" alt="image" src="https://github.com/user-attachments/assets/b8554568-2e6c-48f2-8ea3-07ad42edf7fd" />

