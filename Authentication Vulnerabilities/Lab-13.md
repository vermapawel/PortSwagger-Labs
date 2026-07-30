**Authentication Vulnerabilities - Lab #13 Broken brute-force protection, multiple credentials per request**

<img width="876" height="435" alt="image" src="https://github.com/user-attachments/assets/4e76cd1f-f62e-44d0-9544-0121c541ecb8" />

We have victim's username and a list of passwords which we can use to brute force. 

Lets start the lab and try to login at carlos account with any random password

<img width="900" height="215" alt="image" src="https://github.com/user-attachments/assets/e2d6aaf3-878f-41f9-9f73-297414c1f553" />

We got an error

Lets inspect this traffic

<img width="900" height="250" alt="image" src="https://github.com/user-attachments/assets/205195e8-0aab-4365-a416-d48731078251" />

It takes JSON string that have parameters, username and password. 

Lets move this traffic to Repeater and send this traffic 3–4 times

So after 4 times, the account gets locked.

<img width="900" height="392" alt="image" src="https://github.com/user-attachments/assets/f97b9a26-f1c1-441a-8ccd-80106c9a3c84" />

We will try to find any vulnerability in Brute Force mechanism

Now, lets check is password parameter accept only one value or more than 1 value

<img width="900" height="460" alt="image" src="https://github.com/user-attachments/assets/49aa5b31-deec-4120-b9d9-33dd2f951b0a" />

We have added three passwords and got invalid username or password error. Also we got 200 OK response. It means the server accepts this request without any issue. So we can pass multiple passwords at a time.

Now we have a list of approx. 100 passwords. Lets put all those password here and forward the traffic.

If the application accepts an array of passwords, then we will get 302 response for redirection for the valid password.

<img width="900" height="422" alt="image" src="https://github.com/user-attachments/assets/738a2612-73ce-451e-8a38-764229a7e337" />

So we got 302 status code which is redirected to /my-account page, but we dont know which one is the correct password. 

We can see one session Id is created for the correct password. 

Lets copy that session ID 0xcjYAnN0zgefxNnHTgqkr1zMWjxs5JB

Go to the login page, right click and go to Inspect

<img width="900" height="394" alt="image" src="https://github.com/user-attachments/assets/707dade6-e4e5-428f-8ab9-e1c909701f3b" />

Replace the cookie from that one that we have got.

And refresh the page, we have logged-in as Carlos

<img width="900" height="457" alt="image" src="https://github.com/user-attachments/assets/ad5ab1b9-f27f-47a5-a259-5251a08bc5a1" />




