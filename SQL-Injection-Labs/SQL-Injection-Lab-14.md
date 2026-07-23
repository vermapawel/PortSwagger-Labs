**SQL Injection -- Lab #14 Blind SQL injection with time delays and information retrieval**

<img width="720" height="515" alt="image" src="https://github.com/user-attachments/assets/17ff972c-249b-4d12-a2a1-e7b7843ef548" />

Lets start the Lab

<img width="640" height="358" alt="image" src="https://github.com/user-attachments/assets/3667257f-99f9-4091-afe3-7072ab994ce1" />

**STEP 1:- Need to determine if the parameter is vulnerable to SQLi**

Lets delay the query for 10 seconds and check

***‘ || pg_sleep(10) --***

<img width="640" height="258" alt="image" src="https://github.com/user-attachments/assets/1b3e22e4-cd86-4e04-9fd6-8f55701ea303" />

We can see that Response time is approx. 10 seconds. It means that the application is vulnerable to Time Based SQLi

**STEP 2:- Need to confirm if users table exists in the Database**

To confirm we will ask Application if users table is there in the Database. If application sleeps for 10 seconds, it means users table is there. If not, there is no users table.

Lets create a use case

**‘|| (SELECT case WHEN (1=1) THEN pg_sleep(10) else pg_sleep(-1) end) --**

So, when condition is True, then the application will sleep for 10 seconds, else application will not sleep at all (-1)

As the condition is 1=1 which is always true, the application should sleep for 10 seconds. Lets validate

<img width="640" height="233" alt="image" src="https://github.com/user-attachments/assets/6f5caaa4-b165-4c12-b73a-2e9457d0b516" />

There is delay in the response.

Now if we put a false condition, there should not be any delay. Lets check

***‘|| (SELECT case WHEN (1=0) THEN pg_sleep(10) else pg_sleep(-1) end) --***

<img width="640" height="234" alt="image" src="https://github.com/user-attachments/assets/ddeae718-87f4-4161-8b1d-7b86780b7c3a" />

As we have put the condition 1=0, which is false, so the else part of the query got executed and there is no delay.

So, we have a way to ask the application True or False question.

Now lets ask the application if users table exists in the database or not.

***‘|| (SELECT case WHEN (username =’administrator’) THEN pg_sleep(10) else pg_sleep(-1) end from users) --***

In the payload we are confirming if and administrator user exists and also users table exists. If there is a delay for 10 seconds, it means both conditions are true

<img width="640" height="240" alt="image" src="https://github.com/user-attachments/assets/f7afb26f-f173-4e82-bf75-0b510569138e" />

There is a delay for 10 sec. It confirms that administrator users exists in the users table.

**STEP 3:- Need to enumerate the length of the password**

***‘|| (SELECT case WHEN (username =’administrator’ AND LENGTH(password)>1) THEN pg_sleep(10) else pg_sleep(-1) end from users) --***

We are confirming if the length of the password is greater than 10 characters. If yes, the application will sleep for 10 seconds

<img width="640" height="205" alt="image" src="https://github.com/user-attachments/assets/bcfdad89-d4a7-40a5-9af7-f98068a0a71e" />

So, it confirms that there are more than one characters in the password.

Lets check if length of the password is more than 25 characters

<img width="640" height="231" alt="image" src="https://github.com/user-attachments/assets/73577f55-fe78-4ff8-97a8-fa88696fd707" />

There is no delay, it means length of the password is not more than 25 characters.

Lets brute force the length of the password.

<img width="640" height="280" alt="image" src="https://github.com/user-attachments/assets/9f799d7c-7bcf-40f7-8c7c-6e340a3b3a53" />

<img width="640" height="208" alt="image" src="https://github.com/user-attachments/assets/c202f96f-1e51-4164-99f7-d99c733f7d31" />

We can see the difference in Response received between Request 19 and 20. So we understand that length of the password is 20 characters.

**STEP 4:- Need to enumerate the administrator password**

***‘|| (SELECT case WHEN (username =’administrator’ AND SUBSTRING(password,1,1)=’a’) THEN pg_sleep(10) ELSE pg_sleep(-1) end from users) --***

We are checking if the 1st character of the password is a or not.

<img width="640" height="229" alt="image" src="https://github.com/user-attachments/assets/14fb62dc-b682-4d4a-ba2d-427e9b9869b0" />

There is no delay, it mans its not a.

Lets brute force the 1st character of the password. We have set the sleep value to 5. We will check all alphanumeric characters.

<img width="640" height="253" alt="image" src="https://github.com/user-attachments/assets/e380b46b-7d9d-4325-a016-379b32ed9e29" />

<img width="640" height="213" alt="image" src="https://github.com/user-attachments/assets/0d55033f-d0eb-4dce-be9b-dea84d2e04ee" />

Now, in the result I don't see any sleep time of 5 seconds for any of the characters. It means there is something wrong with the attack.

At Resource pool, Default resource pool is selected which is sending 10 requests at a time.

<img width="640" height="372" alt="image" src="https://github.com/user-attachments/assets/6d7be905-c5d1-4e8b-93e3-2913a76057e5" />

We need to send one request at a time. So need to select Custom Resource Pool.

Now, in my Burp suite, I have created a Custom resource pool that will send 1 request at a time.

<img width="640" height="181" alt="image" src="https://github.com/user-attachments/assets/498d66b8-f1ad-4d20-98ca-1540c0d9187a" />

Lets start the attack again

<img width="640" height="191" alt="image" src="https://github.com/user-attachments/assets/34ef8c3f-76ff-469f-9304-ab2d1a34b120" />

We can see the Response Time is 5 seconds for d. It means 1st character of the password is d.

Now, lets brute both position and password characters simultaneously

<img width="640" height="279" alt="image" src="https://github.com/user-attachments/assets/a00b44ef-e945-49a0-a5bd-0e4c3c31357f" />

As we know that password length is 20. We are selecting 20 numbers for brute forcing.

And for passwords characters we are selecting alphanumeric characters.

Also, we are choosing Custom response time which will send one request at a time.

<img width="640" height="271" alt="image" src="https://github.com/user-attachments/assets/ad1cac62-5950-446d-9e6b-cf563d2d4ea5" />

<img width="640" height="218" alt="image" src="https://github.com/user-attachments/assets/b430bbff-58ff-4543-9108-d212c1069651" />

We will mainly focus on Response received. We can arrange the characters as per payload 1 and we will get the password

dj3nszleco9z2wbh1bco

Lets login with Administrator

<img width="640" height="395" alt="image" src="https://github.com/user-attachments/assets/df844739-848e-4299-a796-2258ae71e909" />

Lab is solved !!!!




