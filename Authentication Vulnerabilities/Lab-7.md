**Authentication Vulnerabilities — Lab #7 Username enumeration via account lock**

<img width="892" height="390" alt="image" src="https://github.com/user-attachments/assets/02c407a9-9bf3-4079-8d45-56bf18334eb7" />

Lets start the Lab

<img width="667" height="302" alt="image" src="https://github.com/user-attachments/assets/44d60b76-57f7-4802-884e-b8e6b7da598a" />

We have put a random username and password which is incorrect.

Lets intercept this traffic in Burpsuite

<img width="1100" height="631" alt="image" src="https://github.com/user-attachments/assets/5577af5c-e5c8-4c3b-ae79-987cc1c3a650" />

We have forwarded this traffic 5–6 times, account is not getting locked.

So it may be possible that when we are using different incorrect username, account is not getting locked.

We need to check what happened if we use a correct username with incorrect passwords multiple times.

Lets move this traffic to Intruder

<img width="1100" height="545" alt="image" src="https://github.com/user-attachments/assets/d4d286f4-8d00-4481-8ace-5d970dfa3cf2" />

We are using cluster bomb attack as we need to bruteforce username and password. For username we will use the list of usernames that is provided.

For password we will use null value. Payload count will be 5.

So it means, every usename will try to login without any password for 5 times. We are checking how application responds if there are multiple login attempts from a valid username.

<img width="1100" height="586" alt="image" src="https://github.com/user-attachments/assets/79ce51ed-85da-49a8-9fe5-3e5e2d24915f" />

<img width="1100" height="595" alt="image" src="https://github.com/user-attachments/assets/5d52a4df-97bf-4e04-9180-a255d0550a9d" />

For username argentina there is a different length. Lets use this usename multiple time and check if we are locked out or not.

<img width="1100" height="534" alt="image" src="https://github.com/user-attachments/assets/ff515a9a-51a4-4120-b3a8-4c525b7427ec" />

After multiple attempts we are locked out. Now we know that argentina is a valid username. Lets bruteforce the password.

<img width="1100" height="546" alt="image" src="https://github.com/user-attachments/assets/9283fc8f-155e-446d-9ca9-4eb55daf18c4" />

<img width="1100" height="395" alt="image" src="https://github.com/user-attachments/assets/d2a2d250-2cff-4eba-a4a4-9b3f38011c36" />

We can see that response has different length. Lets try password moon.

<img width="835" height="446" alt="image" src="https://github.com/user-attachments/assets/124fb0be-c319-4b68-8451-2c00ab4ac6a1" />
