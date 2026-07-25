**Authentication Vulnerabilities || Lab #1 || Username enumeration via different responses**

<img width="868" height="561" alt="image" src="https://github.com/user-attachments/assets/ad5e16f9-65f2-47de-b928-b5a7fe5c5dab" />

Goal of this lab is to enumerate a valid username, brute-force this user’s password, then access their account page.

Lets start the Lab

Try to login as Test || test

<img width="1100" height="518" alt="image" src="https://github.com/user-attachments/assets/c57b30a7-5800-45dc-9c95-1c272f2c4107" />

We get error Invalid username

Lets check this traffic in Burp suite

<img width="1100" height="547" alt="image" src="https://github.com/user-attachments/assets/bca3a4e7-7919-423b-b821-2d787f15fe0e" />

Now we will enumerate the username and then the password. Lets move this traffic to Intruder

**Step 1 → Enumerating username**

We have a list of usernames provided in the Lab description.

<img width="891" height="535" alt="image" src="https://github.com/user-attachments/assets/ebe72130-b946-45cc-926c-6b260de977fa" />

<img width="1100" height="421" alt="image" src="https://github.com/user-attachments/assets/8596a64d-5c1b-4093-8547-d45c594df695" />

We will use attack type as Sniper attack. Attack pointer will be test of the username.

Payload type will be Simple list. Let's paste all usernames in the payload and start the attack.

<img width="1100" height="282" alt="image" src="https://github.com/user-attachments/assets/325aba13-1491-4386-a11e-e6fc435f084b" />

Here we are looking for a change in Length.

Now, for username albuquerque there is a change in length. Also for this username, we are getting Incorrect password. It means this is a valid username.

<img width="1100" height="541" alt="image" src="https://github.com/user-attachments/assets/9811c325-5169-4dd9-b70e-1a295bce4cef" />

**Step 2→ Enumerating password**

There is a list of passwords in the Lab description as well.

<img width="853" height="409" alt="image" src="https://github.com/user-attachments/assets/ac08f358-3be7-464c-8335-f30047ee1d2f" />

<img width="1100" height="425" alt="image" src="https://github.com/user-attachments/assets/af833e27-0514-47fa-bd97-6d7ed6f3d826" />

We will use attack type as Sniper attack. Attack pointer will be test of the password. Username will be **albuquerque**

Payload type will be Simple list. Let’s paste all passwords in the payload and start the attack.

<img width="1100" height="274" alt="image" src="https://github.com/user-attachments/assets/d6e10829-3211-46a6-ade8-e406efc7deae" />

This time we will pay attention on Status code. If the login is successful, the status code will be 302.

<img width="1100" height="404" alt="image" src="https://github.com/user-attachments/assets/069dd2e9-ef3e-46ba-a19d-0bdbaa27a50a" />

So, for payload **2000**, the status code is 302. In the Responce we can see that it redirects to /my-account.

Lets try to login **albuquerque || 2000**

<img width="1100" height="443" alt="image" src="https://github.com/user-attachments/assets/955ef121-036e-47b4-9bd0-493f0efac3af" />

We are logged in and Lab is solved !!!
