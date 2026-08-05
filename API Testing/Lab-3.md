**API Testing || Lab#3 || Finding and exploiting an unused API endpoint**

<img width="756" height="540" alt="image" src="https://github.com/user-attachments/assets/16f8296b-b23b-4488-82f5-6ad789d73626" />

Goal of this lab is to exploit a hidden API endpoint to buy a Lightweight l33t Leather Jacket.

Our credentials → wiener : peter

Lets open the lab and login

<img width="832" height="437" alt="image" src="https://github.com/user-attachments/assets/b61e50b6-842c-4224-b424-bd5ee4add1a8" />

We can see that we have $0.00 store credit. Lets go to home.

<img width="1000" height="502" alt="image" src="https://github.com/user-attachments/assets/437bd941-638d-4f5c-a331-c5978283e167" />

This is the product we have to purchase. Lets view details

<img width="801" height="317" alt="image" src="https://github.com/user-attachments/assets/41b33a32-49f3-44bd-b7a3-3aeb9e90974f" />

<img width="1000" height="482" alt="image" src="https://github.com/user-attachments/assets/a1f60e91-de4c-49ad-b6e4-e948cea5e4ad" />

Now, lets check traffic in Burpsuite

<img width="1000" height="375" alt="image" src="https://github.com/user-attachments/assets/c0444025-4c60-41f2-9531-f0d4aabca4d1" />

There is an API request for price of the product. Lets move this traffic to Repeater

<img width="1000" height="378" alt="image" src="https://github.com/user-attachments/assets/0f1e9084-3a6c-4af9-9969-a0feffbccedc" />

Now, lets check if we have anything in /api

<img width="1000" height="446" alt="image" src="https://github.com/user-attachments/assets/61751dbb-43bf-4580-88b8-78944e3005ae" />

We got an error. 

Lets change the method to POST and check

<img width="1000" height="441" alt="image" src="https://github.com/user-attachments/assets/d72529a0-9ac4-43b9-b0c6-787d7175b928" />

We got an error that method not allowed. However we find that GET and PATCH methods are allowed.

Lets check with PATCH method

<img width="1000" height="408" alt="image" src="https://github.com/user-attachments/assets/57d875c8-608c-4957-9636-e12d912ebf46" />

We got an error that only JSON content type is supported. Lets put content type as JSON in the request

<img width="1000" height="511" alt="image" src="https://github.com/user-attachments/assets/0815a1cc-4993-48e3-9538-eb43f18102ce" />

We got server error. It is because we dont have anything in the body.

<img width="1000" height="441" alt="image" src="https://github.com/user-attachments/assets/eb4c1a76-ec65-46fa-820e-bfb91e3960b5" />

We have added {} which is the part of JSON content type. This time we got an another error. Its saying price parameter is missing.

<img width="1000" height="435" alt="image" src="https://github.com/user-attachments/assets/a6930af0-af18-47e3-85b1-fcfed29ae4df" />

The error is price cannot be -ve and it should be integer. We have passed string value in the price.

Lets try with integer value

<img width="1000" height="539" alt="image" src="https://github.com/user-attachments/assets/49b377e5-52f2-4e1c-8e78-70d7b7b18545" />

And this time price set to $0.10. Lets check

<img width="1000" height="551" alt="image" src="https://github.com/user-attachments/assets/e2567c99-4159-4174-8eb5-0f3f801cbf37" />

And we can see that price of the product is $0.10. 

So this API can change the prices of the product

As we dont have any credit in our account. Lets set the price to $0.00

<img width="1000" height="509" alt="image" src="https://github.com/user-attachments/assets/9bdd5ae2-63d6-448d-a4bd-8fc67893db37" />

Lets check again

<img width="1000" height="499" alt="image" src="https://github.com/user-attachments/assets/ef8b9897-71b5-49f8-8e71-5aca11ca2aa4" />

Price is $0.00 now. Lets empty our cart and add this product again

<img width="697" height="557" alt="image" src="https://github.com/user-attachments/assets/6453c58a-0f17-4897-9be5-f17e47ee818c" />

Lets place order to solve the lab

<img width="1000" height="402" alt="image" src="https://github.com/user-attachments/assets/cce42505-1914-49f5-9472-ae97cc10771f" />

And lab is solved !!!
