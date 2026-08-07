**Business Logic Vulnerabilities || Lab#1 || Business Logic Vulnerabilities**

<img width="772" height="342" alt="image" src="https://github.com/user-attachments/assets/414af877-9882-4996-a4a2-016b91bb69eb" />

Goal - Exploit a logic flaw to buy a Lightweight l33t leather jacket.

Credentials:- wiener : peter

Lets start the Lab and login

<img width="1000" height="593" alt="image" src="https://github.com/user-attachments/assets/04dd47be-bd37-4939-9277-391fc9c365bf" />

We have a Store credit of $100. The price of the product is $1337. Lets view details

<img width="795" height="232" alt="image" src="https://github.com/user-attachments/assets/8706dc16-b005-491e-8226-98df4b890afc" />

Lets add the product to the cart and go to cart

<img width="1000" height="269" alt="image" src="https://github.com/user-attachments/assets/b629294b-1c1a-4804-83b3-b50d3844c936" />

<img width="832" height="611" alt="image" src="https://github.com/user-attachments/assets/17782d1f-496c-44e6-b35d-38fef2897717" />

Lets check the traffic in Burp suite

<img width="1000" height="592" alt="image" src="https://github.com/user-attachments/assets/764d2c40-bb8e-4b15-9f5c-adeb251c35a7" />

This is a POST request. This traffic contains all the details regarding the product. Lets move this traffic to Repeater

Here we have multiple parameters. One of them is price. 

Lets check if we can manipulate the price parameter. The idea over here is, if this price parameter is only validated on the client side, we should be able to change its value.

<img width="1000" height="576" alt="image" src="https://github.com/user-attachments/assets/82b25538-282f-40f5-8e49-6988f88b2625" />

<img width="811" height="582" alt="image" src="https://github.com/user-attachments/assets/406ab195-a399-4226-afa1-6090a750fb1d" />

We can see that the product has been added to the cart. Lets place the order.

<img width="916" height="456" alt="image" src="https://github.com/user-attachments/assets/93aab174-1b5d-4106-97f7-06873a4cdecd" />

And lab is solved
