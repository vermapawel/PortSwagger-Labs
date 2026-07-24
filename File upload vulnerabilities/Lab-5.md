**File upload vulnerabilities || Lab#5 || Web shell upload via obfuscated file extension**

<img width="777" height="372" alt="image" src="https://github.com/user-attachments/assets/e6709c64-55b0-4e61-84c8-1ef4ef5ea6f5" />

Goal of this lab is to exploit the file upload vulnerability to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab and login with the credentials that we have wiener || peter

<img width="702" height="507" alt="image" src="https://github.com/user-attachments/assets/41b08933-6127-4479-ae04-ca0d1d13b429" />

Lets upload the php file and check

<img width="735" height="476" alt="image" src="https://github.com/user-attachments/assets/8f5102f9-120e-43e4-822b-9b02ffe651d6" />

<img width="1057" height="237" alt="image" src="https://github.com/user-attachments/assets/d8c9faaf-4484-4a0b-a28d-bba27a7bcb21" />

We can only upload JPG and PNG file.

Lets intercept this traffic in Burp Suite

<img width="1100" height="79" alt="image" src="https://github.com/user-attachments/assets/a59e7324-f81b-4701-bbaf-6324c80cd830" />

Move this traffic to Repeater

<img width="1047" height="427" alt="image" src="https://github.com/user-attachments/assets/349dd5f5-9570-4607-a1b6-3ce380ab652b" />

Lets us null bite (%00) in the file name to ignore the file extension type

filename=”phpfile.php%00.png”

1st, the application will check the file extension .png. It will allow it to upload. Also, the null bite will ask server to ignore .png and we will left with the php file.

<img width="986" height="457" alt="image" src="https://github.com/user-attachments/assets/97e3fcc4-c8ed-42ba-a17c-a43de014cb4e" />

And our file is uploaded. Lets check

<img width="861" height="557" alt="image" src="https://github.com/user-attachments/assets/3997fca0-15d9-4783-82cb-12778207adb9" />

<img width="1100" height="314" alt="image" src="https://github.com/user-attachments/assets/6bc594a4-5e0c-4afe-9bfb-d1e126fb4ecd" />

Its saying URL is not found on the server. There must be something wrong.

Lets check developers tool

<img width="1100" height="305" alt="image" src="https://github.com/user-attachments/assets/002be4e0-b697-4d76-8c74-7140007be261" />

This is the file upload location. Lets copy the link and put on the browser.

<img width="1100" height="191" alt="image" src="https://github.com/user-attachments/assets/88921cbf-31d1-41b7-9dfe-06a2313aa1f2" />

And now our paylaod is working. Lets execute some commands

<img width="1100" height="176" alt="image" src="https://github.com/user-attachments/assets/c5921984-4a09-4a35-b184-60e63c3418bb" />

Now lets get to output of /home/carlos/secret

<img width="1100" height="254" alt="image" src="https://github.com/user-attachments/assets/f60817f5-698a-49a4-9e3e-0f32aebbbf93" />

Lets submit this key and the lab is solved

<img width="1100" height="280" alt="image" src="https://github.com/user-attachments/assets/5601dbbc-d3f0-464b-9a2d-fc647d6193dc" />






















