**LFI || Lab#4 || File path traversal, traversal sequences stripped with superfluous URL-decode**

<img width="781" height="380" alt="image" src="https://github.com/user-attachments/assets/9484fb7c-9473-4329-b5a2-12408a089747" />

Goal of this lab is to retrieve the contents of the /etc/passwd file.

Lets start the lab

<img width="927" height="602" alt="image" src="https://github.com/user-attachments/assets/691f9b07-5bbf-4b11-a72d-ac55f70f8ddc" />

Lets intercept the traffic in Burpsuite

<img width="1077" height="327" alt="image" src="https://github.com/user-attachments/assets/34c00b2a-5a5e-4255-955f-046a25a6e643" />

We can see lots of .jpg files. It seems these files are stored in /image folder of the application. Here parameter is filename that is fetching the images.

Lets move one traffic to Repeater

<img width="1100" height="328" alt="image" src="https://github.com/user-attachments/assets/cfa8f838-f126-43cb-aad6-02743cf66931" />

Client is using GET request to fetch any file on the server. Server responded with 200 OK means GET request was successful and it displaying the content of 66.jpg file.

Now, if the application is vulnerable to LFI, we would be able to see other files available on the server.

Please note that LFI will only display those files that are readable by the privileges of the application.

Now, lets try all the previous payloads

absolute path /etc/passwd

<img width="1100" height="284" alt="image" src="https://github.com/user-attachments/assets/336722ec-3e0f-41bf-88da-aa441281a7cd" />

../../../etc/passwd

<img width="1100" height="260" alt="image" src="https://github.com/user-attachments/assets/57b76241-96bd-4f67-bb0b-a4f4914ded5d" />

….//….//….//etc/passwd

<img width="1100" height="291" alt="image" src="https://github.com/user-attachments/assets/30858103-5e15-4b07-b9b4-0786f985346d" />

Non of previous payloads are working

Now, lets encode the ../../../etc/passwd

Select the payload and right click

<img width="1100" height="766" alt="image" src="https://github.com/user-attachments/assets/c36e4a2a-d647-4aa9-9024-503bb6bb28e9" />

Payload is encoded but still it didn’t worked

<img width="1100" height="314" alt="image" src="https://github.com/user-attachments/assets/e1df79d2-2b3e-41a7-89df-14b2d23373b1" />

Now as per lab description, the application is decoding the URL. So when we encode the URL for the 1st time, it decoded as ../../../ and blocked it.

Lets encoded the URL again and try

<img width="1100" height="401" alt="image" src="https://github.com/user-attachments/assets/6825731b-2267-41fb-a410-d328ae559e84" />

And this time we got a 200 OK response and got the content of /etc/passwd

We have encoded the URL twice. So even after if application is decoding the URL one time and looks for ../../../, the payload is still encoded.

So we have tricked the application by encoding the URL twice.

Our lab is solved

<img width="1100" height="505" alt="image" src="https://github.com/user-attachments/assets/7d25d760-646a-4800-a734-689036afc1af" />

