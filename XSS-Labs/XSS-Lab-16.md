**XSS || Lab #16 Exploiting XSS to bypass CSRF defenses**

<img width="1100" height="588" alt="image" src="https://github.com/user-attachments/assets/c82961e6-122e-4600-b417-1141287bd1ef" />

Goal of this lab is to steal a CSRF token and change the email address of a user how views the blog post comments

Our credentials is wiener:peter

Lets start the Lab

<img width="1100" height="557" alt="image" src="https://github.com/user-attachments/assets/1ad7edbc-a1b7-47e9-8db6-73e82f63d9da" />

Login with the credentials provided wiener:peter

<img width="1100" height="386" alt="image" src="https://github.com/user-attachments/assets/aad6f9a6-0506-422a-a9c9-f4daba305267" />

Here we can update the email.

<img width="1100" height="381" alt="image" src="https://github.com/user-attachments/assets/637202f8-113e-4187-81e0-a7a0408c3fde" />

Lets intercept its traffic in Burp suite

<img width="1100" height="636" alt="image" src="https://github.com/user-attachments/assets/c3c04bac-7d7e-4635-9160-92d545e66a15" />

This is the traffic to change the email address on the account.

<img width="1100" height="602" alt="image" src="https://github.com/user-attachments/assets/36668a24-e638-4e0e-b75f-aa652b9cd1e5" />

At the bottom we can see email address that we put and a CSRF token

email=test%40test.com&csrf=zVsFh5u4WsE1urdWW3325R93VuOFG6GF

CSRF stands for Cross Site Request Forgery.

<img width="1100" height="399" alt="image" src="https://github.com/user-attachments/assets/fe02401a-d84b-4c11-882e-2bfe82f0aae7" />

Now, to prevent this type of attack, application use CSRF token which are random token stored at client side.

<img width="1100" height="428" alt="image" src="https://github.com/user-attachments/assets/d4b1ffc4-0ce6-4c47-94d0-0e8fc6a2bb4f" />

However, if there is any XSS vulnerability in the application, then attacker can send a request to 1st obtain the SCRF token and then perform another request in order to get user change his email address or any other request that attacker wants.

Now, 1st we need to find XSS vulnerability in the application.

In the post, there is an comment option. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

<img width="882" height="658" alt="image" src="https://github.com/user-attachments/assets/d1fbf6e9-b891-4ff7-9ae9-77aecaab31ed" />

<img width="925" height="372" alt="image" src="https://github.com/user-attachments/assets/0355aecf-02a0-4ecf-b0aa-33e8a7f19df6" />

<img width="931" height="559" alt="image" src="https://github.com/user-attachments/assets/1790bb19-f4f7-43ac-9cf8-1c0c922336ae" />

We can see that Name field (test1) is reflected back to us. Also test1 is a hyperlink it means website field also got reflected back. And comment field is reflected back as well.

So we need to check all these three field for XSS vulnerability.

Lets start with comment field and check if its vulnerable to XSS

&lt;script&gt;console.log("hello!!")&lt;/script&gt;

Its a simple script that output a string in the web console

Now if the comment field is not vulnerable to XSS, the application will take it like a string and it will be displayed in the comment section.

However if its vulnerable to XSS, there will no comment and we will get a hello!! printed in the console panel of the developers tool.

<img width="901" height="696" alt="image" src="https://github.com/user-attachments/assets/0ac759cd-3108-4938-9b55-40c573006580" />

<img width="825" height="523" alt="image" src="https://github.com/user-attachments/assets/84232fb0-742b-4b0e-a446-79f57a019637" />

Now, we don’t see our script is displayed here. It means that its get executed as a code. Lets validate

<img width="1100" height="330" alt="image" src="https://github.com/user-attachments/assets/e138ea18-c8e6-4564-84eb-b750d4dc388d" />

We can see that hello!! got printed in the Console tab of the Developers tool. So definitely comment filed is vulnerable to XSS.

Now, we need to get the CSRF token. Lets write a scrip for that

<img width="812" height="523" alt="image" src="https://github.com/user-attachments/assets/c5f4d8ed-f0e4-43dc-a58b-b0c89f3c2e9d" />

Lets put this script in the comment field

<img width="886" height="636" alt="image" src="https://github.com/user-attachments/assets/d3a93ad9-6f77-424e-ab76-770ec6701bda" />

And as we post comment, the lab is solved

<img width="1100" height="360" alt="image" src="https://github.com/user-attachments/assets/d5414fb6-5b1b-476d-9925-0a79285585c3" />

