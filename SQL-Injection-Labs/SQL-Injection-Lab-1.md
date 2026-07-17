**SQL Injection — Lab #1 SQL injection vulnerability in WHERE clause allowing retrieval of hidden data**

<img width="844" height="438" alt="image" src="https://github.com/user-attachments/assets/a7e26cf6-439a-4192-aac3-90fcc9512c74" />

The backend query that is running should be like,

**SELECT * FROM products WHERE category = ‘Gifts’ AND released = 1**

Lets open the Lab

<img width="1100" height="759" alt="image" src="https://github.com/user-attachments/assets/505fd48c-2cd9-45b9-9166-567a9d6ad89a" />

Our goal is to get the website display those products which are not released yet.

As per the lab description there is SQL vulnerability in **Category** filter of the website.

<img width="1100" height="738" alt="image" src="https://github.com/user-attachments/assets/19b53f0d-8e99-4bfa-b203-a0948773dcca" />

So when we are selecting any **category**, the URL change accordingly.

<img width="1100" height="773" alt="image" src="https://github.com/user-attachments/assets/4519816d-615d-49d4-a3e2-348aa175a547" />

When we are selecting **Pets** following is the SQL query running.

**SELECT * FROM products WHERE category = ‘Pets’ AND released = 1**

As per this query it is selecting all the rows from products table where category column is equal to Pets and released column is equal to 1.

**category = ‘Pets’ AND released = 1**

Now here we have **AND** operator. So it means it will only display those products where category = Pets and release = 1. Here both conditions must match. If category = Pets and release is anything other than 1, it will not display the products.

Now, first lets check if the application is vulnerable to SQL injection or not.

Most common way to break the SQL query is using ‘ or “

Lets check

**web-security-academy.net/filter?category=’**

<img width="1100" height="372" alt="image" src="https://github.com/user-attachments/assets/d9d1ef47-6a0d-4008-92e0-9c0bc13f8e03" />

We get an error message **Internal Server Error**

On the backend

**SELECT * FROM products WHERE category = ‘’’ AND released = 1**

The ‘ that we have added closed the starting ‘ and we have left with single ‘ that breaks the SQL query and it throws an error. So, this application could be vulnerable to SQL injection.

Lets try to create a SQL injection payload

**SELECT * FROM products WHERE category = ‘’--‘ AND released = 1**

Adding -- will comment everything after it. So after category = ‘’ everything will be commented and get ignored.

Lets test

**web-security-academy.net/filter?category=’ --**

<img width="1100" height="510" alt="image" src="https://github.com/user-attachments/assets/ca183bac-342b-4c0d-9f7f-6ce599548394" />

We dont get any error as its a valid query. Also it does not display anything as category is not set to any value.

Now we are sure that this application is vulnerable to SQL injection.

In this Lab, we have to display the products which are not released (Hidden Data).

Lets make a payload

**SELECT * FROM products WHERE category = ‘or 1=1 --**

Here ‘ is closing the 1st ‘ (which is not visible and running at the backend).

We are setting a condition 1=1 which is always true and after this condition we are commenting everything else in the SQL query with the help of --

So the above query will select all the rows where category is nothing (‘’) or the conditional statement 1=1 is true (1=1 is always true) and will display all the products.

**So our payload is ‘or 1=1 --**

<img width="1100" height="473" alt="image" src="https://github.com/user-attachments/assets/b00a004c-7000-4bda-9dda-aa9b6f1ce48e" />

Now website is displaying all the products which are not released yet.

<img width="1100" height="550" alt="image" src="https://github.com/user-attachments/assets/51c2ca6a-ecf0-42e3-a8ae-dd8d7f2845fe" />

We have solved the Lab !!!














































