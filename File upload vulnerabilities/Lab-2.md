**File upload vulnerabilities || Lab#2 || Web shell upload via Content-Type restriction bypass**

<img width="787" height="411" alt="image" src="https://github.com/user-attachments/assets/2b507f70-c29e-4a39-9ded-b8dd52e7da4c" />

Goal of this lab is to exploit the file upload vulnerabilitie to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab

<img width="952" height="527" alt="image" src="https://github.com/user-attachments/assets/f7880924-afa8-486b-985d-faa2bb77ad06" />

Lets login with the credentials that we have wiener || peter

<img width="1017" height="656" alt="image" src="https://github.com/user-attachments/assets/b94b99a6-4918-4a78-8f5a-c0ac68f0cbf7" />

There is an option to upload a file. Lets try to upload the same php file that we used in last lab

<img width="742" height="500" alt="image" src="https://github.com/user-attachments/assets/2630b5cb-22c4-4fb0-a19c-ba11ee9005c0" />

<img width="1097" height="217" alt="image" src="https://github.com/user-attachments/assets/a2c43baf-57e8-4dea-b4c5-6c0b6578514e" />

But this time we got an error. Content type application/octet-stream is not allowed.

It seems we can only upload .jpeg and .png file.

Lets check this traffic in Burp suite.

<img width="1100" height="206" alt="image" src="https://github.com/user-attachments/assets/94c8c53f-ff76-4a82-9e83-7c342b5bf4b8" />

This is the POST request. Lets move this traffic to repeater

<img width="1100" height="440" alt="image" src="https://github.com/user-attachments/assets/b89f6175-fe56-44e6-a520-f9d5f738efaf" />

Here we can see that Content-Type: **application/octet-stream**

Lets try to change the Content-Type to image/png which is allowed

<img width="1100" height="367" alt="image" src="https://github.com/user-attachments/assets/cb8cb0b6-da30-44de-8f18-f87f44804fee" />

Lets forward this traffic and we got a 200 OK response. Means this traffic is allowed and php file have been uploaded.

Lets check

<img width="857" height="472" alt="image" src="https://github.com/user-attachments/assets/f8f6a83b-4f7d-4ad4-8f66-840518bea9a1" />

We can see one broken image, means php file is here. Lets open this file in a new tab

<img width="786" height="552" alt="image" src="https://github.com/user-attachments/assets/cf24fe88-66ac-4b06-82d2-b574522038c7" />

<img width="1100" height="209" alt="image" src="https://github.com/user-attachments/assets/f05e2089-dbe1-49a2-a6ef-e7491527623e" />

We got the output of whoami.

Now, lets get the output of /home/carlos/secret

cat /home/carlos/secret

<img width="1100" height="156" alt="image" src="https://github.com/user-attachments/assets/dfb9662a-99cf-412e-8a15-b7d094f3fe11" />

Lets copy this and submit

<img width="952" height="332" alt="image" src="https://github.com/user-attachments/assets/525c955f-49ea-4f33-ac99-811651b66aa2" />

And lab is solved

<img width="1100" height="318" alt="image" src="https://github.com/user-attachments/assets/66b8ccdd-458b-40a9-9a7b-215b426914e3" />


















