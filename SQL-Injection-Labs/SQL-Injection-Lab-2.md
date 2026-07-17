**SQL Injection — Lab #2 SQL injection vulnerability allowing login bypass**

<img width="1100" height="409" alt="image" src="https://github.com/user-attachments/assets/dcf85b6c-9d05-4faa-ba67-2a8954587866" />

In this Lab Login Functionality is vulnerable to SQL injection.

Goal of this lab is to login as **administrator**

<img width="1100" height="465" alt="image" src="https://github.com/user-attachments/assets/672a716e-5689-471e-b098-46713cdb526b" />

Now first try to login with some common credentials

admin || admin

<img width="886" height="391" alt="image" src="https://github.com/user-attachments/assets/05381ad7-b2b7-4f75-b33a-62bf513db285" />

It gives error ‘Invalid username or password’. In general, it's called non verbose generic message. Its not giving much information regarding credentials.

Lets assume if we put credentials admin || password and error message says password is incorrect, its giving us hint that username i.e admin is correct. So we got the username and we can perform brute force attack for the password.

First we need to check if this application is vulnerable to SQL injection or not.

Lets put ‘ in the username and any random password and see how the application behaves.

<img width="897" height="382" alt="image" src="https://github.com/user-attachments/assets/3d48e4a3-804c-43b7-a0d1-307875aa150d" />

<img width="1006" height="211" alt="image" src="https://github.com/user-attachments/assets/83538a84-3957-4702-9ce4-a07841c355fe" />

We got ‘Internal Server Error’. So we have break the SQL query. This application could be vulnerable to SQL injection.

Now in this Lab we don't have the backend SQL query that is running at the backend how login functionality works. We have to guess it.

**SELECT firstname FROM users where username=’admin’ and password=’admin’**

<img width="466" height="213" alt="image" src="https://github.com/user-attachments/assets/d1e92078-52ec-4670-b9c0-cb51e0d42264" />

It queries the users table.

It returns the firstname of any user whose:

username is 'admin'

password is 'admin'

So this type of query should be running at the backend. Lets try to find a way how we can exploit it.

When we put a ‘ in the username, the query becomes as following

**SELECT firstname FROM users where username=’’’ and password=’admin’**

We got an error page.

<img width="1036" height="270" alt="image" src="https://github.com/user-attachments/assets/b0a471d3-819e-4d98-a59f-ff6cfe67ee02" />

This is because the extra single quote ‘ breaks the query. First two quotes is used for a legitimate query and the 3rd quote becomes an extra which breaks it and application throws ‘Internal Server Error’ message.

Now, we can try to login as a user and ignore the password field in the SQL query.

**SELECT firstname FROM users where username=’admin’ — and password=’admin’**

<img width="457" height="226" alt="image" src="https://github.com/user-attachments/assets/8cc18dac-9c1a-4c20-adfc-d5731123b33d" />

The AND password='admin' part is ignored.

We are commenting out with the help of — anything after **SELECT firstname FROM users where username=’admin’**

So if there is any user admin, it will login without asking for its password.

Lets test. We can put any password, it will not matter as it will get ignored.

Our payload is ‘ --

<img width="1021" height="265" alt="image" src="https://github.com/user-attachments/assets/220b79e0-e575-464e-803d-47a38a619be7" />

It does not worked and we got same error. It means there is not user named admin in the system.

Now, lets try with **administrator**

**SELECT firstname FROM users where username=’administrator’ -- and password=’admin’**

Our payload is ‘ --

<img width="799" height="348" alt="image" src="https://github.com/user-attachments/assets/c05e4844-2ec7-4dfb-a4e8-3ce1f23d5a13" />

And we are logged in successfully.

<img width="1100" height="377" alt="image" src="https://github.com/user-attachments/assets/942ac620-8dc5-44c9-9223-8aa5039c9c47" />

And Lab is solved !!!































