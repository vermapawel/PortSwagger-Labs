**HTTP Host header attacks || Lab#6 || Host validation bypass via connection state attack**

<img width="780" height="512" alt="image" src="https://github.com/user-attachments/assets/5561f8fb-ed42-42ce-872c-c36f31b0c3ac" />

Goal of this lab is to access the internal admin panel located in the 192.168.0.0/24 range, then delete the user carlos.

Lets start the Lab and go to Home page.

<img width="1000" height="379" alt="image" src="https://github.com/user-attachments/assets/7297137c-1338-43d3-a378-e17721c5f1a9" />

Lets check this traffic in Burp suite

<img width="1000" height="376" alt="image" src="https://github.com/user-attachments/assets/4fc38fe2-51fe-4a8a-ab1c-f6fa521da0c6" />

Move this traffic to Repeater.

<img width="1000" height="485" alt="image" src="https://github.com/user-attachments/assets/8f07b101-1eb2-4a31-b6d1-773a12230a3e" />

Now, we will send two requests. The 1st request will have the correct host header so that it can validate. 2nd request will have the host header of the internal server so that we can access it.

IP address of the Admin panel is provided i.e 192.168.0.1/admin

Below is the 1st request. It has the correct host header.

<img width="1000" height="513" alt="image" src="https://github.com/user-attachments/assets/a8a33e49-51d5-4784-a608-8d35880d9d09" />

Below is the 2nd request. It has IP address of the admin panel in the Host header. We have changed the directory to admin as we need admin page.

<img width="1000" height="375" alt="image" src="https://github.com/user-attachments/assets/cfb48b3a-71e6-4332-87e3-f1567f999599" />

If we send this request, it will redirects to the application home page. So if we change the Host header to anything that is not correct, it will redirect to the Home page.

We want admin panel on this internal server 192.168.0.1

Lets go to the 1st request.

Right Click > Add tab to group > New tab group

<img width="987" height="452" alt="image" src="https://github.com/user-attachments/assets/e9465799-2580-4722-ac00-a3ac254ca681" />

<img width="885" height="592" alt="image" src="https://github.com/user-attachments/assets/0cd35e4b-3607-4099-812b-9288e5e0147b" />

We can give any Group name. Click on Create

<img width="996" height="477" alt="image" src="https://github.com/user-attachments/assets/178f2e66-e4b3-4650-9d95-3b4fee252cf7" />

One group is created. We will add 2nd request in this group as well.

Now, to perform this attack both request needs to be in same connection.

<img width="1000" height="423" alt="image" src="https://github.com/user-attachments/assets/d1a99bcc-48f3-419c-ae24-7c7f141e0566" />

<img width="1000" height="471" alt="image" src="https://github.com/user-attachments/assets/c709d1af-af97-4f7c-ba85-5ac81e0c1992" />

Both request is sent under same connection.

<img width="1000" height="570" alt="image" src="https://github.com/user-attachments/assets/4effd028-df7a-4d99-a0b1-ce83f8f3cb21" />

This time we can see for 2nd request we got an Delete user functionality. 

This works because the application is validating the host header on the 1st request and assumes all the other requests that are sent under the same connection has same Host header.

Lets check this response in browser

<img width="812" height="287" alt="image" src="https://github.com/user-attachments/assets/57132a7b-b49f-4cfa-a490-532bdf52c482" />

<img width="1000" height="356" alt="image" src="https://github.com/user-attachments/assets/f4e69776-3a5c-418a-804c-c5c0a2bf4964" />

To solve the lab we have to delete Carlos user.

<img width="972" height="207" alt="image" src="https://github.com/user-attachments/assets/14d5afaa-54ec-4d2f-8737-4575e7c0e03b" />

It will not work from here as this functionality is under 192.168.0.1 domain. And this request is coming from some other domain.

Lets check this traffic

<img width="1000" height="454" alt="image" src="https://github.com/user-attachments/assets/ba3a77e8-e4dc-4546-b715-2d08ea967339" />

Move it to Repeater

Change the Host header to 192.168.0.1 and add this request in the Attack Group. Remove Request 2 from the Group.

Forward this traffic

<img width="1000" height="410" alt="image" src="https://github.com/user-attachments/assets/585ba722-40eb-4781-8a43-5953dfd46cb0" />

We got a 302 Redirect. User carlos has been deleted.

<img width="1000" height="286" alt="image" src="https://github.com/user-attachments/assets/7fa0b32c-44b5-4850-a4b1-5888eb4d4ffa" />

Lab is solved.
