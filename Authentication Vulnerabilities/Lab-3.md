**Authentication Vulnerabilities || Lab #3 || Password reset broken logic**

<img width="844" height="508" alt="image" src="https://github.com/user-attachments/assets/78425cd0-1972-41bf-b86d-b9cd3cc217f8" />

In this Lab we have our credentials and victim’s username.

Goal of this Lab is to reset victim’s password and login in his account.

<img width="1012" height="459" alt="image" src="https://github.com/user-attachments/assets/13c740c2-e625-42de-9050-df4e8d9d5d9c" />

Lets check the reset functionality of the application.

We will put our username

<img width="958" height="351" alt="image" src="https://github.com/user-attachments/assets/87a0cf4f-763c-43c5-93d3-d01e42d6e365" />

Its sending post request to the application.

<img width="1100" height="423" alt="image" src="https://github.com/user-attachments/assets/e3ef13d1-9445-40c4-9ad6-772e256d8e4d" />

Lets check the email client

<img width="943" height="280" alt="image" src="https://github.com/user-attachments/assets/165ce3f0-0953-48b7-b567-b3e733ad5cf0" />

<img width="1100" height="498" alt="image" src="https://github.com/user-attachments/assets/87fa98d3-b58c-4cec-a58d-5ef97619e1f3" />

The application sends a forget password link to reset the password.

<img width="1100" height="293" alt="image" src="https://github.com/user-attachments/assets/bf901b88-6488-4263-b800-3e57bb2aad29" />

Forget password mechanism has forgot password token.

Lets change the password and check how application works

<img width="1027" height="456" alt="image" src="https://github.com/user-attachments/assets/aac04cff-435a-4119-b644-3d1d60b3590b" />

<img width="1100" height="236" alt="image" src="https://github.com/user-attachments/assets/3aef28f2-e10e-4adb-8be3-405492e95b0b" />

Lets move this traffic to repeater

<img width="1100" height="656" alt="image" src="https://github.com/user-attachments/assets/3b7d1abf-a9e3-4fda-b93e-310cd07dfcbf" />

When we change the password, it has temp-forgot-password-token, username and new password.

So the application takes forget password token twice, one in the URL and one in the body of the code. For changing the password, these two tokens are getting compared and if they are not same, it will not reset the password.

So if we change this token to anything and change the username to carlos and see if it works.

<img width="1100" height="607" alt="image" src="https://github.com/user-attachments/assets/d89961a8-2fbf-4e29-bd18-354d80505680" />

We got a 302 response.

Lets try to login now.

<img width="990" height="471" alt="image" src="https://github.com/user-attachments/assets/1ad01f66-d0f7-4031-bc09-73f29496e865" />

And we are logged in, Lab is solved !!!

So vulnerability of the application is that it compares the forgot password token. And if they are same, it will allow to change password of any username.

