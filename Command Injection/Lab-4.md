**Command Injection || Lab#4 || Blind OS command injection with out-of-band interaction**

<img width="777" height="612" alt="image" src="https://github.com/user-attachments/assets/503886c3-4e9c-4df4-8f69-0bae3cc20f38" />

To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator.

Lets start the lab

<img width="882" height="661" alt="image" src="https://github.com/user-attachments/assets/263c33e5-c687-4a89-9b95-4cb9432bf257" />

As per lab description, the lab contains a blind OS command injection vulnerability in the feedback function.

<img width="911" height="627" alt="image" src="https://github.com/user-attachments/assets/1591e6f9-87f4-46f4-afc0-d56c76b8f288" />

Lets intercept the traffic with Burpsuite

<img width="1100" height="299" alt="image" src="https://github.com/user-attachments/assets/fdac6e3f-e265-43bb-b7cc-0e2748512ac7" />

Lets move this traffic to Repeater

<img width="1100" height="427" alt="image" src="https://github.com/user-attachments/assets/3081ac55-1d42-4874-8802-cbe1a9af4b69" />

Now, from the previous labs we have identified that email parameter is vulnerable to the command Injection.

Lets open Burp collaborator. Burp collaborator is an out of band server that we can control.

For Burp collaborator we need Burp Suite Professional. As I dont have Burp Suite Professional, I am putting the screen shots.

<img width="776" height="386" alt="image" src="https://github.com/user-attachments/assets/543a5773-5332-46b6-885b-83eda216bc82" />

<img width="1075" height="447" alt="image" src="https://github.com/user-attachments/assets/a2d84415-f693-4773-871a-387086d240f4" />

<img width="452" height="25" alt="image" src="https://github.com/user-attachments/assets/33a75d43-6c8b-4f42-b838-a7b48009b5c7" />

This will be the external server. We will perform DNS lookup on this server to confirm this is vulnerable to Blind OS command injection.

Lets create the payload

<img width="562" height="27" alt="image" src="https://github.com/user-attachments/assets/ef1cc03e-eed6-4af9-9fa0-19447821aa4a" />

We will inject our payload in email parameter and URL encode it.

<img width="787" height="615" alt="image" src="https://github.com/user-attachments/assets/ff526891-0081-47b6-b053-d04142f860fd" />

We got a 200 OK response.

Now, if this parameter is vulnerable to Command Injection, we will see a ping back to our domain.

<img width="755" height="652" alt="image" src="https://github.com/user-attachments/assets/fe7d761f-e57a-425e-8e8c-4adc20478211" />

We can see that it perform the DNS request it means its vulnerable. The lookup was done from IP 3.251.104.183 which is application IP address.

And the lab is solved !!

<img width="717" height="276" alt="image" src="https://github.com/user-attachments/assets/7aa0f9de-b6a4-4ca3-be67-20a458485a63" />

