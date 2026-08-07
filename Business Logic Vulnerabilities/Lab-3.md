**Business Logic Vulnerabilities || Lab#3 || Inconsistent security controls**

<img width="791" height="392" alt="image" src="https://github.com/user-attachments/assets/baf2561f-6232-4c8a-88a5-f557edc41361" />

Goal of this lab is to delete carlos user

Lets start the lab

<img width="810" height="492" alt="image" src="https://github.com/user-attachments/assets/709af6e4-a1d8-468d-a906-051377e61ee8" />

Now, we need to find Admin Panel. Lets try some common keywords

<img width="1000" height="273" alt="image" src="https://github.com/user-attachments/assets/ec676b9c-a74e-4a30-98c0-8dc93a15f638" />

And we found the Admin panel, however we have to be DontWannaCry use to access it.

Lets click on Register

<img width="760" height="437" alt="image" src="https://github.com/user-attachments/assets/98256753-0a31-4364-8133-551822307088" />

<img width="972" height="312" alt="image" src="https://github.com/user-attachments/assets/3581e930-d662-4858-8aec-a62cf7276250" />

As we dont have access to the test@dontwannacry.com, lets check if we can login without registration

<img width="801" height="390" alt="image" src="https://github.com/user-attachments/assets/9a7138fb-49e0-44e2-b53d-430088f862d0" />

And we are not able to. So it looks like we have to complete the Registration first.

Lets go to the email client.

<img width="917" height="382" alt="image" src="https://github.com/user-attachments/assets/0798f405-caa6-4d72-ab3a-5d303b468e49" />

<img width="1000" height="302" alt="image" src="https://github.com/user-attachments/assets/caaf8992-5ec3-4c03-9dd4-39d89359bd1a" />

Lets again Register using this email address

<img width="832" height="452" alt="image" src="https://github.com/user-attachments/assets/316c5705-1b53-49b4-9208-9a6eaaec7f66" />

<img width="835" height="275" alt="image" src="https://github.com/user-attachments/assets/5169f23f-3ed1-49b1-9184-1b6ae14ed9d4" />

Lets go to email client.

<img width="1000" height="358" alt="image" src="https://github.com/user-attachments/assets/6f18b4ec-9140-4333-bb5d-d7d61460ede3" />

Lets go to the link and complete registration

<img width="846" height="277" alt="image" src="https://github.com/user-attachments/assets/7f36fe7b-8c3c-44e3-883e-b6615363d114" />

Lets try to login again

<img width="777" height="297" alt="image" src="https://github.com/user-attachments/assets/813d39e6-95b7-4a2a-82fd-d270e610b2ee" />

We are able to login. However we will not be able to access the Admin panel.

We have a functionality to update email address.

<img width="1000" height="355" alt="image" src="https://github.com/user-attachments/assets/9445e64b-6a46-4be6-ba8d-7fb40a73280e" />

We are able to update the email address without any confirmation. Now we have access to Admin panel as well

<img width="1000" height="282" alt="image" src="https://github.com/user-attachments/assets/d1589b05-a32a-46a4-aeac-e181e3a49e75" />

To solve the lab, we need to delete carlos user. Lets delete it

<img width="1000" height="366" alt="image" src="https://github.com/user-attachments/assets/011bdb36-e815-43ac-b344-2d06aa2319f5" />

And lab is solved
