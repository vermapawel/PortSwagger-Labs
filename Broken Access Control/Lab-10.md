**Broken Access Control ||Lab #10 User ID controlled by param with password disclosure**

<img width="867" height="392" alt="image" src="https://github.com/user-attachments/assets/81551867-0895-4d57-9478-1c6a54b2f9d6" />

Goal of this lab is to delete user carlos. 

Our credentials have been provided wiener:peter

Lets open the lab and login with our credentials

<img width="900" height="468" alt="image" src="https://github.com/user-attachments/assets/957253f2-80b2-46d4-b806-5a423cd19f96" />

There is an option to update email address and password.

Lets check this traffic in Burp suite

<img width="900" height="339" alt="image" src="https://github.com/user-attachments/assets/ef749adf-8514-47ba-87ba-69da0fbffa3a" />

There is a parameter id that takes username. 

Lets check for administrator

<img width="900" height="322" alt="image" src="https://github.com/user-attachments/assets/2f216154-9111-477e-802f-8387c4c9430a" />

We got a 200 response. Also we got the password for administrator dn6xqdmn6w1btdbr67bk

Lets login via administrator

<img width="900" height="392" alt="image" src="https://github.com/user-attachments/assets/b479b280-4344-434a-b252-3612d5b822b2" />

Now there is Admin panel. Lets delete user carlos to solve the lab

<img width="657" height="210" alt="image" src="https://github.com/user-attachments/assets/06b62698-2620-4312-aec3-3d08db104ac9" />

<img width="792" height="322" alt="image" src="https://github.com/user-attachments/assets/2ffe91c4-5a8e-4dab-9bec-f715a77e8665" />

And lab is solved
