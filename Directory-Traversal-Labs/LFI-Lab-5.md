**LFI || Lab#5 || File path traversal, validation of start of path**

<img width="782" height="347" alt="image" src="https://github.com/user-attachments/assets/773c428c-a852-4d18-8827-d935f2cc9879" />

Goal of this lab is to retrieve the contents of the /etc/passwd file.

Lets start the lab

<img width="1100" height="586" alt="image" src="https://github.com/user-attachments/assets/622e80b0-d07e-4f69-979a-0dfb513d97bc" />

Lets intercept the traffic in Burpsuite

<img width="1100" height="336" alt="image" src="https://github.com/user-attachments/assets/973c43d9-ec8c-4d93-a3f4-638fc35aedda" />

Lets move one traffic to Repeater

<img width="1100" height="448" alt="image" src="https://github.com/user-attachments/assets/db359e71-7fc6-40ef-9fa5-83b6853a01aa" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 73.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

In this capture we can see the directory structure where images are stored

/var/www/images/73.jpg

Lets try to put absolute path for passwd file

<img width="1097" height="362" alt="image" src="https://github.com/user-attachments/assets/590aa0e3-d7d1-4608-85e3-9a506a514f6f" />

We got a 400 error. “Missing parameter ‘filename’ ”

It seems that the application requires to start the path from /var/www/images. So we have put our payload after this path.

Lets put the payload after /var/www/images

<img width="1080" height="465" alt="image" src="https://github.com/user-attachments/assets/fbfe0f89-76da-4f66-9fcf-aea4623fffd8" />

And we got the /etc/passwd file

<img width="817" height="545" alt="image" src="https://github.com/user-attachments/assets/77189322-7460-409c-b300-78bd2f994f5a" />

<img width="942" height="272" alt="image" src="https://github.com/user-attachments/assets/5c178e5d-02d7-46cc-bb79-be7432675237" />

Lab is solved

<img width="1100" height="409" alt="image" src="https://github.com/user-attachments/assets/9ba133a9-7135-4938-bf75-b3c5aa09e4d0" />

