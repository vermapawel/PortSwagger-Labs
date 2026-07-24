**LFI || Lab#3 || File path traversal, traversal sequences stripped non-recursively**

<img width="772" height="360" alt="image" src="https://github.com/user-attachments/assets/30ac4147-29b6-4ce9-96fb-86b1b4cbe925" />

Goal of this lab is to retrieve the contents of the /etc/passwd file.

Lets open the lab

<img width="832" height="661" alt="image" src="https://github.com/user-attachments/assets/17c3069f-b818-4c87-86ca-c04751a92251" />

Lets intercept the traffic in Burpsuite

We can see lots of .jpg files. It seems these files are stored in /image folder of the application. Here parameter is filename that is fetching the images.

<img width="1100" height="380" alt="image" src="https://github.com/user-attachments/assets/5d409c98-2ee6-46da-982c-fab61e2ec28f" />

Lets move one traffic to Repeater

<img width="1077" height="437" alt="image" src="https://github.com/user-attachments/assets/cedb8c3e-b7b1-4746-8cc5-390590967c32" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 7.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

Lets try absolute path first /etc/passwd

<img width="1086" height="487" alt="image" src="https://github.com/user-attachments/assets/f242ed67-a772-4709-8643-ed04f24d7e0c" />

We got an error.

Lets try path traversal sequence

<img width="1100" height="366" alt="image" src="https://github.com/user-attachments/assets/4cb38eac-6ec5-4807-9f79-d2505d54cbc3" />

Again we got an error.

Now some applications try to block ../ sequences by looking for that exact substring.

Lets use ….//….//….//etc/pass

<img width="1100" height="424" alt="image" src="https://github.com/user-attachments/assets/61a024da-39f9-4bd2-b7a9-fb4d8f0ef118" />

And we got a 200 OK response and content of /etc/passwd

When we use ….//….//….//etc/pass, we tricks the application and it doesnot recognize ….// as ../

But the file system resolves ….// as ../ anyway, because multiple dots and slashes collapse during path normalization and it display the content of /etc/passwd

Lab is solved

<img width="997" height="447" alt="image" src="https://github.com/user-attachments/assets/f975777d-2653-43ea-ba3d-18c9880293bf" />














