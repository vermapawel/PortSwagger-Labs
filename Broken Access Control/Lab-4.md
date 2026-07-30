**Broken Access Control ||Lab #4 User role can be modified in user profile**

<img width="877" height="422" alt="image" src="https://github.com/user-attachments/assets/b85b315d-8201-4215-9db1-b719f4735d6e" />

We have our credentials give wiener:peter

Goal of this lab is to delete user carlos

Lets start the lab and login with our credentials.

<img width="900" height="340" alt="image" src="https://github.com/user-attachments/assets/e0b8ce69-58d8-43f9-b542-1076831d61c6" />

Lets capture traffic in Burp suite

<img width="900" height="468" alt="image" src="https://github.com/user-attachments/assets/5a8added-76dd-42b4-b249-b9ee469bc6c0" />

This is POST request, we have put our credentials and we got a 302 response.

<img width="900" height="370" alt="image" src="https://github.com/user-attachments/assets/01fa1674-2376-4f2b-ae73-14e3d32b096b" />

Here the page is redirected to my-account and in id parameter there is weiner. 

Lets move this traffic to Repeater

Lets change the parameter to admin and check if we can access admin panel

<img width="900" height="479" alt="image" src="https://github.com/user-attachments/assets/ddd8a430-2f90-4ae8-9607-6825b1f4ecca" />

We got a 302 response. Let follow redirection.

<img width="900" height="434" alt="image" src="https://github.com/user-attachments/assets/822f206e-55b9-4915-b060-27765d6869f1" />

And we re-directed to login page. It means if we put ID other than the one which is assigned to the session cookie, it will just redirect to the login page. So this id parameter is not vulnerable.

<img width="856" height="420" alt="image" src="https://github.com/user-attachments/assets/a0e1ba5b-1303-4038-bc42-17952567fcb1" />

Now, lets put any email address and check how application behaves

<img width="900" height="439" alt="image" src="https://github.com/user-attachments/assets/51a9a6e4-339e-4795-b345-d65df09a2d96" />

Lets move this traffic to Repeater

<img width="900" height="400" alt="image" src="https://github.com/user-attachments/assets/4ad70e51-51ea-448c-bd4b-8a3e9cf98051" />

Now, as per lab description, /admin is only accessible to to logged-in users with a roleid of 2.

Lets add roleid in the body of the request and forward the traffic

<img width="900" height="398" alt="image" src="https://github.com/user-attachments/assets/6382e337-4fba-4542-963a-246c63351f15" />

We got a 302 response and roleid changed to 2.

Lets reload the page

<img width="900" height="218" alt="image" src="https://github.com/user-attachments/assets/c41939c3-6d56-4a70-a149-ce5e83a8a650" />

And now we have admin panel because our roleid is 2 now.

<img width="900" height="251" alt="image" src="https://github.com/user-attachments/assets/e4ee37ae-15b8-48bd-9243-3b33047770ef" />

To solve the lab, lets delete the user carlos

<img width="900" height="295" alt="image" src="https://github.com/user-attachments/assets/fac009b8-6483-4670-9211-441f1828b2af" />

And lab is solved















