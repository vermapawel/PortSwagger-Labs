**SQL Injection -- Lab #11 Blind SQL injection with conditional responses**

<img width="1100" height="549" alt="image" src="https://github.com/user-attachments/assets/e76a6eb5-026f-45a3-9e4e-da11a7fdc834" />

Lets start the Lab

When we go to the different Categories, we can see one **Welcome back** message

<img width="1100" height="438" alt="image" src="https://github.com/user-attachments/assets/39b0d08b-cafa-41d9-b417-371d729f0e86" />

Lets open the Burp suit

Click on ‘Home’ and intercept the traffic

<img width="1100" height="484" alt="image" src="https://github.com/user-attachments/assets/f879c016-af82-439d-bdbd-d3d80f0802b2" />

We can see two Cookies **TrackingID** and **Session**

Now first we need to confirm if the application is vulnerable to Blind SQLi

Lets try to Imagin how the query looks at the backend

SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’

Now if this tracking ID already exists in the Database, then this query returns a tracking and it should be a Welcome back! message.

<img width="1100" height="406" alt="image" src="https://github.com/user-attachments/assets/2f06728c-5db8-4084-baa4-3e1ed6547e98" />

We got the Welcome Back! message

If this tracking ID kxGAznznU8JGOP4c is not in the database, the query will return nothing and we don’t get a Welcome back! message.

Lets confirm.

<img width="1100" height="376" alt="image" src="https://github.com/user-attachments/assets/a13f6e4a-8d22-48e4-8572-7fa0b90c55f0" />

We have edited the TrackingID and we dont get the Welcome Back! message as this edited TrackingID is not in the Database.

It means that there is a different behavior when tracking ID is present in Database and when tracking ID is not present in Database.

To confirm if the application is vulnerable to Blind based SQLi, we have to enforce a True used case and confirm its reaction (return Welcome back!) and enforce a False used case and confirm its reaction (no Welcome back returns).

The backend query looks something like this:-

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’***

Lets create a payload

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND 1=1 --'***

We have we added ' which will close the 1st '

We have also added one condition 1=1 using AND operator and commented rest of the query.

Lets understand the query

We are selecting one tracking-id from tracking-id table where tracking ID is kxGAznznU8JGOP4c and 1=1

Now we know that tracking ID kxGAznznU8JGOP4c exists in the database so trackingID = ‘kxGAznznU8JGOP4c’ will be true and 1=1 will always be true.

So the query is True and it will results in displaying Welcome back! message.

Lets validate

<img width="1100" height="398" alt="image" src="https://github.com/user-attachments/assets/9c0dad1a-7140-4fcd-aa62-90c1d0b1140f" />

We got **Welcome back!** message

Now, if we can prove that we dont get a Welcome back! when the used case is false, then we have a exploitable Blind based SQLi.

SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ **AND 1=0 -- '**

Here we have put 1=0 which is false, so the complete statement will become false and there will be no **Welcome back!** message.

<img width="1100" height="413" alt="image" src="https://github.com/user-attachments/assets/b1c21c47-5746-43ca-9ca0-3714faef3cb4" />

We dont get Welcome back! message.

So we proved that application responded differently at True used case and at False used case.

Now, we will confirm if the Database has users table or not

If we get a Welcome back! message, it means users table exists.

Lets create a payload

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND (SELECT ‘x’ FROM users LIMIT 1)=’x’ — '***

<img width="1100" height="379" alt="image" src="https://github.com/user-attachments/assets/dc0fe4c8-4c85-4b9f-b641-7fb5f5678845" />

We got a Welcome back! message. It means **users** table is there in the Database.

Now, we need to confirm if username **administrator** exists in the **users** table or not.

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND (SELECT username FROM users WHERE username=’administrator’)=’administrator’ --***

<img width="1100" height="378" alt="image" src="https://github.com/user-attachments/assets/48bbaa91-19a6-44bf-97aa-a2b21534fdc7" />

We got Welcome back! message. It means administrator is there in the users table.

Now we will enumerate the password for the administrator user

First we need to know the length of the password.

Now we know the length of the password, we will ask the application a series of True and False questions.

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND (SELECT username FROM users WHERE username=’administrator’ and LENGTH(password)>1)=’administrator’ --'***

