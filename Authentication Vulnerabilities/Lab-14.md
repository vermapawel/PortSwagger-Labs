**Authentication Vulnerabilities - Lab #14 2FA bypass using a brute-force attack**

<img width="862" height="492" alt="image" src="https://github.com/user-attachments/assets/745c2988-f5e6-4e2d-b934-cfb1aa76faa1" />

We have victim's credentials carlos:montoya

Lets open the lab and login to victim's account

<img width="807" height="382" alt="image" src="https://github.com/user-attachments/assets/9741a593-14a5-425d-a200-55e70d9bbab4" />

Its asking for a verification code

<img width="772" height="186" alt="image" src="https://github.com/user-attachments/assets/397d105d-93f3-4ff9-958d-8e4c36ada573" />

Lets put random security code and check how application behaves. 

So after two wrong security code, application present login screen.

<img width="900" height="196" alt="image" src="https://github.com/user-attachments/assets/8f004ad2-43aa-44ed-b887-6eea0ef2a4fc" />

I have tried multiple times and there is no locked out feature. After every two wrong code, there is login page.

Lets intercept this traffic in Burp suite

<img width="900" height="360" alt="image" src="https://github.com/user-attachments/assets/250d0cc7-b298-4731-8865-da79708d2547" />

We can see there are two request. 1st traffic, **login** has GET request is where we have put the credentials. We got a 302 response for redirection. The other traffic, **login2** which is responsible for generation of 2-FA code. 

Lets put a random code and see check that traffic

<img width="900" height="387" alt="image" src="https://github.com/user-attachments/assets/ce8cae5c-4e6d-48c3-82c4-c30f06ff70b8" />

Now, we will automate the attack

<img width="827" height="467" alt="image" src="https://github.com/user-attachments/assets/3670057f-3921-45f5-a7d7-72835199ff07" />

<img width="772" height="562" alt="image" src="https://github.com/user-attachments/assets/9e604824-8faf-47ea-be0f-af1a94c3b299" />

<img width="692" height="622" alt="image" src="https://github.com/user-attachments/assets/199fd06b-c5c4-4ee7-bb31-c1589dd8a07b" />

<img width="900" height="312" alt="image" src="https://github.com/user-attachments/assets/86348f74-8736-4f82-81e7-d62ef0305699" />

We have selected all three traffic. 1st is GET login page where we will put credentials, 2nd

<img width="900" height="316" alt="image" src="https://github.com/user-attachments/assets/7e1c9505-a6d9-4196-b9e3-2da02d6c7736" />

Macro is selected. 

Now, lets move login2 where we have mfa-code to the Intruder. 

We will bruteforce the mfa code.

<img width="900" height="382" alt="image" src="https://github.com/user-attachments/assets/5a539f6c-4831-4d9a-b4f7-27e09cd51f7f" />

<img width="900" height="291" alt="image" src="https://github.com/user-attachments/assets/0e5e4171-efba-4a28-b361-649e16c8a7f0" />

<img width="900" height="281" alt="image" src="https://github.com/user-attachments/assets/c6e9dc30-0f23-4c57-a759-476209eddf72" />

<img width="900" height="388" alt="image" src="https://github.com/user-attachments/assets/74e79a9c-4809-42f7-8d4e-0078c176c3d6" />







