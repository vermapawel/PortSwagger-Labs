**HTTP Host header attacks || Lab#5 || SSRF via flawed request parsing**

<img width="780" height="525" alt="image" src="https://github.com/user-attachments/assets/b47f41cb-35eb-4659-bfce-379dfadecd79" />

Goal of this lab is to access the internal admin panel located in the 192.168.0.0/24 range, then delete the user carlos.

Lets start the Lab and go to Home page.

<img width="995" height="392" alt="image" src="https://github.com/user-attachments/assets/044eae65-c095-4774-9386-a36b990f24d5" />

Lets check this traffic in Burp suite

<img width="1000" height="462" alt="image" src="https://github.com/user-attachments/assets/51129d22-861f-4bf5-975b-e3ed2ca7d5f9" />

Move this traffic to Repeater.

Now lets check if the application is only parsing a position of header instead of all the header.

<img width="1000" height="462" alt="image" src="https://github.com/user-attachments/assets/7443c0d4-b9da-4a93-99b7-b84400eef36c" />

We got Forbidden error.

Lets check again

<img width="1000" height="412" alt="image" src="https://github.com/user-attachments/assets/bc66b23b-1b6f-42e0-ba4c-7a7fbcedaf6a" />

We again got Forbidden error. 

So the application is properly parsing this Host header and checking that not an arbitrary value is passed. 

Now, Sometimes the servers are configured to understand the absolute URL.

Lets supply the absolute URL and check

<img width="1000" height="226" alt="image" src="https://github.com/user-attachments/assets/d6c7a3f5-eb8f-4609-8928-518639339d06" />

Lets copy the URL

<img width="1000" height="467" alt="image" src="https://github.com/user-attachments/assets/920aa292-0bae-4c78-b825-cf0f2a7e03da" />

We got a 200 OK response. 

Now supplying absolute URL in the request line and Host header can lead to discrepancies between different systems and if not managed correctly can lead to vulnerability. 

So the application is checking the absolute URL, and if it is valid, it ignores the Host header. 

Lets go to the collaborator

<img width="1000" height="733" alt="image" src="https://github.com/user-attachments/assets/71176d48-178a-4797-8ebb-8636b33b849b" />

And put the server link in the Host header

<img width="1000" height="626" alt="image" src="https://github.com/user-attachments/assets/4a4a8bfa-0d56-405d-872d-3524b8a93e25" />

We got a 200 OK response. So it confirms that the application is vulnerable to Host header injection and SSRF vulnerability.

Lets go to collaborator

<img width="832" height="652" alt="image" src="https://github.com/user-attachments/assets/6bd42c5a-9516-432d-901f-7fcce5163556" />

And we can see response from the application.

Now, there may be another server available in the network. We will perform an IP scan to determine where the HTTP server is hosted.

Lets move this traffic to Intruder

We have an IP range provided in the lab description 192.168.0.0/24.

Lets move this traffic to Intruder

<img width="1000" height="425" alt="image" src="https://github.com/user-attachments/assets/aa67ef05-c040-4d54-b7f8-96eb3d3eecbd" />

We will check each IP address one by one. Start attack

<img width="1000" height="557" alt="image" src="https://github.com/user-attachments/assets/e1e6f336-f77f-49aa-86aa-f1ec41b6c21d" />

For IP 192.168.0.47 we got 302 response. Location is /admin.

We will put this IP address in the Host and forward the traffic.

<img width="1000" height="466" alt="image" src="https://github.com/user-attachments/assets/7e661a9f-efed-4182-a155-b540cfc4e933" />

We got a 302 redirection. Its directing to /admin

Now in Host header 192.168.0.47 we cannot add /admin. 

We will add /admin in the absolute path.

<img width="1000" height="475" alt="image" src="https://github.com/user-attachments/assets/d8f48a38-0e86-43ec-92da-a265663535ea" />

Let got a 200 OK response. Lets check this response in browser.

<img width="1000" height="433" alt="image" src="https://github.com/user-attachments/assets/7a0334b2-a8d7-43e0-9c65-483998810ff1" />

Lets delete user carlos. But this will not work. Because we are doing id externally.

<img width="986" height="157" alt="image" src="https://github.com/user-attachments/assets/2ec7a1d2-3d06-49e3-bdda-42720c3edb71" />

Lets check this traffic in Burpsuite

<img width="1000" height="441" alt="image" src="https://github.com/user-attachments/assets/2c0ae2b9-7cb3-4f04-b2d6-7b35c4cb1a83" />

Move this traffic to Repeater

Put the IP address in Host and forward the traffic. This will delete the user carlos

<img width="1000" height="399" alt="image" src="https://github.com/user-attachments/assets/897ed0ee-14ac-4bf8-a3cc-a50dc3b37abb" />

We got an error. We need to put absolute path

<img width="1000" height="364" alt="image" src="https://github.com/user-attachments/assets/280ec9dc-8cf9-403b-8180-34545fb4ae17" />

We got a 302 Response code. User carlos got deleted

<img width="977" height="275" alt="image" src="https://github.com/user-attachments/assets/afc7f0e8-7803-4915-a940-26f0564632a2" />

And lab is solved !!!



