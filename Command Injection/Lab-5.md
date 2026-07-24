**Command Injection || Lab#5 || Blind OS command injection with out-of-band data exfiltration**

<img width="847" height="657" alt="image" src="https://github.com/user-attachments/assets/91c7b0ce-bce9-4284-b2a5-f293fbd6bc77" />

To solve the lab, exploit the blind OS command injection vulnerability to execute whoami command and exfiltrate via DNS query to Burp Collaborator.

Lets start the lab

<img width="830" height="602" alt="image" src="https://github.com/user-attachments/assets/a4f942ee-2a50-47ed-b374-4f596a3bbc2a" />

As per lab description, the lab contains a blind OS command injection vulnerability in the feedback function.

<img width="671" height="572" alt="image" src="https://github.com/user-attachments/assets/b96f8579-af08-425d-b16c-a9783049b98e" />

Lets intercept the traffic with Burpsuite

<img width="1100" height="81" alt="image" src="https://github.com/user-attachments/assets/39798fbb-ded1-4e51-bbd6-afa41f7f29e8" />

Lets move this traffic to Repeater

<img width="1100" height="497" alt="image" src="https://github.com/user-attachments/assets/5aa3cb37-b8a2-485a-ab87-960ae2fe0f0f" />

Now, from the previous labs we have identified that email parameter is vulnerable to the command Injection.

Lets open Burp collaborator. Burp collaborator is an out of band server that we can control.

For Burp collaborator we need Burp Suite Professional. As I dont have Burp Suite Professional, I am putting the screen shots.

<img width="776" height="386" alt="image" src="https://github.com/user-attachments/assets/31d30c0d-f219-44a7-800e-20c518140260" />

<img width="1075" height="447" alt="image" src="https://github.com/user-attachments/assets/35a8c8d6-7180-4e36-b6d8-0a757fdd732d" />

This will be the external server. We will perform DNS lookup on this server to confirm this is vulnerable to Blind OS command injection.

Lets create the payload

<img width="557" height="30" alt="image" src="https://github.com/user-attachments/assets/8c2d67c0-9fa4-42bf-a162-0bbb32c8172e" />

We will inject our payload in email parameter and URL encode it.

<img width="777" height="707" alt="image" src="https://github.com/user-attachments/assets/cc5873af-7098-4010-858b-d210e966b73d" />

We got a 200 OK response.

Now, if this parameter is vulnerable to Command Injection, we will see a ping back to our domain.

<img width="752" height="571" alt="image" src="https://github.com/user-attachments/assets/75ce0f2a-fc08-4d88-a2a6-f7d5a5d1129f" />

We can see that it perform the DNS request it means its vulnerable. The lookup was done from IP 3.251.104.183 which is application IP address.

Now, the next step is to exfiltrate data using this technique.

Lets create a payload

<img width="632" height="27" alt="image" src="https://github.com/user-attachments/assets/4700d593-69c4-45c1-a74d-cd851010c6db" />

Lets put this payload to the email parameter and forward the traffic.

<img width="772" height="592" alt="image" src="https://github.com/user-attachments/assets/393c6705-d6a0-4560-9189-8be27f5adf9f" />

We can see a 200 OK response.

<img width="757" height="491" alt="image" src="https://github.com/user-attachments/assets/0b53e573-82cf-4893-9815-aecd1eecdf99" />

We can see that DNS lookup was done and we have the output of the command whoami i.e. peter-tZXgy0

<img width="812" height="402" alt="image" src="https://github.com/user-attachments/assets/a3e4e8e2-a411-43a4-a6cd-df4fe3c60f1f" />

And lab is solved !!

<img width="802" height="245" alt="image" src="https://github.com/user-attachments/assets/f21a5384-ba26-4dfe-9c65-56047091c8b4" />
