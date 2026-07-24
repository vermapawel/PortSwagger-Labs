**LFI || Lab#1 || File path traversal, simple case**

<img width="782" height="376" alt="image" src="https://github.com/user-attachments/assets/104de962-d90e-4398-bed0-a40ec992dc9a" />

Goal of this Lab is to retrieve the contents of the /etc/passwd file.

<img width="1100" height="687" alt="image" src="https://github.com/user-attachments/assets/3f6fef9a-6f8b-4f81-bb9a-572eb2843b84" />

Lets intercept the traffic in Burpsuite

<img width="1042" height="526" alt="image" src="https://github.com/user-attachments/assets/34e8d697-311a-4c47-827b-adc4f82bddd1" />

We can see lots of .jpg files. It seems these files are stored in /image folder of the application. Here parameter is filename that is fetching the images.

Lets move one traffic to Repeater

<img width="1100" height="491" alt="image" src="https://github.com/user-attachments/assets/fe8f1dcb-28bc-458a-a761-3ed135140e79" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 16.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

Now, lets check the absolute path

<img width="1100" height="443" alt="image" src="https://github.com/user-attachments/assets/eae599be-224b-4824-80f6-467434448d3c" />

We got a 400 error. No such file.

Lets try to move back in the directories

<img width="1026" height="442" alt="image" src="https://github.com/user-attachments/assets/5397fe1f-6905-4a17-9574-4a6a236daae1" />

We again got a 400 error. No such file.

Lets try to move one more folder back.

<img width="1062" height="452" alt="image" src="https://github.com/user-attachments/assets/78a8b19c-4dc3-48ec-b934-aa1e0343c5fc" />

This time we got the output of /etc/passwd file.

So that path is ../../../etc/passwd

Most probably directory structure is /var/ww/images/16.jpg

When we add ../ it will move back to one directory.

We have added ../../../etc/passwd, so it will move three directories back which should be root directory and in root directory passwd file is present inside /etc.

Lab is solved.

<img width="1100" height="314" alt="image" src="https://github.com/user-attachments/assets/5e4c0938-992b-4b44-b74a-46ddff7df973" />

