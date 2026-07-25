**Authentication Vulnerabilities — Lab #5 Username enumeration via response timing**

<img width="841" height="592" alt="image" src="https://github.com/user-attachments/assets/c18e5c34-7260-4c2a-850f-0fc2798d76f1" />

List of username and password are provided.

Your credentials: wiener:peter

Goal of this Lab is to enumerate the username and then brute force its password.

Lets start the lab

We will put a random username and password and inspect the traffic.

<img width="982" height="426" alt="image" src="https://github.com/user-attachments/assets/63b69328-c540-42f6-99eb-4083fe0cb01c" />

Lets intercept the traffic in Burpsuite

<img width="1100" height="452" alt="image" src="https://github.com/user-attachments/assets/af30378d-cd0e-40ea-98f5-627ad0dd1600" />

Lets move this traffic to repeater.

<img width="1100" height="441" alt="image" src="https://github.com/user-attachments/assets/0c68c5f2-b151-4726-828e-7b72b026690d" />

This request takes approx. 175 milliseconds.

Now lets put a valid username and an invalid password.

<img width="1100" height="406" alt="image" src="https://github.com/user-attachments/assets/8766faab-3169-4085-ac23-a31caf3456d9" />

It takes approx. 196 miliseconds. Lets try again.

After trying 2–3 time we can see that the response time is 212 miliseconds.

<img width="1100" height="404" alt="image" src="https://github.com/user-attachments/assets/7a247f9b-f46e-4187-bdf4-1342d759e9f4" />

This is because we are locked out for 30 mins.

<img width="1097" height="537" alt="image" src="https://github.com/user-attachments/assets/c138b7c2-062f-4c21-bdde-399a7cbcfcc0" />

So there is a mechanism in the login form if we put incorrect credentials, our IP will be blocked for 30 mins.

Now, to over come this we can try to add X-Forwarded-For: 1 and then send the request.

<img width="1100" height="458" alt="image" src="https://github.com/user-attachments/assets/2d568d45-12c2-41c5-a017-22a61248defa" />

Now we dont get that 30 mins time out error.

Setting X-Forwarded-For to arbitrary values is often used to **Bypass IP-based restrictions** (e.g., brute force protections that block repeated attempts from the same IP). It also used to Spoof the client IP to trick the server into thinking the request comes from somewhere else.

So after every 3 request, we have to change the X-Forwarded-For value so that we dont get 30 mins time out error.

Now, we dont see much time difference when we put valid username and invalid password. Lets try few more things

Lets increase the password length and try.

<img width="1100" height="458" alt="image" src="https://github.com/user-attachments/assets/b658213e-926e-49f4-bb45-d650c79f6d97" />

Time is 194 miliseconds

Lets increase the password length and try again. Also as we locked for 30 mins, lets change X-Forwarded-For: 2

<img width="1100" height="595" alt="image" src="https://github.com/user-attachments/assets/a6b44233-5d71-46dd-b3ba-0080a3282673" />

This time time period is 693 milliseconds. So, every time we are increasing the password length, the application is taking more time.

Now, lets put an invalid username and try again, keeping the same password length.

<img width="1100" height="568" alt="image" src="https://github.com/user-attachments/assets/3c1222d1-7dd7-401a-a97c-20cb1ba69886" />

Time period is 171 milliseconds. So when the username is correct and password length is long, its taking more time when username is incorrect and password list is same.

It means, the application is checking username first, it username is incorrect, it does not check the password hence processing time is less. But when username is correct, then application is checking password and since we have sent a long password its taking more time to execute.

We can take advantage of the feature of the application. Lets move this traffic to Intruder.

We will select attack type as Pitchfork attack as we have to bruteforce in two areas.

Due to the 30 mins lock functionality, we have to keep changing the X-Forwarder-For value. We will add one position to its value. Payload Type will be Numbers.

<img width="1100" height="582" alt="image" src="https://github.com/user-attachments/assets/be3f5702-dab3-4e51-ba01-6ea33efd85d0" />

Second position will be username. We have a list of username provided. We will use that list for bruteforcing.

<img width="797" height="415" alt="image" src="https://github.com/user-attachments/assets/0975f635-c2c1-4642-9893-0d9a12503b8c" />

Copy all the username and paste in the payload.

<img width="1100" height="596" alt="image" src="https://github.com/user-attachments/assets/01a60664-84a0-45ec-885d-63ddcadb9e75" />

Lets start the attack

<img width="1100" height="616" alt="image" src="https://github.com/user-attachments/assets/3796e466-fbf7-4c74-a01c-cb403e781114" />

Now, when the username is **ak**, the response time it high, i.e 618. It means alpha is a correct username and therefore the application try to check the lengthy password, due to which response time is high.

Now we got a valid username i.e ak. Now lets brute force for passwords.

We have a list of password provided. We will use that list of passwords for bruteforcing.

<img width="1100" height="476" alt="image" src="https://github.com/user-attachments/assets/cefd513e-133f-4d30-8d95-c818c70ce94a" />

<img width="1100" height="643" alt="image" src="https://github.com/user-attachments/assets/70e1e814-ba89-4a96-89c3-62c3730e8de6" />

Now, when we try to login we are locked for 30 mins.

<img width="997" height="440" alt="image" src="https://github.com/user-attachments/assets/a41dc9ea-20a6-4034-9adf-22f7c27682b4" />

Lets add X-Forwarded-For header and forward the traffic.

<img width="1100" height="554" alt="image" src="https://github.com/user-attachments/assets/0c2b6dbb-4cd4-4b94-a7b5-4282256f3778" />

We got a 302 code, means the page is redirected to somewhere. Lets follow the redirection.

<img width="1100" height="572" alt="image" src="https://github.com/user-attachments/assets/6bbd02e2-2faf-41a9-94bb-52cd68e54340" />

Lets forward the traffic and follow the redirection.

<img width="1100" height="515" alt="image" src="https://github.com/user-attachments/assets/a7670935-b2ab-463d-95ac-16b890b5be0f" />

This time we got 200 OK response.

<img width="746" height="317" alt="image" src="https://github.com/user-attachments/assets/b8441eb5-7219-41ca-9f39-d2b8d301e20c" />

Now, we dont see that 30 mins lockout error. Lets put the username and password that we have founded

<img width="707" height="392" alt="image" src="https://github.com/user-attachments/assets/8294d03a-1900-4045-aa24-536620407cff" />

And lab is solved
