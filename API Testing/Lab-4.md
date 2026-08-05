**API Testing || Lab#4 || Exploiting a mass assignment vulnerability**

<img width="780" height="567" alt="image" src="https://github.com/user-attachments/assets/85e01b16-8f5e-4f1e-a656-41d013f56be7" />

Goal of this lab is to find and exploit a mass assignment vulnerability to buy a Lightweight l33t Leather Jacket.

Our credentials :- wiener : peter

Lets start the lab and login

<img width="697" height="366" alt="image" src="https://github.com/user-attachments/assets/d4e2387d-976f-4a7d-a17c-a5be5fcd2645" />

We can see that we have $0.00 store credit. Lets go to home.

<img width="1000" height="587" alt="image" src="https://github.com/user-attachments/assets/c3e5eb67-9f4a-4d0e-847d-1b2582c4eeeb" />

This is the product we have to purchase. Lets view details

<img width="805" height="287" alt="image" src="https://github.com/user-attachments/assets/fc0d2087-a022-4654-83b3-affb2493d231" />

<img width="870" height="362" alt="image" src="https://github.com/user-attachments/assets/b73aaf56-ac7c-4c0b-975d-f165bd6ee1d6" />

Lets place the order

<img width="636" height="365" alt="image" src="https://github.com/user-attachments/assets/42915955-d847-4640-8169-0d59c997eaf9" />

Now, lets check traffic in Burpsuite.

Now we have two traffic that contains API.

1st traffic has GET method. I think its the one when we add the product in the cart. It shows if any discount is there on the product or not. It also shows the product item details.

<img width="1000" height="445" alt="image" src="https://github.com/user-attachments/assets/34bdbc49-1592-456f-ae1f-22ee9fe08293" />

The other traffic that has API parameter is when we place the order. It has POST method. In the response there is a message INSUFFICIENT_FUNDS.

<img width="1000" height="514" alt="image" src="https://github.com/user-attachments/assets/75cf8453-446a-459b-b491-017fb870950f" />

Lets move both traffic to Repeater and check one by one

Now, in the POST method traffic, there is item details but there is no item price. But we have item price parameter in GET method traffic. Lets put item price parameter in POST method traffic

<img width="1000" height="594" alt="image" src="https://github.com/user-attachments/assets/5ab001b2-b21c-43be-93ef-6e6a30c7fea6" />

We got INSUFFICIENT_FUNDS message. Lets make the price 0 and check

<img width="1000" height="551" alt="image" src="https://github.com/user-attachments/assets/e322b460-7f93-4acf-b088-c98fa683281e" />

Again we got the same error. 

Now, in the GET method traffic there is a parameter chosen_discoun and it has percentage of discount. 

Lets add this parameter in POST method traffic. Also we will remove item_price parameter.

<img width="1000" height="601" alt="image" src="https://github.com/user-attachments/assets/d97d6f99-dbad-49b4-97a8-6be4b9a5b17d" />

We got the same message.

Lets change  the percentage to 200 and check

<img width="1000" height="587" alt="image" src="https://github.com/user-attachments/assets/b47156a0-ac0f-41cc-bc39-5d857e8193c6" />

We got an error Invalid percentage discount. 

It seems that chosen_discount parameter is working. 

Lets make discount percentage 100

<img width="1000" height="647" alt="image" src="https://github.com/user-attachments/assets/5354151b-3975-4dc5-a13b-6608058e052d" />

And we got confirmation that item has been added in the cart and order placed. 

Lets refresh the page

<img width="1000" height="304" alt="image" src="https://github.com/user-attachments/assets/9e0ba991-9b64-4be7-834c-f6c47187bb0f" />

And we can see the lab is solved !!!
