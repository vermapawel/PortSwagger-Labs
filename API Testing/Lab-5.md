**API Testing || Lab#5 || Exploiting server-side parameter pollution in a REST URL**

<img width="776" height="545" alt="image" src="https://github.com/user-attachments/assets/2e5a6c6b-cea0-49b0-9197-b2239ad4fad9" />

Goal of this lab is to login as administrator and delete user carlos. 

Lets start the lab and go to home.

<img width="957" height="442" alt="image" src="https://github.com/user-attachments/assets/d2573632-b1fb-4a2e-9b7c-f8b13c54ba55" />

There is a functionality Forgot password. We know that there is a user administrator.

Lets check

<img width="532" height="232" alt="image" src="https://github.com/user-attachments/assets/1172fc6b-fba7-4e24-99c8-608d11024047" />

It seems that password link is sent to the email address. We dont have access to this email

Lets check this traffic in Burp

<img width="1000" height="431" alt="image" src="https://github.com/user-attachments/assets/42059017-d4b2-450c-8928-dd7c510ef5a3" />

Lets move this traffic to Repeater

Now, lets modify the username and check

<img width="1000" height="479" alt="image" src="https://github.com/user-attachments/assets/ac827223-8fb7-4ea7-af55-10eb298652f9" />

It says this username does not exist.

Lets try again

<img width="1000" height="448" alt="image" src="https://github.com/user-attachments/assets/8392a80a-426f-4936-b39a-fb71a77e5576" />

And this time we get a different error. Its saying Invalid route. It gives us hint regarding LFT

Lets try

<img width="1000" height="477" alt="image" src="https://github.com/user-attachments/assets/d2e962f5-9bd8-4b3c-8be7-18bece8d4d0b" />

We got an error. 

Now, there is a file called openapi.json. This file is essentially the blueprint of an API written in JSON format. It follows the OpenAPI Specification (OAS), which is a standard way to describe RESTful APIs. 

Lets check if we can access this file.

<img width="1000" height="429" alt="image" src="https://github.com/user-attachments/assets/570df467-b202-40d4-a0cb-37c39b660219" />

We got an error, however we got a path

***api/internal/v1/users/{username}/field/{field}***
 
Lets put this path in the username parameter and check

<img width="1000" height="451" alt="image" src="https://github.com/user-attachments/assets/345c771c-5957-42c5-967d-771b4daf3015" />

Its saying username does not exist. Lets put username as administrator

<img width="1000" height="486" alt="image" src="https://github.com/user-attachments/assets/6af556a7-bcdd-4a9e-b26c-eefcfcf4b3d1" />

Now this time its saying field name field does not exists

<img width="1000" height="499" alt="image" src="https://github.com/user-attachments/assets/c8d37af3-f16b-49ad-b1dc-afae9be55124" />

This time we got administrator user details.

Lets check any other field like email

<img width="1000" height="501" alt="image" src="https://github.com/user-attachments/assets/e6ac36b0-bfcb-4e4e-b2bc-f94ea9a285ef" />

We got 200 OK response. So it seems field is giving us all fields available in user schema.

Lets check if we can get anything with password

<img width="1000" height="486" alt="image" src="https://github.com/user-attachments/assets/6d208f0b-8876-4305-b286-687763a5e20d" />

Password filed does not exists.

Now we need to find a way to reset / change the password of administrator.

Lets check forgot password traffic.

This is a request for forgot password in Javascript.

<img width="1000" height="468" alt="image" src="https://github.com/user-attachments/assets/0465ee7e-0a78-4c2b-af35-3a461f088b77" />

There is a variable passwordResetToken which holds the token for password reset. 

Also its path is /forgot-password?passwordResetToken=&lt;token&gt;

Lets check if passwordResetToken filed is present.

<img width="1000" height="458" alt="image" src="https://github.com/user-attachments/assets/eacbf9d4-2614-4665-a4ff-2d1d91ca2b2e" />

We got the password reset token. 

Now, lets put this token in the password reset path and put in the URL.

/forgot-password?passwordResetToken=19dgnppaxebkmdcspibx2q16yvt8j0dd

<img width="1000" height="324" alt="image" src="https://github.com/user-attachments/assets/c68a06e8-f20b-4d0f-8b0a-d7beaa263c92" />

We got an option to change the password. Lets changed the password for administrator. 

Lets login

<img width="1000" height="312" alt="image" src="https://github.com/user-attachments/assets/7a3ee4a2-88d9-4d2c-85bc-e1c628b81d8e" />

We have access to Admin panel. To solve the lab we have to delete carlos user

<img width="1000" height="268" alt="image" src="https://github.com/user-attachments/assets/a34f3ede-bf99-499f-99eb-80641a4fd7cb" />

<img width="1000" height="314" alt="image" src="https://github.com/user-attachments/assets/44602757-8d73-451b-88c3-8979e9d4cbd7" />

And lab is solved !!!!
