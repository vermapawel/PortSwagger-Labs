**Broken Access Control ||Lab #6 Method-based access control can be circumvented**

<img width="875" height="372" alt="image" src="https://github.com/user-attachments/assets/254eb879-eccb-4c7f-8ffb-2315128f6e65" />

Goal of this lab is to become administrator of the account. 

We have credentials of administrator and our account.

Lets start the lab and login via administrator

<img width="900" height="217" alt="image" src="https://github.com/user-attachments/assets/102eec12-cf19-4959-b12c-e429b490430e" />

There is a functionality to upgrade any user as administrator. Lets upgrade the user carlos

<img width="707" height="222" alt="image" src="https://github.com/user-attachments/assets/3e339254-5305-4e6e-b5ea-87de0f4f86e7" />

Carlos is an admin user now. Lets check this traffic in Burp suite

<img width="900" height="441" alt="image" src="https://github.com/user-attachments/assets/ca10dd18-e10a-4655-b54a-7e770c24b06f" />

Lets move this traffic to Repeater

<img width="900" height="512" alt="image" src="https://github.com/user-attachments/assets/8ba4fa75-ad6e-468f-bb3f-c6063e7f683a" />

This is a post request and the end point is /admin-roles. It takes username of the user and action to upgrade or downgrade. 

Lets login with normal user

<img width="900" height="265" alt="image" src="https://github.com/user-attachments/assets/5b15cc9c-c5a7-43b3-b0d8-fa833a02dc44" />

For this account we don't see admin panel as we don't have privileges.

Lets check this traffic in Burp suite

<img width="900" height="354" alt="image" src="https://github.com/user-attachments/assets/a17dac7b-a983-43ab-9b96-ff64e645b760" />

Lets copy this session ID xxoG1pU4Nfo2jICboUCRfk7ygsWnNKQx and put in /admin-roles traffic and check,

<img width="900" height="439" alt="image" src="https://github.com/user-attachments/assets/d6f76145-a8ae-494c-985d-66ffc61c9464" />

We are not authorized this normal user to change the role of any other user.

Now, lets change the method and try

<img width="737" height="702" alt="image" src="https://github.com/user-attachments/assets/edb48620-b854-4716-84d4-58e2859aece2" />

Right click and change request method

Now the method is GET, lets change the username to wiener and forward the traffic.

<img width="900" height="379" alt="image" src="https://github.com/user-attachments/assets/a33444f7-6602-4abf-a224-de9403bc9802" />

We got a 302 response.

<img width="900" height="294" alt="image" src="https://github.com/user-attachments/assets/84fc7f2b-27ce-4ab4-b182-6cfd76b2dae2" />

And lab is solved. We can see Admin panel option as wiener is ADMIN.

So, here the access control is implemented on the POST method and not on the GET method, and GET method is allowed, it has broken access control vulnerability.



