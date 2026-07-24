**LFI || Lab#6 || File path traversal, validation of file extension with null byte bypass**

<img width="776" height="342" alt="image" src="https://github.com/user-attachments/assets/108f5a89-fe45-4f63-8c5f-f2b2d52a53fb" />

Goal of this lab is to retrieve the contents of the /etc/passwd file.

Lets start the lab

<img width="920" height="627" alt="image" src="https://github.com/user-attachments/assets/66065c7a-3d68-4e6a-9a23-002a5e3d1a29" />

Lets intercept the traffic in Burpsuite

<img width="1100" height="338" alt="image" src="https://github.com/user-attachments/assets/67529f84-ce47-4124-ac8b-783a494f5a9c" />

Lets move one traffic to Repeater

<img width="1100" height="452" alt="image" src="https://github.com/user-attachments/assets/d1c30b27-c8b8-4a7d-bd5b-677bd7b3a8db" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 20.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

Now, lets try to use the absolute path first /etc/passwd

<img width="1032" height="292" alt="image" src="https://github.com/user-attachments/assets/b7a4b653-7ebc-4528-a2e7-b025fcc83079" />

We got an error, lets try ../../../etc/passwd

<img width="1011" height="277" alt="image" src="https://github.com/user-attachments/assets/5cc96a78-3c79-4aea-bc1f-10a1ed7b2636" />

Again we got an error

Lets double encode the URL and check

<img width="1100" height="319" alt="image" src="https://github.com/user-attachments/assets/1660534d-34e7-4642-b85e-eb21275c4c73" />

Again we got an error.

Now, lets add a null byte %00 and try again

<img width="1066" height="417" alt="image" src="https://github.com/user-attachments/assets/39b4bb55-a98f-4e86-9836-3be70edefdc6" />

We and got /etc/passwd file

GET /image?filename=../../../etc/passwd%0020.jp

Some applications append a fixed extension (like .jpg) to whatever filename you supply.

If you send ../../../etc/passwd, the app tries to open /etc/passwd.jpg → which doesn’t exist.

By using null bytes (%00) we asked application to ignore everything after the null byte.

So, application interpreted /etc/passwd%00.jpg as /etc/passwd and it showed the content of /passwd file.

Lab is solved

<img width="1100" height="422" alt="image" src="https://github.com/user-attachments/assets/4931e9c5-689a-40a5-864e-64737f0a16db" />



