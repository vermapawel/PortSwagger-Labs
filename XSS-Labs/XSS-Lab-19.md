**XSS || Lab #19 Reflected XSS with some SVG markup allowed**

<img width="832" height="487" alt="image" src="https://github.com/user-attachments/assets/cc0c6d83-3c55-41f8-a2ce-40c44e21e3a0" />

Goal of this Lab is to perform a cross-site scripting attack that calls the alert() function.

Lets start the Lab

<img width="817" height="592" alt="image" src="https://github.com/user-attachments/assets/7bb4a281-2726-47c5-80fb-a659ff5c3298" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

We have a search parameter in the application. Lets check

<img width="858" height="379" alt="image" src="https://github.com/user-attachments/assets/9eb1e460-cef7-489a-88b9-fad737234b53" />

We can see that the string that we have put in the search parameter got reflected back. So this search parameter needs to check if it has XSS vulnerability.

Lets put a simple script and check

&lt;script&gt;alert(1)&lt;/script&gt;

<img width="1072" height="358" alt="image" src="https://github.com/user-attachments/assets/d1bda059-a787-4d92-bd86-914177e4aa38" />

<img width="964" height="247" alt="image" src="https://github.com/user-attachments/assets/1e38370e-67a5-42a3-ae2b-4e349d30b526" />

We got a message that this tag is not allowed. It means there is some kind of Firewall or some kind of validation in the backend that is checking for certain tags and blocking them.

Lets intercept the traffic is Burp suite

<img width="1100" height="386" alt="image" src="https://github.com/user-attachments/assets/d8ccccb2-322a-4108-b960-249dd3ea631e" />

We will brute force all and check which Tags are allowed. Lets move this traffic to Intruder

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

<img width="1100" height="586" alt="image" src="https://github.com/user-attachments/assets/e2c4f420-d442-419a-b982-60f7c59797f1" />

<img width="1100" height="437" alt="image" src="https://github.com/user-attachments/assets/c8bb4c42-a521-4e83-ad4e-bd2517aec3a0" />

Lets start the attack

<img width="1100" height="284" alt="image" src="https://github.com/user-attachments/assets/738af593-a42f-4868-87ea-21942545b799" />

There are few 200 response code it means these tags are allowed.

In this lab we need to use SVG tag. Lets find the payload for this tag

From the brute force attack we know that animatetransform tag is allowed.

<img width="1100" height="808" alt="image" src="https://github.com/user-attachments/assets/039a96f2-1ebb-43ff-b7b9-9cf586a24657" />

&lt;svg&gt;&lt;animatetransform onbegin=alert(1) attributeName=transform&gt;

Lets use this tag

<img width="934" height="460" alt="image" src="https://github.com/user-attachments/assets/f6bf16a6-cdd2-4094-943f-25ba428fa9db" />

We got an alert in the form of pop-up message.

<img width="906" height="400" alt="image" src="https://github.com/user-attachments/assets/cbc1f94a-6353-4955-8350-e49e9acd4509" />

And Lab is solved !!

<img width="1100" height="493" alt="image" src="https://github.com/user-attachments/assets/23b9c37d-326f-4b19-a41e-64e0afc9e358" />