<img width="1100" height="391" alt="image" src="https://github.com/user-attachments/assets/a782559b-c8bc-488d-8fae-7d85e2b3d436" />

We got the Welcome back! message it means password length is greater than 1, which is obvious.

Lets check if password length is greater than 30

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND (SELECT username FROM users WHERE username=’administrator’ and LENGTH(password)>30)=’administrator’ --'***

<img width="1100" height="387" alt="image" src="https://github.com/user-attachments/assets/6a215271-f129-4d22-9150-692ac6c48712" />

This time we don't get Welcome back! message. It means password length is less than 30.

To make it easy, lets brute force it

In the Burp Suite, sent the request in Intruder for brute forcing

<img width="1100" height="431" alt="image" src="https://github.com/user-attachments/assets/f7f0b3dc-af71-4f25-b92d-d2a4329f27ec" />

Lets start the attack

<img width="1100" height="397" alt="image" src="https://github.com/user-attachments/assets/1e2fa5d4-1e41-4bb3-a7e3-adda343be71e" />

We can see the change in Length at Request 20. Lets see if that request has Welcome back! message or not.

<img width="1100" height="414" alt="image" src="https://github.com/user-attachments/assets/7ea864ac-2ef5-4513-ac98-b69ce67c290f" />

It don't have Welcome back! message.

Lets check the Request number 19.

<img width="1100" height="485" alt="image" src="https://github.com/user-attachments/assets/885ce93e-c787-4ef5-b76e-cad142bd790c" />

<img width="1100" height="485" alt="image" src="https://github.com/user-attachments/assets/ee4c8d23-9443-459c-bc89-bf92f106b42f" />

On request 19 there is Welcome back! message.

It means password length is 20 as we have set the condition greater than (>). So the next payload will be greater than 20 where there is not Welcome back! message. So the password length is greater than 19 and not greater than 20, So its length is 20.

Now we know the password, we will ask the application a series of True and False questions like,

If the 1st character of the password is a. If we don't get the Welcome back! message, then we will ask if 1st character of the password is b. Again, if we don't get the message, we will ask if 1st character is c.

Lets say we get the Welcome back! message. So we know that password starts with c

Now again we will ask the application if the 2nd character is a. If we don't get the Welcome back! message, then we will ask if 2nd character of the password is b and we will continue the same process to guess the complete password.

***SELECT tracking-id FROM tracking-table WHERE trackingID = ‘kxGAznznU8JGOP4c’’ AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username=’administrator’)=’a’ --'***

<img width="1100" height="448" alt="image" src="https://github.com/user-attachments/assets/cb36aa3f-d154-4e0d-b4b7-5795681b909c" />

And we don't get Welcome back! response. It means 1st character of the password it not a.

Lets use a different type of attack called Cluster Bomb

In this type of attack, we can set multiple payload and brute force.

<img width="1100" height="397" alt="image" src="https://github.com/user-attachments/assets/dfe2efb8-a53a-4bfa-a005-7e654f48e6cf" />

<img width="1100" height="442" alt="image" src="https://github.com/user-attachments/assets/c3a3e2cf-d9bb-4b8a-9aba-80b7fe222f59" />

<img width="1100" height="323" alt="image" src="https://github.com/user-attachments/assets/969eb0d0-da46-4761-ae33-51ea30541a66" />

We can see the difference in length. Most payload has a length of 11574. Some of them are having length of 11635.

All those payloads having length of 11635. We can confirm that those payloads have Welcome back!

Can can short the output as per length.

<img width="1100" height="431" alt="image" src="https://github.com/user-attachments/assets/80dbecb8-97b2-4bdc-a974-eb68473b584d" />

Now, Payload 1 which is the 17th character of the password has value of b. It means the 17th character of the password is b. Similarly, 19th character of the password is also b.

According to this we have got the password o64cpw70wye3tpy6buby

Lets try to login as administrator

<img width="1100" height="453" alt="image" src="https://github.com/user-attachments/assets/7cce173e-98c7-45ff-9ab7-72fd81bf5b4e" />

And we are logged in and lab is solved.






