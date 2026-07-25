**SSRF || Lab#2 : Basic SSRF against another back-end system**

<img width="877" height="467" alt="image" src="https://github.com/user-attachments/assets/284de1de-05a6-4924-b2d3-cbcdb4024b38" />

Vulnerable parameter → Stock Check functionality.

Goal of the lab is to scan the internal 192.168.0.X range for an admin interface on port 8080, and then delete user carlos.

Lets open the Lab

<img width="797" height="611" alt="image" src="https://github.com/user-attachments/assets/bb972b4b-364a-4103-9588-c3078ab68b06" />

When we click on Check stock, it will display how many units are available in that particular store for example, 30 units are available in Paris store.

Lets intercept this traffic in Burp suite

<img width="1100" height="329" alt="image" src="https://github.com/user-attachments/assets/4c385f0c-6ccf-4db7-a2b4-2c2fbf43da5a" />

Lets move this traffic to Repeater

<img width="1031" height="497" alt="image" src="https://github.com/user-attachments/assets/e4bdc7f8-1613-421c-a268-d6bc331bb648" />

We can see there is a URL as it starts with http and have some parameter. Its seems its URL encoded. Lets decode it.

stockApi=http://192.168.0.1:8080/product/stock/check?productId=1&storeId=1

So, this application is talking to a different ip 192.168.0.1 on port 8080 to check the stock of an item. The path to the stock check feature is /product/stock/check

Lets check if we can access the external IP 192.168.0.1 on port 8080

<img width="1015" height="442" alt="image" src="https://github.com/user-attachments/assets/40a83ff0-78e5-4126-a71e-f01b55f87122" />

We again got an error. Let check if any other application that running in this network

<img width="1100" height="502" alt="image" src="https://github.com/user-attachments/assets/e1a70ad3-04b2-4dd0-859f-96d262f2f3d2" />

We got 500 Internal Server Error.

Lets check again

<img width="1100" height="495" alt="image" src="https://github.com/user-attachments/assets/6b3d8998-69f4-411a-8dc0-1f4d96bc36d1" />

Again we got 500 Internal server error.

Now we have to check for all 255 octate. Let move this traffic to Intruder

<img width="1100" height="567" alt="image" src="https://github.com/user-attachments/assets/5ee9a58c-da00-40ee-9109-2809728096fd" />

<img width="1100" height="572" alt="image" src="https://github.com/user-attachments/assets/5f7eceec-6a70-49af-92e3-06236385f0f2" />

For 95, the status code is 404 and the response is Not Found. It means some application is running on 192.168.0.95

Lets move this traffic to Repeater and check further

<img width="1100" height="470" alt="image" src="https://github.com/user-attachments/assets/302793af-1fd9-4128-81e7-89d4c15db3e6" />

We got a 200 OK responce when we add /admin in the URL.

<img width="1100" height="399" alt="image" src="https://github.com/user-attachments/assets/56a5e89a-323a-440b-a81e-67fb57709340" />

We can see Admin page and users details. To solve the lab we need to delete carlos user.

Lets find the path for carlos user.

<img width="1100" height="446" alt="image" src="https://github.com/user-attachments/assets/22e340d9-464f-4733-acf6-7d4889ce575a" />

We got the path. Let try to delete the user.

<img width="1100" height="490" alt="image" src="https://github.com/user-attachments/assets/231b31ec-2547-4f0d-a529-0483442a9a1c" />

We got a 302 Found. It means its getting re-directed to an another page.

Lets check if user is deleted or not.

<img width="1100" height="419" alt="image" src="https://github.com/user-attachments/assets/ef0ac189-bdb8-4916-afc7-29a150aec46b" />

We can see user got deleted and lab is solved

<img width="845" height="262" alt="image" src="https://github.com/user-attachments/assets/d20d7b1f-63ed-4703-a8c1-b68f61ee0e41" />
