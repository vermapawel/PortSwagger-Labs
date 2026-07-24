**File upload vulnerabilities || Lab#1 || Remote code execution via web shell upload**

<img width="802" height="367" alt="image" src="https://github.com/user-attachments/assets/02edab4a-755b-43ee-aeb9-02a3607c864c" />

Goal of this lab is to exploit the file upload vulnerability to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab

<img width="1056" height="485" alt="image" src="https://github.com/user-attachments/assets/a24d5ac0-8e38-4356-bdc7-91ad8b4a25f9" />

Lets login with the credentials that we have wiener || peter

<img width="1022" height="646" alt="image" src="https://github.com/user-attachments/assets/586d4293-c558-4609-9740-83aefbe64cb9" />

There is an option to upload any file for Avatar. Lets upload any random .jpg file to validate.

<img width="1007" height="272" alt="image" src="https://github.com/user-attachments/assets/531a9277-b236-438c-83af-54599b226cc9" />

Image has been uploaded. Lets intercept this traffic in Burp suite

<img width="1100" height="115" alt="image" src="https://github.com/user-attachments/assets/d12ce870-91c4-4c17-a5b1-f10e02f4c038" />

Lets move this traffic to Repeater

<img width="1061" height="486" alt="image" src="https://github.com/user-attachments/assets/18038ce7-9816-4996-af0c-e42fb9cc5ea5" />

We can see that the file type is image/jpeg

Now, lets create a php file and try to upload it.

<img width="1100" height="250" alt="image" src="https://github.com/user-attachments/assets/d9067ee6-1856-47db-86d9-6e6c3ed4e43f" />

&lt;?php system($_GET[‘cmd’]);?&gt;

<img width="957" height="592" alt="image" src="https://github.com/user-attachments/assets/40f70733-f9fb-4ae5-a7c3-c0b860181694" />

Lets upload the php file.

<img width="895" height="442" alt="image" src="https://github.com/user-attachments/assets/167425ff-7857-40a5-ab43-a04881f3b9d8" />

<img width="1020" height="197" alt="image" src="https://github.com/user-attachments/assets/bc4093e3-e50e-4023-b80f-71f5fe86da97" />

File has been uploaded

Lets open the file

<img width="897" height="655" alt="image" src="https://github.com/user-attachments/assets/8c9cc551-ed1c-417b-97ce-392900c5fdda" />

As we have uploaded a php script, we can run any command.

<img width="1100" height="196" alt="image" src="https://github.com/user-attachments/assets/f3cdba9e-b55f-44c2-ad1e-5426cb3f3fff" />

We got the output of whoami

Now, lets get the output of /home/carlos/secret

cat /home/carlos/secret

<img width="1100" height="193" alt="image" src="https://github.com/user-attachments/assets/d915e3e9-6a5b-427e-99d9-9f570aef0132" />

Lets copy this and submit

<img width="1072" height="442" alt="image" src="https://github.com/user-attachments/assets/f852e029-492e-4a19-b5c8-bb2d4e647858" />

And lab is solved.

<img width="1100" height="281" alt="image" src="https://github.com/user-attachments/assets/112916f6-9cea-41c5-8b8d-f1ad76b9dac5" />

