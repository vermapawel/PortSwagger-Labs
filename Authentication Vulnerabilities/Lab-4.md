**Authentication Vulnerabilities — Lab #4 Username enumeration via subtly different responses**

<img width="850" height="580" alt="image" src="https://github.com/user-attachments/assets/cc4c05d6-c2ce-4e3f-bdb1-71ef20d7d13a" />

List of username and password are provided.

Goal of this Lab is to enumerate the username and then brute force its password.

Lets start the lab

<img width="883" height="409" alt="image" src="https://github.com/user-attachments/assets/68aa059c-2c40-4b34-90c2-1c862a024dd6" />

We will put a random username and password and inspect the traffic

<img width="1100" height="629" alt="image" src="https://github.com/user-attachments/assets/cdff0f93-530c-4cdf-93c1-ba8be422d8b7" />

Lets move this traffic to intruder

There is list of username provided in the descriptiuon of the Lab.

<img width="817" height="378" alt="image" src="https://github.com/user-attachments/assets/a9a47370-50ab-4122-96ac-b7cd40183a4d" />

We will use these usernames in the payload.

<img width="1100" height="449" alt="image" src="https://github.com/user-attachments/assets/60429bb4-da78-4326-ab50-5c4d958c92a9" />

Lets start the attack

<img width="1100" height="306" alt="image" src="https://github.com/user-attachments/assets/1a0d2be1-dd33-44c6-9fda-661e6e5aa13d" />

Now, in the result, all status code is 200, there is no difference. Also in the length there are lots of difference.

Lets compare the responses of two payloads

Right click > Send to comparer (response)

<img width="1100" height="473" alt="image" src="https://github.com/user-attachments/assets/04407fec-751d-487e-91e5-8c0006d5982b" />

<img width="1100" height="424" alt="image" src="https://github.com/user-attachments/assets/aa948f29-c9d7-4aa3-9b36-a2835ae62c5a" />

Its just the analytics scripts are different for each word it seems. There fore there is a difference in the length.

So we cannot determine if any of the username is valid.

Lets inspect the traffic again.

We will put an obvious incorrect username and check what error message we got.

<img width="1100" height="628" alt="image" src="https://github.com/user-attachments/assets/2093907e-6887-4415-b1d1-64ef9957c069" />

Lets copy this error message “Invalid username or password.” and search in the sniper attack payload.

For searching we should have Professional version of Burp. Else we need to check each response one by one.

Since I don't have Professional version, I am putting screen shots.

<img width="769" height="396" alt="image" src="https://github.com/user-attachments/assets/f7df4b0e-9c02-4525-ac1d-610f5c410bba" />

We are performing negative search. It means the response which don't have “Invalid username or password.” will be shown.

<img width="781" height="537" alt="image" src="https://github.com/user-attachments/assets/cc2a6d7e-f2a0-468e-b160-e58be08cb362" />

Now, pay a close attention to the error message we got. In the error message there is no .

So the difference here is that when the username is invalid, the error contains . and when username is valid, the error don't contain .

Lets check each response one by one

<img width="1100" height="467" alt="image" src="https://github.com/user-attachments/assets/19abe1eb-af3e-4a86-ac91-5c3af03d2a72" />

So for username alpha, the error don't have .

It means its the valid username.

<img width="1100" height="466" alt="image" src="https://github.com/user-attachments/assets/be6dc9cc-a339-4aca-b74c-ae4545880dab" />

Now, lets brute force for the password.

We have a list of passwords in the Lab description. We will use those passwords as payload.

<img width="1100" height="416" alt="image" src="https://github.com/user-attachments/assets/9d14beab-f1cd-4e82-9fe8-c18ce25afac0" />

We are looking for a 302 response.

<img width="1100" height="495" alt="image" src="https://github.com/user-attachments/assets/455fb06a-697a-4eff-bc0d-abc0a927a721" />

We got the password **joshua**

Lets try to login.

<img width="1100" height="377" alt="image" src="https://github.com/user-attachments/assets/ee8f1f70-a9ed-4938-b491-765c0f95a1cf" />

And lab is solved !!!!




