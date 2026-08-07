**HTTP Host header attacks || Lab#3 || Web cache poisoning via ambiguous requests**

<img width="786" height="462" alt="image" src="https://github.com/user-attachments/assets/2f954f9e-2386-4927-9faf-362c347953d4" />

Goal of this lab is to poison the cache so the home page executes alert(document.cookie) in the victim's browser.

Web Cache poisoning is a technique where an attacker exploits the behavior of the application and its corresponding cache so that a harmful HTTP response is served to other user of the application.


<img width="872" height="296" alt="image" src="https://github.com/user-attachments/assets/7f44f937-80a0-43d7-ae82-bb1ed38bfa56" />

Lets understand how Cache work.

We have a user 1 who is requesting  a home page from a Web server for the 1st time. This request is not cached. This request will reach to the Web server. The backend server will extract the code for the homepage and sends it back to the user 1 browser.

Now, when user 2 request the same home page, because the same homepage was already requested by user 1, the request will not go all the way to the Web server, it will go to the Web Server cache and cache will send it to the user 2 browser.

This is how web cashing works. The servers uses this functionality to reduce the traffic load. If the server has to send a new response to every HTTP request, it will likely overload the server and cause latency issue. 

Now, if there are some implementation flaws in cache design, an attacker can exploit this vulnerability to deliver a malicious payload to other users of the application using web cache.

**Three steps to construct a Web Cache poisoning attack**

1. Identify and evaluate unkeyed inputs :- Unkeyed inputs are the inputs that web cache ignore when deciding whether to serve a cached response to the user.
   
2. Elicit a harmful response from the backend server.
   
3. Get the response cached.

Lets start the lab

<img width="841" height="472" alt="image" src="https://github.com/user-attachments/assets/5a352a44-f103-4dcb-bb79-260ed1b0329d" />

Lets click on Home. Check this traffic in Burp suite

<img width="1000" height="446" alt="image" src="https://github.com/user-attachments/assets/ddce6d1e-c3b4-4132-9900-be45cfe6a3c8" />

Lets move this traffic to Repeater

<img width="1000" height="408" alt="image" src="https://github.com/user-attachments/assets/6ee1a3cc-6b37-4b9b-acc0-ab3fda747e9d" />

We can see Caching header in the Response, it means application is caching response.

**Step 1:-** We need to identify the unkeyed inputs. In this lab we already know that Host header is the unkeyed input. 

Lets change the Host header to an another value

<img width="1000" height="455" alt="image" src="https://github.com/user-attachments/assets/2fae0a5c-5047-43fa-99a1-fc8c9ba40c5e" />

We got a Gateway Timeout error. It seems application is accepting a specific format of Host header. 

Lets add one more Host header. There may be a flaw in the application regarding validation of Host header. Sometime they only validate 1st host header and don't validate the other.

<img width="1000" height="539" alt="image" src="https://github.com/user-attachments/assets/cca0c573-c1a9-45e7-b518-a7124d39da59" />

We got a 200 OK response. It means application is accepting 2 host headers. 

Also the 2nd host header (google.com) is actually displayed in the response.

Please note that in response **X-Cache : miss**

It means that its not cached and the response is coming from the server. 

Lets send the request 3–4 times.

<img width="1000" height="541" alt="image" src="https://github.com/user-attachments/assets/81857101-cd8d-4faa-b778-69fff20e3508" />

Now, the X-Cache : hit. It means the response is coming from cache and not from the server. 

Now, when we are testing on a live website, we should use cache buster in the request. If we do attempt an exploit and if its successful, all the user that request the home page (GET /) will be exploited.

Cb=12324. It could be any random parameter. 

Now, if we perform any exploit, the exploit will only run on this specific URL (GET /?cb=12345). So no users will get affected by this exploit.

Once we confirm that our exploits works, we will remove cache buster and will send out exploit to the main page because we do want the victim who is accessing the main page get exploit.

Lets test again

<img width="1000" height="506" alt="image" src="https://github.com/user-attachments/assets/8f7aa0ef-dfbc-4732-b2a2-9ce53f862236" />

X-Cache : miss because we are using a different URL

Lets copy the location where the Host Header payload is getting injected.

```
<script type="text/javascript" src="//google.com/resources/js/tracking.js"></script>
```

Now, we will inject our own malicious sever host. We will create this specific file resources/js/tracking.js and will add malicious java script code in this tracking.js file

Lets go to exploit server.

<img width="907" height="270" alt="image" src="https://github.com/user-attachments/assets/d45240af-e537-45ee-a6de-190d32dfb8c9" />

In the File, he have given the same location /resources/js/tracking.js.

In the Body we will include the malicious javascript code.

To complete the lab we need to alert the users cookie.

<img width="1000" height="737" alt="image" src="https://github.com/user-attachments/assets/3bf896a9-1863-4869-a9cd-5282d9a64753" />

Store the exploit. Lets view the exploit

<img width="1000" height="180" alt="image" src="https://github.com/user-attachments/assets/f582536f-c770-4bcd-9b8d-3fdb8e3335ba" />

We can see after our web server, in location /resources/js/tracking.js there is a javascript file to display the cookie of the user.

Now, we have to inject our Host in response and forward the traffic 4–5 times. We are looking for X-Cache : miss

<img width="1000" height="426" alt="image" src="https://github.com/user-attachments/assets/996ac47a-b2f3-4945-bb5f-683f1b68797e" />

Now, if we go to the URL /?cb=12345 we should get an alert.

<img width="1000" height="272" alt="image" src="https://github.com/user-attachments/assets/ce1ac4ad-e520-40de-a8cd-a4d73302c417" />

We got an alert with an empty cookie. However our payload worked. 

Now we know that the payload works, we need to send the home page to the victim user. 

Lets remove the Cache Buster and forward the traffic.

<img width="1000" height="424" alt="image" src="https://github.com/user-attachments/assets/37c0ee17-917b-4459-b901-6925338ce58e" />

Lets forward the traffic 3–4 time and we will get X-Cache : hit

<img width="1000" height="311" alt="image" src="https://github.com/user-attachments/assets/f344e6bc-f6e4-4baa-866f-d003874ed96f" />

And Lab is solved.

<img width="1000" height="266" alt="image" src="https://github.com/user-attachments/assets/dde62cac-2f09-415a-92aa-da48fe313b3f" />
