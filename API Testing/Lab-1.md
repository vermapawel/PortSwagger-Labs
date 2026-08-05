**API Testing || Lab#1 || Exploiting an API endpoint using documentation**

<img width="782" height="541" alt="image" src="https://github.com/user-attachments/assets/a9c2a295-e575-45ef-a6da-b58c43423d67" />

Goal of this lab is to delete user carlos. 

Our credentials → wiener:peter

Lets start the lab and login

<img width="757" height="332" alt="image" src="https://github.com/user-attachments/assets/c2ef529d-9727-4ff5-a757-5e146caeee18" />

There is a functionality to update email. Lets test

<img width="750" height="342" alt="image" src="https://github.com/user-attachments/assets/6b117aaa-e734-4c9b-a979-9bba618506e3" />

Lets check this traffic in Burpsuite

<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/2d2ecb19-1ceb-4d7c-adff-029f7f46521d" />

There is an API request made to change the email. Its using PATCH method.

Lets move this traffic to Repeater

<img width="1000" height="531" alt="image" src="https://github.com/user-attachments/assets/20cd8f44-0188-49ed-a718-8d45a1fea4fe" />

We can see PATCH method is used.

<img width="916" height="545" alt="image" src="https://github.com/user-attachments/assets/2963056b-9d4a-4d48-840c-4342c4ab4719" />

Lets check if we can use GET method

<img width="1000" height="465" alt="image" src="https://github.com/user-attachments/assets/dad339c4-b771-4455-82a0-0cb5a26c2f4b" />

We are getting user details. Lets check for user carlos

<img width="1000" height="475" alt="image" src="https://github.com/user-attachments/assets/08a0337b-6a7f-4932-8a66-29214a588d41" />

We get username and email for carlos user. This is what we call as information discloser. This API is getting information of other users as well those are not logged in.

Now, lets remove username and check if we get user details

<img width="1000" height="433" alt="image" src="https://github.com/user-attachments/assets/88c0325b-cbcc-4f23-b232-11c2373b27c3" />

We got 400 Bad Request. Lets check if we can get api details

<img width="1000" height="491" alt="image" src="https://github.com/user-attachments/assets/8f7a1192-a848-48fc-9442-2cb149439512" />

We got a 302 Response. Lets follow redirection.

And we got a 200 OK. Lets Render

<img width="1000" height="469" alt="image" src="https://github.com/user-attachments/assets/8615fe0f-c272-4b8e-8de3-3cae2491a916" />

It seems these are the list of API that we can use here. 

There is a DELETE API. Its endpoint is /user (username and it should be string type)

Lets try to delete carlos user using this method

<img width="1000" height="437" alt="image" src="https://github.com/user-attachments/assets/681abf60-e28f-434c-b1f3-3eeaf1b95bda" />

We got a 200 OK. User is deleted

<img width="1000" height="443" alt="image" src="https://github.com/user-attachments/assets/00d51f90-87c8-463f-af1b-a1cbfc9019c5" />

Lab is solved !!!!
