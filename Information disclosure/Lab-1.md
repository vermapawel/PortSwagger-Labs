**Information disclosure || Lab#1 || Information disclosure in error messages**

<img width="772" height="372" alt="image" src="https://github.com/user-attachments/assets/0c3f0ded-0e6b-4839-afc7-3f711e2aea31" />

To solve the lab, we need to get the version of the third party framework.

<img width="1000" height="393" alt="image" src="https://github.com/user-attachments/assets/46eacbd5-72cd-46b3-8d1f-4e241891fece" />

Lets start the lab and check products. We are looking for parameters in the application as any parameter should talk to the backend.

Lets intercept the traffic in burp suite

<img width="1000" height="407" alt="image" src="https://github.com/user-attachments/assets/5316da2e-58b1-4fe9-87cc-8ffb9e619c4c" />

We got a parameter productid. Lets move this traffic to Repeater

<img width="1000" height="442" alt="image" src="https://github.com/user-attachments/assets/3d9da137-9910-49fd-a3b7-c020c493d672" />

Now, let change the parameter productid values and check how application behaves. 

We will give unexpected input so that if the application don't have proper error handling, it can disclose some important information.

<img width="1000" height="556" alt="image" src="https://github.com/user-attachments/assets/f83bb0f0-bc13-4a7b-96bc-88fb3d715a84" />

We have passed the value ' in parameter which is unexpected and it display that Apache server is running. 

The idea over here is to get some information about the application.

<img width="842" height="267" alt="image" src="https://github.com/user-attachments/assets/55748f9c-63f7-40d6-91b1-1e1908cdae13" />

<img width="892" height="322" alt="image" src="https://github.com/user-attachments/assets/0d6fc7e4-571c-49d8-b241-dca90fae7acc" />

And lab is solved

<img width="932" height="335" alt="image" src="https://github.com/user-attachments/assets/a385917c-4788-4e8f-87d9-c70a0dca710c" />
