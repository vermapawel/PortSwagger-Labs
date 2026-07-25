**SSRF || Lab#3 : Blind SSRF with out-of-band detection**

<img width="870" height="562" alt="image" src="https://github.com/user-attachments/assets/49f291ac-12c7-4f5b-98f2-292565764ab1" />

Goal of this Lab is to case an HTTP request to Burp Collaborator

Lets open the lab and click on view details

<img width="876" height="592" alt="image" src="https://github.com/user-attachments/assets/7be3b3d0-845f-4e0c-a336-2246665e5c24" />

Lets intercept this traffic in Burp suite

<img width="1100" height="277" alt="image" src="https://github.com/user-attachments/assets/48f0b58a-47d3-49bb-945f-4e0aa15a4753" />

Lets move this traffic to Repeater

<img width="1100" height="421" alt="image" src="https://github.com/user-attachments/assets/4319c37a-a957-42b6-ad1e-cca5558dc2a5" />

In this lab we have a Referer header which is taking an input to track what the user is looking on the website.

Lets open Burp Collaborator Client.

<img width="811" height="491" alt="image" src="https://github.com/user-attachments/assets/630c764a-e98f-423c-b489-758d02d2ad81" />

As I am using Burp suite community, I don't have Burp Collaborator Client.

<img width="947" height="337" alt="image" src="https://github.com/user-attachments/assets/a96167d3-0ca7-440d-bcc0-4264dabe5910" />

<img width="947" height="337" alt="image" src="https://github.com/user-attachments/assets/fae60c93-2523-4ed0-88e9-fe51c03b08ec" />

This is our Burp Collaborator domain. Lets add this in the Referer and forward the traffic.

<img width="867" height="522" alt="image" src="https://github.com/user-attachments/assets/5fd31ff2-4beb-41ba-9d2e-d9da6e6cabe9" />

Lets open Burp Collaborator Client.

<img width="665" height="642" alt="image" src="https://github.com/user-attachments/assets/bebdd52a-c46b-4e5f-9546-ffdf7032a0be" />

And we are getting response from external server. It means it is vulnerable to SSRF.

Lab is solved

<img width="697" height="247" alt="image" src="https://github.com/user-attachments/assets/966bc794-70ec-4e7e-84dc-ad9779dfe579" />
