**HTTP Host header attacks || Lab#4 || Routing-based SSRF**

<img width="777" height="522" alt="image" src="https://github.com/user-attachments/assets/0b311e59-cd6e-4cc8-a0c8-2d61b24a7040" />

Goal of this lab is to access the internal admin panel located in the 192.168.0.0/24 range, then delete the user carlos.

Lets start the Lab

<img width="817" height="457" alt="image" src="https://github.com/user-attachments/assets/340bc6fd-88fc-46b8-ab73-333513970934" />

Click on Home and intercept the traffic in Burpsuite.

<img width="1000" height="409" alt="image" src="https://github.com/user-attachments/assets/50e7d348-392b-4f00-a71c-e6847eb84a23" />

Lets move this traffic to Repeater

<img width="735" height="627" alt="image" src="https://github.com/user-attachments/assets/b8bc78cb-a4f9-4690-8b3a-056a9e92be75" />

Now, we can perform SSRF attack vector if there is Host Based injection vulnerability. This specific attack vector (SSRF) occurs when the traffic between the client and backend server is routed through an intermediary system such as Load Balancer or reverse proxy. 

We have a application client. It is hosted on an application sever in the internal network. Internal network is protected by a Firewall. In that internal network, there could be multiple servers.

<img width="907" height="155" alt="image" src="https://github.com/user-attachments/assets/f11fb374-6ff4-4686-8fab-dff78f737ec9" />

If an attacker is trying to access server 1 or server 2, he will not be able to as there are Firewall rules who blocks the attacks. 

In SSRF attack, we exploit one internal server, lets say server 1 through the application server. Now, both application server and other servers are in same network, there is a trust relationship between them they can access each other. 

First we need to confirm if this application is vulnerable to Host injection and SSRF. 

Lets open Burp collaborator. As my burp collaborator is not working, I am putting screen shots

<img width="825" height="576" alt="image" src="https://github.com/user-attachments/assets/f42a10d8-33fd-4d56-bd61-9918f25bc4cb" />

<img width="352" height="32" alt="image" src="https://github.com/user-attachments/assets/c92e50f0-89be-47b9-bce0-fdd376f60626" />

This is our external server. Lets put this server in Host header. If Host header accepts any arbitrary value, we should get a ping response in the Burp collaborator.

<img width="1000" height="626" alt="image" src="https://github.com/user-attachments/assets/d95e0b75-0e2c-430a-947f-ad4df1253441" />

Go to collaborator and Poll now, we can see HTTP and DNS request

<img width="982" height="671" alt="image" src="https://github.com/user-attachments/assets/e5444fea-fab3-43a5-9d38-ef19d7e9f69b" />

So it confirms that this application is vulnerable to Host injection and SSRF.

Now, there may be another server available in the network. We will perform an IP scan to determine where the HTTP server is hosted.

Lets move this traffic to Intruder

We have an IP range provided in the lab description 192.168.0.0/24.

<img width="1000" height="364" alt="image" src="https://github.com/user-attachments/assets/812be45a-d8cd-4647-b7fe-4d5ffd1dc156" />

We will check each IP address one by one. Start attack

<img width="1000" height="524" alt="image" src="https://github.com/user-attachments/assets/060dc71e-7a06-4ca2-ad67-563ace1541f0" />

For IP 192.168.0.249 there is 302 Response code. Location is /admin.

We will put this IP address in the Host and forward the traffic.

<img width="1000" height="489" alt="image" src="https://github.com/user-attachments/assets/e96d62f6-5d30-4c78-80c4-ab5986916e36" />

We got a 302 redirection, follow redirection

<img width="1000" height="432" alt="image" src="https://github.com/user-attachments/assets/d7a00577-68ba-4d10-b116-29ea666ca00b" />

We are at the admin page. Lets check this request in browser.

<img width="997" height="470" alt="image" src="https://github.com/user-attachments/assets/1cd703c5-3c39-4f2d-803b-45c964844f13" />

Lets delete user carlos. But this will not work. Because we are doing id externally.

<img width="902" height="192" alt="image" src="https://github.com/user-attachments/assets/3ab7ba67-ee9c-4c2b-a9a3-3c0e4e4ccb42" />

Lets check this traffic in Burpsuite

<img width="1000" height="499" alt="image" src="https://github.com/user-attachments/assets/1b018a28-a72d-472d-8e60-df192028098c" />

Move this traffic to Repeater

<img width="1000" height="431" alt="image" src="https://github.com/user-attachments/assets/32edab83-146e-4b43-a23f-4d2c55f51c47" />

Put the IP address in Host and forward the traffic. This will delete the user carlos

<img width="1000" height="266" alt="image" src="https://github.com/user-attachments/assets/b8ba19b1-287b-44e9-bdae-a827d0a650ac" />

And lab is solved !!!
