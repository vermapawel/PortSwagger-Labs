**File upload vulnerabilities || Lab#3 || Web shell upload via path traversal**

<img width="776" height="365" alt="image" src="https://github.com/user-attachments/assets/d87b79c1-1b08-49b7-8c8a-5544b5c687ea" />

Goal of this lab is to exploit the file upload vulnerability to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab

<img width="1085" height="407" alt="image" src="https://github.com/user-attachments/assets/31470205-a85b-4285-932d-2592de3f64d0" />

Lets login with the credentials that we have wiener || peter

<img width="812" height="472" alt="image" src="https://github.com/user-attachments/assets/90839563-49ac-4af9-8b3e-4504d6d992d3" />

There is an option to upload a file. Lets try to upload the same php file that we used in last lab

<img width="702" height="470" alt="image" src="https://github.com/user-attachments/assets/e9e7255e-a7ba-446b-8365-9d88b46c6093" />

<img width="1005" height="202" alt="image" src="https://github.com/user-attachments/assets/65794de3-0ad5-463c-a1ae-3164632672f0" />

File have been uploaded successfully. Let check

<img width="822" height="462" alt="image" src="https://github.com/user-attachments/assets/c3400e96-9530-4767-91d5-1e3e548fae72" />

We can see one broken image, means php file is here. Lets open this file in a new tab

<img width="1027" height="192" alt="image" src="https://github.com/user-attachments/assets/57f8e15f-a439-4f18-ab55-46b05022c0f9" />

This time the application is just display the content of the php file.

Lets check the traffic in Burpsuit

<img width="982" height="167" alt="image" src="https://github.com/user-attachments/assets/64e2aec1-a204-4c0a-ba47-4a1565276448" />

Let move this traffic to repeater

<img width="1100" height="347" alt="image" src="https://github.com/user-attachments/assets/f6a2e4e4-7390-48c1-ab2d-0fda05fdc9f8" />

Now, lets try to execute some command

<img width="1100" height="423" alt="image" src="https://github.com/user-attachments/assets/4847d7d7-1d8e-4c12-8d60-7806e1250d06" />

We are not getting output of the command.

The application allows to upload any file but it does not allow to execute any command in /files/avatars directory.

So we need to find any other directory where we can upload the .php file and execute it.

Lets check that traffic on Burp suite where we have uploaded the file

<img width="1100" height="128" alt="image" src="https://github.com/user-attachments/assets/fe643f11-bcb9-4315-8f3c-bd92a767113e" />

Lets move this traffic to repeater

<img width="1100" height="405" alt="image" src="https://github.com/user-attachments/assets/c05057a2-ae77-46de-9312-c6badf21e9d6" />

Here we can see that file is uploaded in avatars folder.

Let upload the file one folder behind the avatars folder.

filename=”../phpfile.php”

<img width="1100" height="321" alt="image" src="https://github.com/user-attachments/assets/de8ff291-65e6-4ca2-86f1-a62448922610" />

File is still getting uploaded in avatars folder. Lets URL encode / and try again.

<img width="1100" height="333" alt="image" src="https://github.com/user-attachments/assets/e07d8555-b9d8-4391-83d6-5e58b288c6d5" />

This time php file is uploaded in one directory above avatars directory which is file directory.

Lets test

<img width="1100" height="427" alt="image" src="https://github.com/user-attachments/assets/f23eec92-5bdd-486f-b390-cb35fc78d631" />

In the request, we have removed the avatars directory. Our php file was uploaded here. We got the output of ID command.

Now, lets get the output of /home/carlos/secret

GET /files/phpfile.php?cmd=cat /home/carlos/secret

URL encode and forward the traffic.

<img width="1100" height="320" alt="image" src="https://github.com/user-attachments/assets/e8759833-377a-482c-ad83-b6b1327837d8" />

And we got the secret key. Lets submit it.

<img width="1037" height="345" alt="image" src="https://github.com/user-attachments/assets/7078ef58-b180-4f82-9e2d-2671664ad6d6" />

<img width="852" height="242" alt="image" src="https://github.com/user-attachments/assets/3a9b6532-4d3f-4226-842a-cfc6bbbd49a4" />

And our lab is solved.






