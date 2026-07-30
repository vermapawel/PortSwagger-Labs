**Broken Access Control ||Lab#12 Multi-step process with no access control on one step**

<img width="880" height="407" alt="image" src="https://github.com/user-attachments/assets/81f56a54-85ff-4338-8e67-319eb5e9b988" />

Goal of this lab is to become administrator user from a normal user.

Lets open the lab and login via administrator

<img width="900" height="263" alt="image" src="https://github.com/user-attachments/assets/764bf00d-6bdf-42d5-b2e1-64219af3b001" />

Lets upgrade the carlos user and check how this application works

<img width="742" height="177" alt="image" src="https://github.com/user-attachments/assets/c87d3c92-3f66-4163-a96b-8f65621e8533" />

Lets check this traffic in Burp suite

<img width="900" height="398" alt="image" src="https://github.com/user-attachments/assets/775abcdb-d17a-42ea-87e0-d90e37813658" />

Lets move these two traffic to Repeater

There is multi step process to upgrade any user.

1st step is to set action on the username to upgrade. 

2nd step is to confirm it we really what to make any user as admin.

Lets login to the regular account

<img width="900" height="476" alt="image" src="https://github.com/user-attachments/assets/eea432a2-9f33-4567-940f-1874596d0343" />

This is the cookie that identifies the normal user 6IM8KIJL5LCT1WpYpklp15SYA8IgpTrk

Lets use this cookie in the admin-roles traffic and see if it works

This is the first traffic where we click upgrade

<img width="900" height="424" alt="image" src="https://github.com/user-attachments/assets/d1bf5f40-a60d-4ecd-ba48-d77574e1602b" />

We got a message Unauthorized. It means access control rules are put on this step. Lets move to the next step where we confirm to upgrade the user.

<img width="900" height="466" alt="image" src="https://github.com/user-attachments/assets/8378bb46-9114-4f64-8ae7-05447cef4444" />

We will change the cookie value and username. We got a 302 response. Lets follow redirection.

<img width="900" height="354" alt="image" src="https://github.com/user-attachments/assets/d31dbdab-c80b-437b-bee0-19fb25b7a592" />

We got a 200 response.

<img width="900" height="366" alt="image" src="https://github.com/user-attachments/assets/b6a88b21-6f03-49e1-9575-173e8f3b0911" />

And lab is solved
