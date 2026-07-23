**SQL Injection -- Lab #17 SQL injection with filter bypass via XML encoding**

<img width="720" height="478" alt="image" src="https://github.com/user-attachments/assets/16a88827-a044-4a01-9364-3037ed67c009" />

End goal of the Lab is to login as administrator

Lets start the Lab

<img width="640" height="473" alt="image" src="https://github.com/user-attachments/assets/6c92b1f9-d529-47dc-b59d-ff14f8b01648" />

Now as per lab description, the vulnerability in Stock Check feature.

<img width="640" height="432" alt="image" src="https://github.com/user-attachments/assets/bdd21e8b-0548-4ce0-9d27-5157199a17f2" />

Lets click on Check stock and capture its traffic in burp

<img width="640" height="388" alt="image" src="https://github.com/user-attachments/assets/a7b68b5c-80c0-40ff-918d-99534b795d7e" />

Lets move this traffic to Repeater and forward this traffic

<img width="640" height="338" alt="image" src="https://github.com/user-attachments/assets/67159816-616d-4b57-9582-9c5ed4c3ca8c" />

Now, it seems that some query is running at the backend. Its setting productID as 1, storeID as 1 and then its displaying how many units are left in the store.

Now, if this query is not properly parameterized, we can exploit if to enumerate contents of the database.

Lets validate

<img width="640" height="330" alt="image" src="https://github.com/user-attachments/assets/ea0b23ee-b80b-4772-824e-357d6c8ba465" />

We get a message “Attack detected’

Lets check the Hint of this Lab

<img width="640" height="141" alt="image" src="https://github.com/user-attachments/assets/3aafd469-f50b-4c7b-82e3-50dc893c2cd5" />

There is a WAF which will block any content that looks like SQL query.

Now, as hint suggest, we need to use a Burp suite extension Hackvertor

<img width="640" height="355" alt="image" src="https://github.com/user-attachments/assets/0142342a-b0e4-4a37-ba7e-be9060b83b9d" />

<img width="640" height="518" alt="image" src="https://github.com/user-attachments/assets/daab90d9-b6d0-4977-85a0-27e97a2f6ab5" />

We can encode the input 1 UNION SELECT NULL in hex_entities

Lets test

<img width="640" height="487" alt="image" src="https://github.com/user-attachments/assets/46eda412-3dac-4a07-b8dc-8e3d099f8cc9" />

This time we dont get that message.

Now, Lets use two null in the payload. If we still get the output, it means there are two columns in the Database

<img width="640" height="510" alt="image" src="https://github.com/user-attachments/assets/12e19256-8501-4517-8261-a34378dc148b" />

We dont get the number of units. It means there are one column in the Database.

Now, we need to two columns to display username and password. However there is only one column.

Lets create a payload

***1 UNION SELECT username || ‘-’ || password FROM users***

<img width="640" height="531" alt="image" src="https://github.com/user-attachments/assets/1ff8db0f-785a-45ec-8679-1963c584f9f1" />

We got the username and password.

Lets try to login

<img width="609" height="453" alt="image" src="https://github.com/user-attachments/assets/c0163b63-4ef3-4519-bab4-25bfa2cea3c7" />

And Lab is solved !!








