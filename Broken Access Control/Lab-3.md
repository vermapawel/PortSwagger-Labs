**Broken Access Control ||Lab #3 User role controlled by request parameter**

<img width="857" height="360" alt="image" src="https://github.com/user-attachments/assets/c7b07d99-fe8c-4323-967d-ceca81fa6f0d" />

We have our credential wiener:peter

Goal of this lab is to delete user carlos.

Lets start the lab and login with our credentials.

<img width="900" height="373" alt="image" src="https://github.com/user-attachments/assets/2a921f3a-9ffe-40ba-9d92-9642aa55cf91" />

Lets capture this traffic in Burp suite

<img width="900" height="428" alt="image" src="https://github.com/user-attachments/assets/e9b81751-860c-473e-8b19-fd597813a42d" />

We can see its a POST request and 302 response. 

Also, there are two cookies, one is Admin with is set as false and other is session cookie.

This is the traffic where we have put credentials and my-account page has opened.

<img width="900" height="403" alt="image" src="https://github.com/user-attachments/assets/c0f6f55c-1dc0-480d-a953-84a1757477ea" />

Lets move this traffic to Repeater

<img width="900" height="446" alt="image" src="https://github.com/user-attachments/assets/b856a291-a9c3-4481-9035-e5fdccbdafa5" />

Now, please note that in the request, Admin cookie is false and in the response, there is nothing from admin keyword. 

Lets make admin cookie true and check the traffic

<img width="900" height="458" alt="image" src="https://github.com/user-attachments/assets/d3111954-09ab-48e2-a9e5-a42361d8462b" />

Now, admin panel appears in the response. So admin cookie is the mechanism to control admin panel. 

Now, lets make admin cookie as true from the Developers tool and refresh the page.

<img width="900" height="572" alt="image" src="https://github.com/user-attachments/assets/972b1ae7-120f-4dd6-9185-64c69609d65b" />

We can see that Admin panel appears.

<img width="900" height="280" alt="image" src="https://github.com/user-attachments/assets/d4509ed2-8912-432d-9713-8842e09dc34c" />

To complete the lab, lets delete user carlos

<img width="882" height="461" alt="image" src="https://github.com/user-attachments/assets/9bde3427-5de7-4e05-8d2a-acc2ae9fe605" />

And lab is solved.




