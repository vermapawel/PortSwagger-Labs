**Broken Access Control ||Lab #7 User ID controlled by request parameter**

<img width="877" height="422" alt="image" src="https://github.com/user-attachments/assets/ed4a15af-757b-412c-bd7a-a7ae6b051525" />

Goal of this lab is to get API key. 

We have our credentials wiener:peter

Lets start the lab and login

<img width="857" height="430" alt="image" src="https://github.com/user-attachments/assets/6daee88d-181d-488d-bde5-7083fd518d04" />

Lets check this traffic in Burp suite

<img width="900" height="335" alt="image" src="https://github.com/user-attachments/assets/98a51567-fb47-4c41-80c5-076b0049a2dc" />

Lets move this traffic to Repeater

<img width="900" height="369" alt="image" src="https://github.com/user-attachments/assets/ddf078a1-ec4c-4716-b985-b35b9376fb3b" />

Now, we can see that there is a parameter id that takes username. Lets change the username to carlos and forward the traffic

<img width="900" height="265" alt="image" src="https://github.com/user-attachments/assets/e2009dd4-9896-427b-8eaf-a295e3b37a20" />

We found the API key for the user carlos. This parameter is client controllable and its not getting checked on the backend.

<img width="900" height="318" alt="image" src="https://github.com/user-attachments/assets/2b229679-720c-4ba8-8448-0b3a79039589" />

And lab is solved

<img width="787" height="287" alt="image" src="https://github.com/user-attachments/assets/b145af60-c26b-42ed-88df-39fe99a19763" />
