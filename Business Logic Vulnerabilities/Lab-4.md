**Business Logic Vulnerabilities || Lab#4 || Flawed enforcement of business rules**

<img width="785" height="447" alt="image" src="https://github.com/user-attachments/assets/b492ef8f-0a14-4253-96d7-8e16d8e2cc9a" />

Goal of this Lab is to buy Leather jacket. 

We have our credentials given wiener : peter

Lets start the lab and login with our credentials

<img width="1000" height="654" alt="image" src="https://github.com/user-attachments/assets/96d2d7c3-f6f6-4275-977e-31f6ab0bc5e0" />

We have a $100 credit in our account. Lets add the product in the cart.

<img width="786" height="575" alt="image" src="https://github.com/user-attachments/assets/5cd3fd43-de7e-4d1c-bd3f-cb44bbafd907" />

We have a code provided. Lets check the code

<img width="671" height="581" alt="image" src="https://github.com/user-attachments/assets/8bf1bcb1-da58-4ac9-ba19-ae65980c28c1" />

The code got applied successfully and we got a discount of $5. 

Lets check this traffic in Burp suite

<img width="942" height="555" alt="image" src="https://github.com/user-attachments/assets/64bc609b-f460-492a-a4f6-a34914af73ee" />

Lets move this traffic to Repeater

<img width="762" height="577" alt="image" src="https://github.com/user-attachments/assets/d8d120d0-5268-4200-a062-1abd2fa65623" />

There are two parameters here. csrf is the standard parameter, The other parameter is coupon. 

Lets if we can apply this coupon again. Forward this traffic

<img width="1000" height="562" alt="image" src="https://github.com/user-attachments/assets/a0594ce4-0c23-4cac-b548-83d3fa8c5290" />

We got a message coupon is already applied. So, we cannot apply same coupon multiple times.

Lets go to home and check if there is any new functionality.

There is an option to sign up to newsletter. Lets Sign up

<img width="862" height="150" alt="image" src="https://github.com/user-attachments/assets/c2e21c72-f5d8-454b-a2d6-a533ba4b4538" />

<img width="996" height="281" alt="image" src="https://github.com/user-attachments/assets/80f56864-ec51-451e-85da-e5d82817ac80" />

We got a new coupon SIGNUP30. Lets check this coupon at checkout

<img width="642" height="612" alt="image" src="https://github.com/user-attachments/assets/a2d4efda-6766-45b7-9fbb-14ef4ecfce2e" />

This coupon also applied. Lets check if we can apply this coupon multiple times or not.

<img width="1000" height="493" alt="image" src="https://github.com/user-attachments/assets/1cc00eb0-7c7d-4249-afd8-627ef4d14585" />

We got message coupon already applied.

Lets try to apply the previous coupon NEWCUST5  and check

<img width="1000" height="525" alt="image" src="https://github.com/user-attachments/assets/fea9f9c4-ed6c-4c34-aaf2-2fe872528c97" />

And this coupon is applied again.

<img width="617" height="617" alt="image" src="https://github.com/user-attachments/assets/03c1f946-3bcb-4c3c-abac-da6b9a9afb85" />

Now, lets try to apply SIGNUP30

<img width="1000" height="570" alt="image" src="https://github.com/user-attachments/assets/b1353d61-1315-4ac0-9a15-7fdb524ded70" />

The coupon got applied again.

<img width="717" height="647" alt="image" src="https://github.com/user-attachments/assets/48beb7d0-21aa-4b50-b7d3-c3ea3d35194b" />

The idea here is we cannot apply same coupon twice in a row. The backend code only verify the last coupon that we have applied. 

Lets keep alternating the coupons until the price drops under $100

<img width="786" height="742" alt="image" src="https://github.com/user-attachments/assets/3ebe20f5-6be5-460e-8d6b-7ceff139cf1d" />

Lets place the order

<img width="887" height="547" alt="image" src="https://github.com/user-attachments/assets/19e8e19f-adc1-41b9-bc1c-77e9f0a6317e" />

And lab is solved
