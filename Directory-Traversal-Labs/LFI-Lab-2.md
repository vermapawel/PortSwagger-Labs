**LFI || Lab#2 || File path traversal, traversal sequences blocked with absolute path bypass**

<img width="1091" height="565" alt="image" src="https://github.com/user-attachments/assets/dd7ca9f2-537a-41ee-8f1b-e887768fc3e7" />

To solve the lab, retrieve the contents of the /etc/passwd file

Lets start the lab

<img width="810" height="530" alt="image" src="https://github.com/user-attachments/assets/3d617c64-de93-4266-a372-398565ca6380" />

Lets intercept the traffic in Burpsuite

We can see lots of .jpg files. It seems these files are stored in /image folder of the application. Here parameter is filename that is fetching the images.

<img width="1100" height="429" alt="image" src="https://github.com/user-attachments/assets/554bd60f-8348-4a58-bdaf-987ae3486a19" />

Lets move one traffic to Repeater

<img width="1100" height="532" alt="image" src="https://github.com/user-attachments/assets/b04e154c-d9ca-49d1-8d78-ed5c47a59adf" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 9.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

Lets use the same payload that we have used to solve the 1st lab

<img width="1040" height="346" alt="image" src="https://github.com/user-attachments/assets/972bc940-5fad-4622-97cb-fa0469b382da" />

But this time we got 400 error. No such file

Now, this time it may be possible that application restrict these types of request.

Lets try to use the absolute path /etc/passwd

<img width="1082" height="430" alt="image" src="https://github.com/user-attachments/assets/f2dd2792-da0b-4b8c-9e76-f7698868295a" />

And we got the output of /etc/passwd and the lab is solved

<img width="1100" height="476" alt="image" src="https://github.com/user-attachments/assets/28419480-fc91-444a-a567-e05ba00d621a" />

