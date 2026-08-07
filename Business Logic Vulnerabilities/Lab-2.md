**Business Logic Vulnerabilities || Lab#2 || High-level logic vulnerability**

<img width="792" height="427" alt="image" src="https://github.com/user-attachments/assets/feace26c-066b-44cb-937b-8c182d617742" />

Goal - Exploit the logic flaw to buy the product for an unintended price.

Credentials :- wiener : peter

Lets start the lab and login

<img width="1000" height="515" alt="image" src="https://github.com/user-attachments/assets/39413247-322e-40bb-b4e0-b822547cc6f5" />

Lets add the product in the cart

<img width="851" height="362" alt="image" src="https://github.com/user-attachments/assets/7356b64e-ebca-4f3d-8ae1-9f32c812612f" />

<img width="1000" height="483" alt="image" src="https://github.com/user-attachments/assets/b5c62b16-0d7b-4b9a-8c88-a81145830bf0" />

Lets intercept this traffic in Burp suite

<img width="1000" height="604" alt="image" src="https://github.com/user-attachments/assets/1f746e9c-5a9b-4d03-b01e-c8ebac38fbd7" />

Lets move this traffic to Repeater

<img width="1000" height="566" alt="image" src="https://github.com/user-attachments/assets/2f7d37f6-b6d1-4491-a849-5e987401d438" />

This is a POST request. There are some parameters. This time there is no price parameter. 

Lets manipulate quantity parameter value and check how application behaves. Lets forward this traffic.

<img width="1000" height="397" alt="image" src="https://github.com/user-attachments/assets/ddbbd8ae-03e2-402f-abb1-89960a7ebbbd" />

One quantity we have already added by application, and when we forward the traffic again, one more quantity got added. So in Cart there are 2 quantities. 

Lets decrease the quantity and check what happens

<img width="1000" height="452" alt="image" src="https://github.com/user-attachments/assets/fa95324a-bc99-4bdf-8c89-ddecf818c3c1" />

So we can add negative item in the cart. The price go in negative. Lets try to buy this

<img width="640" height="537" alt="image" src="https://github.com/user-attachments/assets/81661e8d-4fcb-41da-8f5d-8bcf504e6add" />

However when we tried to place the order, it not accepting. The price cannot be in negative. 

Lets add an another item in the cart.

<img width="977" height="297" alt="image" src="https://github.com/user-attachments/assets/6c40c2dd-c101-4702-a475-7e2b95751984" />

Lets move this traffic to Burp suite

<img width="1000" height="539" alt="image" src="https://github.com/user-attachments/assets/d11d2d9c-fb6a-4583-b83e-5f4c6d59bb5e" />

Lets check the cart

<img width="665" height="562" alt="image" src="https://github.com/user-attachments/assets/cc2053bf-f40c-4042-b630-f8e2ac897af7" />

Now we have total of $1410.78. As we found that we can add negative quantities, we will increase negative quantities until the whole amount comes under $100

<img width="1000" height="462" alt="image" src="https://github.com/user-attachments/assets/e88ea7b1-3797-4c97-9d41-878f5a34f978" />

Now, the total amount is $746 dollars. Lets add more negative quantities

We have added 10 more negative quantities and total price is $8.96 which is under the credit $100

<img width="1000" height="432" alt="image" src="https://github.com/user-attachments/assets/08e40a52-bc2b-4035-a596-d6b7edaf7257" />

Lets place order

<img width="811" height="400" alt="image" src="https://github.com/user-attachments/assets/51f83a8f-1408-411c-991f-9725e304bcf5" />

We have successfully purchased the Leather jacket and lab is solved.
