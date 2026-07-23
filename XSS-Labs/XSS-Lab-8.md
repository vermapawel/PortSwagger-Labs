**XSS || Lab #8 Stored XSS into anchor href attribute with double quotes HTML-encoded**

<img width="720" height="393" alt="image" src="https://github.com/user-attachments/assets/391cf9e6-9211-4447-b24f-315636efe2a5" />

End Goal of the lab is to submit a comment that calls the alert function when the comment author name is clicked.

Lets start the Lab

<img width="640" height="557" alt="image" src="https://github.com/user-attachments/assets/710d5d0d-bc6a-4310-8eb2-6da3696d8475" />

Click on View Post and there is an option to post a comment.

<img width="640" height="429" alt="image" src="https://github.com/user-attachments/assets/d7816ae0-038a-42af-abd7-d6265eac097e" />

<img width="640" height="248" alt="image" src="https://github.com/user-attachments/assets/5ad12ee7-93f3-4250-b3d9-1d6228643738" />

<img width="640" height="362" alt="image" src="https://github.com/user-attachments/assets/244167ad-d652-451f-88c4-d668f7f6ec62" />

We can see that the name and comments are reflected back

Lets intercept the traffic in Burp

<img width="640" height="325" alt="image" src="https://github.com/user-attachments/assets/195eab2b-0566-4261-8e64-c25bfcc337e5" />

We can see that there are 3 places where strings got stored. 1st is the href attribute. 2nd is for the name parameter and 3rd is for comment parameter.

All 3 parameter should be tested for XSS vulnerability.

<img width="640" height="476" alt="image" src="https://github.com/user-attachments/assets/8327e2a0-8d08-4a60-b7a6-4936f6335f7a" />

<img width="640" height="202" alt="image" src="https://github.com/user-attachments/assets/34d0e5af-a392-4190-8665-768608acc994" />

<img width="640" height="338" alt="image" src="https://github.com/user-attachments/assets/485f0a73-638f-42b6-9179-d7790ffe0aa7" />

Now it seems like < is URL encoded in comment field and name field.

< is also encoded in the website filed but it seems some different rules are applied here. Lets test

href=”<&quot;”>

Lets put the payload here

***href=”javascript:alert(1)”>***

<img width="640" height="444" alt="image" src="https://github.com/user-attachments/assets/d5d09489-362d-4be4-acdf-d72c03ebb396" />

<img width="640" height="368" alt="image" src="https://github.com/user-attachments/assets/073096ae-5d49-4a8d-bfa4-dda08f878e7f" />

And the Lab is solved. And if we click on Test we will get an alert message.

<img width="640" height="332" alt="image" src="https://github.com/user-attachments/assets/91aee2a6-e49c-4b39-a597-ceac2d78b0ec" />












