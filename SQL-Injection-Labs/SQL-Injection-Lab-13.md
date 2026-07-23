**SQL Injection -- Lab #13 Blind SQL injection with time delays**

<img width="720" height="387" alt="image" src="https://github.com/user-attachments/assets/adfd9b21-2802-4bdb-9d8b-3e5e0d4a8170" />

In this Lab, the Database will not throw any error on the screen. So we cannot use UNION SQLi. Also the Database will not behave any differently with any error. So we cannot perform Blind SQLi as well.

Since the query is executed synchronously, we can perform some delays in the output.

The Goal of this Lab is to cause a 10 second delay.

Lets start the Lab

<img width="640" height="348" alt="image" src="https://github.com/user-attachments/assets/468e7685-ee7e-4555-bc09-dec49ba78a3c" />

Lets intercept the traffic in Burp suite.

<img width="640" height="595" alt="image" src="https://github.com/user-attachments/assets/2a607dbf-1a5b-4d45-9e32-86edf78f83ff" />

Our vulnerable parameter is Tracking ID.

We need to inject a SQLi code that cause 10 seconds delay. And if we are able to cause a 10 second delay, that means it is vulnerable to Time based SQLi.

Now, we need a query that cause a delay. Lets check the Cheat sheet.

<img width="640" height="185" alt="image" src="https://github.com/user-attachments/assets/22a72e2c-8aa5-4ada-9230-7e8324413ebe" />

As of now we dont know that Database is running in the backend.

Lets test MySQL

***‘ || (SELECT sleep(10) --***

<img width="640" height="229" alt="image" src="https://github.com/user-attachments/assets/f66b3068-f94e-46a6-b483-31d767124182" />

We got the response instantaneously (151 milliseconds). It means the Database is not MySQL

Lets check for PostgreSQL

***‘ || (SELECT pg_sleep(10)) --***

<img width="640" height="478" alt="image" src="https://github.com/user-attachments/assets/4e45da04-27b6-4720-8bc0-8fa4e83e6aaf" />

And there is a response of 10,145 milliseconds which is 10 seconds. So it confirms that Database is Postgre SQL

<img width="640" height="264" alt="image" src="https://github.com/user-attachments/assets/00bab131-1d1b-4281-b642-496ea6d578c3" />

And the Lab is solved !!!





















