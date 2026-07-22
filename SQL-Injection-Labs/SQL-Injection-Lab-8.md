**SQL Injection -- Lab #8 SQLi attack, querying the database type and version on MySQL & Microsoft**

<img width="1100" height="533" alt="image" src="https://github.com/user-attachments/assets/01ea0cfe-6a60-4e71-870b-c7442781227b" />

As per description of the Lab, product category is vulnerable to SQLi.

End goal of the lab is to display the database

Lets start the Lab

<img width="1100" height="743" alt="image" src="https://github.com/user-attachments/assets/d2eaad14-982e-45b1-8275-95e9e933a171" />

As per Lab description Product Category is vulnerable to SQL injection attack.

Lets quickly validate

<img width="1072" height="328" alt="image" src="https://github.com/user-attachments/assets/e06912ee-e4ce-4b18-8685-d7389456aba1" />

We got an error message. It means this application should be vulnerable to SQLi.

Now we can take a guess that there are two columns. One for Title and one for articles.

<img width="1100" height="632" alt="image" src="https://github.com/user-attachments/assets/3d45f481-05d8-4f6f-8297-cfc0236111b3" />

Lets validate

<img width="1100" height="463" alt="image" src="https://github.com/user-attachments/assets/9c4b7c44-9957-4ffd-bd36-724d594e851d" />

Ctrl+U will encode the URL

We got an error. Which is weird. We can see that there are at least two columns.

Now, some database user # for commenting instead of --

Lets try with #

<img width="1100" height="358" alt="image" src="https://github.com/user-attachments/assets/b62c4a16-10c9-4ba0-b7da-a208f8d9d169" />

This time we got HTTP 200 response.

Lets try again

<img width="1100" height="413" alt="image" src="https://github.com/user-attachments/assets/6a12d1e7-911d-48bc-b2de-7d943505e3cf" />

Again we got HTTP 200 response. Lets try again

<img width="1100" height="416" alt="image" src="https://github.com/user-attachments/assets/33a401dc-8a96-420f-9703-fedbe17a6e57" />

This time we got Server Error.

It means there are two columns in the Table.

Now we need to identity the Data type of the columns

Our payload will me

***web-security-academy.net/filter?category=Accessories’ UNION SELECT ‘a’ , NULL#***

<img width="1100" height="424" alt="image" src="https://github.com/user-attachments/assets/62954241-84ad-4f5f-9d9b-41ba4cf9d5f3" />

We got a HTTP 200 response. It confirms that first column is Strings data type.

Lets check for second column data type

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT NULL, ‘a’#***

<img width="1100" height="463" alt="image" src="https://github.com/user-attachments/assets/ebbed9ae-0e11-4c05-bf44-7d20ed004a3c" />

We got a HTTP 200 response.

So we confirmed that both columns are Strings data type.

Now, we need to output the version of the version of the Database

Lets check the Cheat sheet for the query

<img width="1078" height="436" alt="image" src="https://github.com/user-attachments/assets/88ad6a32-e6e2-48cf-b486-c49f8bc6791d" />

Lets try the query for Microsoft query SELECT @@version

Payload will be like this

***web-security-academy.net/filter?category=Lifestyle’ UNION SELECT @@version, NULL#***

<img width="1100" height="410" alt="image" src="https://github.com/user-attachments/assets/1cdfa733-1f6c-4219-a369-84a863e708c2" />

And we got a 200 response and we got the version of the Database

<img width="952" height="538" alt="image" src="https://github.com/user-attachments/assets/ace6fcbf-339e-4ca3-823d-31e4cc36b488" />

Lets forward this traffic to Application

<img width="1100" height="468" alt="image" src="https://github.com/user-attachments/assets/dcb7eb12-1428-47f8-86e9-f39a2df709eb" />

And out Lab is solved !!











