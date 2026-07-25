**Authentication Vulnerabilities — Lab #6 Broken brute-force protection, IP block**

<img width="1100" height="589" alt="image" src="https://github.com/user-attachments/assets/879c18bc-d7e5-4779-a9e5-8754351b7e6e" />

We have our credentials and Victim’s username i.e carlos

Goal of this lab is to login into victim’s account page. We have a list of passwords provided that we can use for brute forcing.

Lets start the Lab

<img width="1100" height="524" alt="image" src="https://github.com/user-attachments/assets/8cd642ce-4935-4de1-a347-2e470cf7ccc9" />

We have put the username and a random password. Lets intercept this traffic

<img width="1100" height="530" alt="image" src="https://github.com/user-attachments/assets/0d4bb7f6-a1c5-4d56-b2f1-4a1319c1baa8" />

Lets move this traffic to Repeater

<img width="1100" height="553" alt="image" src="https://github.com/user-attachments/assets/d4ef3324-8ec5-4ec9-9207-1c7115b4fe74" />

We get error message ‘Incorrect Password’.

When we try for 2–3 time

<img width="1100" height="577" alt="image" src="https://github.com/user-attachments/assets/fe7b34b9-e96a-41b1-ac1e-49eb13ca9a12" />

And we are locked for 1 min. So after 3 wrong attempts, we are locked for 1 mins.

Now, let check what happen if we alternate with incorrect and correct credentials.

So one time we will login with carlos:test (incorrect) then next time we will login with wiener:peter (correct)

Incorrect login

<img width="1100" height="566" alt="image" src="https://github.com/user-attachments/assets/146769e0-cd79-410f-800b-0a6d46fc98ce" />

Correct login

<img width="1100" height="519" alt="image" src="https://github.com/user-attachments/assets/36247aa0-a4f1-41a3-99d8-2a9dd842d33b" />

I have tried it multiple times, incorrect login and correct login, and account is not getting locked.

So this is how we can bypass the brute force security feature to lock the account.

Now we have a list of passwords for carlos.

So we will login once with username carlos and one password from the list, then we will login with username wiener : peter, and account will not locked.

We can do this with the help of Intruder.

<img width="1100" height="524" alt="image" src="https://github.com/user-attachments/assets/72d4a67e-b3b1-4cab-b81b-0172245de82a" />

For this attack, we need one request at a time. We will create a new resource pool with 1 concurrent request.

<img width="1100" height="475" alt="image" src="https://github.com/user-attachments/assets/d6f7bf20-42d6-4eaf-9a6c-001934b0df90" />

Now, we need to alternate wiener:peter request with carlos request.

We will create a macro to automate this

We will go to settings > Sessions > Add

<img width="992" height="492" alt="image" src="https://github.com/user-attachments/assets/592e89c2-a538-4c7d-9476-6bd5829e169d" />

<img width="696" height="457" alt="image" src="https://github.com/user-attachments/assets/2de6a906-45ae-4d33-9280-cb1e0102716a" />

<img width="616" height="632" alt="image" src="https://github.com/user-attachments/assets/cbc41143-f557-4e33-97b9-a16cc578973e" />

We will add a macro

<img width="1021" height="512" alt="image" src="https://github.com/user-attachments/assets/c605d148-ca90-451f-877a-adaa40c5e42c" />

<img width="1100" height="622" alt="image" src="https://github.com/user-attachments/assets/59fce1e0-2a2d-4123-9f16-894b1a09eee0" />

So our macro is set.

<img width="1100" height="416" alt="image" src="https://github.com/user-attachments/assets/a983381a-ba62-4684-b089-eea0cd196813" />

Lets start the attack from Intruder

We will look for 302 response.

<img width="1100" height="247" alt="image" src="https://github.com/user-attachments/assets/e67ff43f-7033-4461-ae1f-a71f73928cb1" />

Lets login with this password.

<img width="767" height="402" alt="image" src="https://github.com/user-attachments/assets/dcf23a52-a803-4ba1-a391-ddac5654d9e5" />

And our lab is solved
