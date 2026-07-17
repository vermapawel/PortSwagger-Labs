**SQL Injection — Lab #3 SQLi UNION attack determining the number of columns returned by the query**

<img width="1086" height="571" alt="image" src="https://github.com/user-attachments/assets/02e23e22-a163-4a64-851a-ab96b7516e59" />

In this Lab Product Category is vulnerable to SQL injection attack.

We have to preform SQL injection UNION attack to determine the numbers of columns in the database contents of other tables.

First we need to understand how UNION operator works.

Lets say we have two tables.

<img width="397" height="148" alt="image" src="https://github.com/user-attachments/assets/ea2021ca-03f1-4318-89d6-92bb03a9abb7" />

Table 1 has two columns A and B. Table 2 has two columns C and D.

Now Imagin we have few queries

**Query1 → SELECT a,b FROM Table 1**

The output of this query will b

<img width="148" height="79" alt="image" src="https://github.com/user-attachments/assets/b901352e-0d71-4bca-b25c-5ea0c9ade346" />

***Query2 → SELECT a,b FROM Table 1 UNION select c,d from Table 2***

UNION operator combines the results of two queries.

So first SELECT a,b FROM Table 1 will run, then select c,d from Table 2 will run. The output will be following.

UNION operator combines the results of two queries.

So first ***SELECT a,b FROM Table 1*** will run, then ***SELECT c,d from Table 2*** will run. The output will be following.

<img width="105" height="112" alt="image" src="https://github.com/user-attachments/assets/592a95da-7f05-4098-967b-0a67f9c508c4" />

The result will be display in one single set table.

Now lets say there is a query which display **Product** table.

***SELECT a,b FROM Product***

We are not interested in the contents of the Product tables. I wanted to know what other tables are there in the SQL like Users table which contains credentials of the users.

So we can use **UNION** operator to display contents of **Users** table. It can trick the database into returning **additional rows** from **another table**

***SELECT a,b FROM Product UNION select username , password FROM Users***

Rules for Using **UNION** Operator

1. The number and the order of the columns must be same in all queries. In our example we have 2 columns in both Tables. (A and B in Table 1 and C and D in Table 2)
   
2. The Data types must be compatible. In our example all data types are integers.

**How we can use UNION operator in SQLi**

Lets say we are doing Blackbox Pentesting and we don't know how many columns a table has.

***SELECT ? FROM Table1***

Here we are using ? because we dont know the number of column Table1 has.

Now, if this query is vulnerable to SQLi we can use UNION operator and try to know how many column Table 1 has.

***SELECT ? FROM Table1 UNION SELECT Null***

As per UNION Operator rule, **the number and the order of the columns must be same in all queries.**

So if the number of column in Table 1 is 3, this query will throw an error as we have put only single value (NULL) in later query.

***SELECT ? FROM Table1 UNION SELECT Null Null***

Again it will throw an error as Table 1 has 3 columns and we have used 2 values in later query (NULL NULL)

***SELECT ? FROM Table1 UNION SELECT Null Null Null***

Now this time we are using three values (Null Null Null) in later query which is equal to number of columns in Table 1, it will throw 200 response.

Lets start the Lab

<img width="1100" height="491" alt="image" src="https://github.com/user-attachments/assets/5bb3e5d7-75c9-4e9b-9709-f4064f9e3310" />

Its looks like a shopping application.

If we select Product category Gifts, it will display only those items available in **Gifts** column.

<img width="1100" height="513" alt="image" src="https://github.com/user-attachments/assets/8126f490-8088-4f92-a756-6496f0215cff" />

Now, from the Lab description we know that Product Category is vulnerable to SQLi. Lets check

<img width="1100" height="282" alt="image" src="https://github.com/user-attachments/assets/c1afdbe1-cab9-42c7-8e13-d0ee188af067" />

SQL code breaks and we got an error message. It means its could be vulnerable to SQLi.

Lets test again

<img width="1100" height="541" alt="image" src="https://github.com/user-attachments/assets/137b482d-467e-47c5-adc0-3cef42a818b3" />

Here we dont get error message as we have comment out the rest of the query.

Lets use UNION operator now to solve the lab

***web-security-academy.net/filter?category=Gifts’ UNION select NULL --***

<img width="1100" height="592" alt="image" src="https://github.com/user-attachments/assets/b20ccbbb-05fd-4248-94b0-123a7aa8a0d9" />

<img width="1100" height="297" alt="image" src="https://github.com/user-attachments/assets/50c53c2b-6de2-4d0d-8d22-e2048cb16760" />

We get an error message. It means there is not just one column in the query which is obvious as we can see name of the product and pricing in the gift category.

<img width="1039" height="399" alt="image" src="https://github.com/user-attachments/assets/606d3065-4617-4607-9ffd-0952b1831e41" />

Lets test again

web-security-academy.net/filter?category=Gifts’ UNION SELECT NULL,NULL --

We again get an error message. It means it has more than 2 columns.

Lets test again

web-security-academy.net/filter?category=Gifts’ UNION SELECT NULL,NULL,NULL --

<img width="1100" height="667" alt="image" src="https://github.com/user-attachments/assets/7c6a3973-3715-4af0-9926-d447aef8450f" />

And the Lab is solved. It means it has three columns.


























