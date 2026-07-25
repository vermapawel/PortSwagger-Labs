**SSRF || Lab#1 : Basic SSRF against the local server**

<img width="882" height="342" alt="image" src="https://github.com/user-attachments/assets/324a7f4e-8c36-4316-8a24-213bda885101" />

Vulnerable parameter → Stock Check functionality.

Goal of the lab is to change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos

Lets open the Lab

<img width="820" height="632" alt="image" src="https://github.com/user-attachments/assets/77c82983-2bf9-4ae7-8526-dbf0415077eb" />

When we click on Check stock, it will display how many units are available in that particular store for example, 576 units are available in Paris store.

Lets intercept this traffic in Burp suite

<img width="1100" height="367" alt="image" src="https://github.com/user-attachments/assets/532917f3-defc-4113-b6ab-502cc6dd4472" />

Lets move this traffic to Repeater

<img width="1100" height="515" alt="image" src="https://github.com/user-attachments/assets/ecdeb369-bb08-4f60-ac9c-f36576d3b1e6" />

We can see there is a URL as it starts with http and have some parameter. Its seems its URL encoded. Lets decode it.

stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1

So, this application is talking to a different URL stock.weliketoshop on port 8080 to check the stock of an item. The path to the stock check feature is /product/stock/check

So anytime we see an URL on the request, we should check for SSRF.

Lets forward this traffic

<img width="950" height="402" alt="image" src="https://github.com/user-attachments/assets/60f0a142-757c-4eae-9f2e-d7b4ada9c7b7" />

We got an error Missing parameter.

Lets encode the URL and forward the traffic ag

<img width="1100" height="490" alt="image" src="https://github.com/user-attachments/assets/67c8f2ab-da20-4b7e-849b-ced0d40cf6d5" />

Now, lets check if we can access the external application itself

<img width="1072" height="512" alt="image" src="https://github.com/user-attachments/assets/6f263176-f779-45a0-80af-e3e5746652a2" />

We got an error. Lets URL encode and try again

<img width="1017" height="506" alt="image" src="https://github.com/user-attachments/assets/10c1c9a4-88ca-4fda-a5aa-2cf159816a40" />

We again got an error. It seems we cannot call this URL unless we provide some parameter.

Lets check if any application is running in local host

<img width="1100" height="474" alt="image" src="https://github.com/user-attachments/assets/8ab3b6d5-334d-4905-a223-7539e83d33f1" />

We got a 200 OK response, it means this application is vulnerable to SSRF.

<img width="1100" height="518" alt="image" src="https://github.com/user-attachments/assets/05974db0-0cd3-4e06-aa54-d789844db985" />

We see an Admin panel, which was not visible earlier.

Its seems that the same application is running on the Local host as well and application dose not need to login to access the admin panel because it assumed that if you are able to access the application, you are already authenticated. There is a trust relationship between the application and the server where its running, it assumes that we are authenticated.

However when we are visiting the same application externally, we need to login.

Lets search the path for admin

<img width="1100" height="569" alt="image" src="https://github.com/user-attachments/assets/200460d7-ecb6-48d9-ae41-aefd9d83a984" />

Now, lets add this path to the local host

<img width="1100" height="479" alt="image" src="https://github.com/user-attachments/assets/a7446bc2-198d-48d3-a1de-cd13572f1b2a" />

We got a 200 OK response. Lets Render it.

<img width="1100" height="485" alt="image" src="https://github.com/user-attachments/assets/29fbc4cf-2567-4110-9adc-221b04b29d21" />

We can see there are two users. To solve the lab we have to delete carlos.

Lets find its path

<img width="1100" height="515" alt="image" src="https://github.com/user-attachments/assets/7c5685aa-8248-426a-bd5d-90ad35942bb9" />

The path is /admin/delete?username=carlos

<img width="1100" height="561" alt="image" src="https://github.com/user-attachments/assets/9d8a8760-9782-492a-b58d-3332e8512c18" />

We got a 302 response code. It means its getting re-directed to an another page. Lets Follow redirection

<img width="1100" height="520" alt="image" src="https://github.com/user-attachments/assets/f65186d1-776f-42f4-a811-ff0e3ce5eab1" />

<img width="1100" height="522" alt="image" src="https://github.com/user-attachments/assets/7398bcb7-cd0d-4f85-a33b-02bad64fdf17" />

Lets check if carlos user was deleted or not. Lets go back to admin page

<img width="1100" height="561" alt="image" src="https://github.com/user-attachments/assets/0705b777-e952-4c26-8d2e-d919a89dc6de" />

There are 0 matches for carlos, it means user has been deleted.

<img width="1100" height="521" alt="image" src="https://github.com/user-attachments/assets/80859e04-59c5-436f-9b22-ea6742845ab7" />

And the lab is solved

<img width="881" height="252" alt="image" src="https://github.com/user-attachments/assets/d54cd35b-2c9d-4f03-8cb5-0ad0ea2ccaf7" />
