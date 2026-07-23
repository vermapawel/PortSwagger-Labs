**XSS || Lab #14 Exploiting cross-site scripting to steal cookies**

<img width="855" height="583" alt="image" src="https://github.com/user-attachments/assets/195d0f17-3e86-42b1-8986-da579953ebeb" />

Goal of this Lab is to steal session cookie by exploiting Stored XSS vulnerability in comment functionality.

As per Lab description we have to use Burp Collaborator’s default public server. This feature is only available in the Professional version of Burp suite. I don't have Professional version of Burp so I will be putting screen shots.

Lets start the Lab

<img width="1020" height="645" alt="image" src="https://github.com/user-attachments/assets/09e26c1f-f0ef-4779-8373-c2eb82721a82" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

When we view any post there is a feature the post comments. Lets check

<img width="882" height="658" alt="image" src="https://github.com/user-attachments/assets/9300900c-0b52-41a1-8d2f-11bf59ddce01" />

<img width="925" height="372" alt="image" src="https://github.com/user-attachments/assets/a50dac76-d4bc-4eaa-909b-9f99dd53e709" />

<img width="931" height="559" alt="image" src="https://github.com/user-attachments/assets/de6cc384-eb18-446a-94e0-0e7dc4a1195b" />

We can see that Name field (test1) is reflected back to us. Also test1 is a hyperlink it means website field also got reflected back. And comment field is reflected back as well.

So we need to check all these three field for XSS vulnerability.

Lets start with comment field and check if its vulnerable to XSS

<script>console.log(“hello!!”)</script>

Its a simple script that output a string in the web console

<img width="901" height="696" alt="image" src="https://github.com/user-attachments/assets/21c734e7-0da8-42e0-9bbc-5e44eb346048" />

<img width="825" height="523" alt="image" src="https://github.com/user-attachments/assets/fc4056d8-869c-4b9f-b4d4-c2441e0993b0" />

Now, we don’t see our script is displayed here. It means that its get executed as a code. Lets validate

<img width="1100" height="391" alt="image" src="https://github.com/user-attachments/assets/74148f7e-df8c-4dd9-946f-b4ceb7f5f5c1" />

We can see that hello!! got printed in the Console tab of the Developers tool. So definitely comment filed is vulnerable to XSS.

So now we will try to steal the session token cookie of the user that visits this page.

Lets write down the script

<img width="1100" height="523" alt="image" src="https://github.com/user-attachments/assets/6ee7705d-e1c0-45a0-aef4-419064c37348" />

fetch() → This will output the cookie of the user that visits the page and it will send to the attacker-controlled server.

method is POST

body: document.cookie → It will add the cookie of the user in the body of the request.

mode: ‘no-cors’ → It will not output any error when browser will try to get a response of the PORT request it will send to the attacker-controlled server.

For attacker-controlled server, we will use Burp collaborator feature in the Burp which is only available in the Professional version.

<img width="1014" height="702" alt="image" src="https://github.com/user-attachments/assets/0c0837f2-ae33-4d84-9e50-06bd49fc114e" />

<img width="987" height="697" alt="image" src="https://github.com/user-attachments/assets/29fad137-7b16-4e16-83ee-6f11a3ab5c87" />

And paste in the script

<img width="757" height="172" alt="image" src="https://github.com/user-attachments/assets/a06ff945-aaea-4bac-99e1-1f7ae0e2fbf3" />

Lets put this script in the comment of the post

<img width="747" height="538" alt="image" src="https://github.com/user-attachments/assets/e2c0dbf6-3e43-47fe-bd44-fc9537f1263d" />

<img width="834" height="370" alt="image" src="https://github.com/user-attachments/assets/d594211a-6976-413e-b654-47a393a03caa" />

Now we will wait for the simulated user to view to blog to trigger our script

<img width="1036" height="700" alt="image" src="https://github.com/user-attachments/assets/46aaf409-f815-4322-9e32-4ac74996e7d4" />

We can see that there is a HTTP request coming from IP 34.251.122.40.

<img width="949" height="553" alt="image" src="https://github.com/user-attachments/assets/793bdcdb-eeed-4585-8b58-bb5ecb55cd3b" />

We can see that there are two cookies set for the user, secret and session

Lets copy the session cookie and check for user details.

<img width="1100" height="268" alt="image" src="https://github.com/user-attachments/assets/a0c7c328-6800-4b61-aecb-917e70b70840" />

In the Application tab of the developer's tool, we can see our cookie which is unauthenticated cookie (as we are not logged in).

We will replace wit with the authenticated cookie that we have captured.

<img width="1100" height="606" alt="image" src="https://github.com/user-attachments/assets/4a2241f9-c04c-4d7d-8fd9-a2e2f2d5cc27" />

And the Lab is solved !!!

<img width="868" height="415" alt="image" src="https://github.com/user-attachments/assets/67db4e77-1588-4b35-b680-e03748450e7c" />

We have compromised the administrator cookie
