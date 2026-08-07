**HTTP Host header attacks || Lab#2 || Host header authentication bypass**

<img width="802" height="397" alt="image" src="https://github.com/user-attachments/assets/0a1a6f6a-78a7-459a-b58d-f8abb20070b7" />

Goal of this lab is to delete user carlos. 

Lets start the lab and check login functionality.

Its asking for username and password.

Lets check it we have robots.txt file

<img width="1000" height="458" alt="image" src="https://github.com/user-attachments/assets/7ed9b4ee-53fc-4b6d-8131-4c7f9e731312" />

<img width="996" height="242" alt="image" src="https://github.com/user-attachments/assets/3db0c162-57ff-402e-9f53-aaaf075dda99" />

Lets check /admin

<img width="1000" height="360" alt="image" src="https://github.com/user-attachments/assets/29b29b01-1395-47f4-a06b-366126d2c091" />

admin page is only allowed for local user. 

So we identified that there is an admin page, and its allowed for all local user and not only for administrator. 

Lets check this traffic in Burpsuite

<img width="1000" height="452" alt="image" src="https://github.com/user-attachments/assets/27d4d15e-366e-4b51-bc80-8e1ebbd762a4" />

This is a GET request. Lets move this traffic to Repeater

<img width="1000" height="468" alt="image" src="https://github.com/user-attachments/assets/dabb4c15-8eb6-4f16-a10a-b3e447dc90d0" />

Here, the host header is the hostname of the application. Lets enter a different hostname and check

<img width="1000" height="506" alt="image" src="https://github.com/user-attachments/assets/199ba275-7b76-4bb6-8bac-7478552c5049" />

We have changed the hostname and still get same message. It seems that the application may not care what the host is. 

Lets check with localhost

<img width="1000" height="509" alt="image" src="https://github.com/user-attachments/assets/00b664ff-ae72-4c34-b365-2e0ce5dd5fee" />

And we see Admin panel and Users. Lets open this response in browser

<img width="851" height="770" alt="image" src="https://github.com/user-attachments/assets/09b1a0ca-769d-40fb-b5cd-c184e4556575" />

<img width="772" height="426" alt="image" src="https://github.com/user-attachments/assets/bbe960d9-ed13-439c-a35d-945600abcb10" />

Paste this link in the browser

<img width="1000" height="285" alt="image" src="https://github.com/user-attachments/assets/82987409-ef31-473a-8d12-48a3967613a8" />

We got the same message, and this is because by default the application takes the hostname of the application and put in the Host header. 

Lets check this traffic in Burpsuite

<img width="1000" height="414" alt="image" src="https://github.com/user-attachments/assets/b4d282b5-dd12-46e0-abbb-74973af98a32" />

We can see the code is 401 Unauthorized and Host is same as in the browser. Lets move this traffic to Repeater

<img width="1000" height="557" alt="image" src="https://github.com/user-attachments/assets/5bc14237-f3cd-4335-9ca5-cd1d40f8f693" />

Lets change the Host to localhost so that application thinks this traffic is coming locally and its already authenticated. We got a 302 Response code.

<img width="1000" height="240" alt="image" src="https://github.com/user-attachments/assets/f241769b-16fd-4889-bb3e-fc7fd472a92f" />

It will delete the user carlos and lab is solved.
