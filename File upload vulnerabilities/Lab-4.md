**File upload vulnerabilities || Lab#4 || Web shell upload via extension blacklist bypass**

<img width="772" height="426" alt="image" src="https://github.com/user-attachments/assets/98367f3b-e738-40ad-ae5a-71cf049b18b5" />

Goal of this lab is to exploit the file upload vulnerability to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab

<img width="862" height="667" alt="image" src="https://github.com/user-attachments/assets/205fbf50-7c79-419c-a14a-b8a1497d6b4f" />

Lets login with the credentials that we have wiener || peter

<img width="702" height="507" alt="image" src="https://github.com/user-attachments/assets/faf3db88-9ae6-4cfa-98bf-a984037e4ad7" />

There is an option to upload a file. Lets try to upload the same php file that we used in last lab

<img width="952" height="272" alt="image" src="https://github.com/user-attachments/assets/1a8d81a6-7fd7-41d1-ab4b-2473d2372b6e" />

We got an error that php files are not allowed. Lets move this traffic to repeater.

<img width="1100" height="56" alt="image" src="https://github.com/user-attachments/assets/8e0fcb1b-3fc8-4ffa-9e4b-290999a04fe9" />

<img width="1100" height="333" alt="image" src="https://github.com/user-attachments/assets/2d443989-654f-4ad7-b05d-bfb67e5dc79e" />

If php is blocked, lets check if its accept php3.

<img width="1100" height="354" alt="image" src="https://github.com/user-attachments/assets/7f308a6b-84b1-4385-8828-426a915f420c" />

File have been uploaded. Lets check

<img width="761" height="491" alt="image" src="https://github.com/user-attachments/assets/d949d0e2-7105-4a95-ad86-36c9ee05f43b" />

We can see one broken image, means php file is here. Lets open this file in a new tab

<img width="991" height="142" alt="image" src="https://github.com/user-attachments/assets/bf0e8e34-bd38-4877-a6d4-3cc6318ab103" />

And we can see the content of the file is getting displayed. It means this php3 file is not executable.

We can try other extensions like php4, php5 etc.

Now, lets check if we are able to upload .htaccess file.

<img width="1100" height="384" alt="image" src="https://github.com/user-attachments/assets/348a74ae-d4e7-459c-a78e-744a81912866" />

And we got a 200 OK response and .htaccess file is uploaded.

Now, we know that Apache server is running.

.htaccess file let us configure Apache web server behavior at the directory level without touching the main server config.

So, we want to add a configuration rule to map the php code to a different file extension.

<img width="505" height="141" alt="image" src="https://github.com/user-attachments/assets/d52e9c2b-4305-40b1-a0fa-576856951583" />

We can do that with AddType parameter.

Lets create a new file with name .htaccess.

AddType application/x-httpd-php .phpfile

<img width="1100" height="298" alt="image" src="https://github.com/user-attachments/assets/b3cdb722-95d7-4851-b740-12598cb121d1" />

Now, lets rename our php file to phpfile.phpfile

<img width="1100" height="620" alt="image" src="https://github.com/user-attachments/assets/8423124f-9a77-4602-bae4-50200f662057" />

Now, lets upload .htaccess file first.

<img width="801" height="482" alt="image" src="https://github.com/user-attachments/assets/36effc58-503b-44c2-bf4a-0b5265a5ef86" />

<img width="995" height="197" alt="image" src="https://github.com/user-attachments/assets/e01c613f-1fd9-4ced-8200-48ce73f2cad9" />

File have been uploaded.

Now lets upload the phptest file.

<img width="892" height="511" alt="image" src="https://github.com/user-attachments/assets/9373ff57-5b40-415e-a112-bc08067fdd00" />

<img width="1032" height="150" alt="image" src="https://github.com/user-attachments/assets/ca9f92ad-7360-40ff-8ab2-9f1a42307994" />

And our payload is uploaded. Let check

<img width="816" height="657" alt="image" src="https://github.com/user-attachments/assets/79e581f9-e948-4d86-998c-4d4f11ec3480" />

<img width="1100" height="205" alt="image" src="https://github.com/user-attachments/assets/6fd31e04-1789-4c5a-af8a-12f2a8c016fb" />

Now, lets get the output of /home/carlos/secret

<img width="1100" height="163" alt="image" src="https://github.com/user-attachments/assets/15af3814-3962-4416-8cc4-e76e35eb14df" />

Lets submit this key

<img width="1100" height="402" alt="image" src="https://github.com/user-attachments/assets/e74ea3a3-e93e-4600-bce3-1542d11a5a90" />

And our lab is solved

<img width="1097" height="282" alt="image" src="https://github.com/user-attachments/assets/8c8dc480-0e61-4c8c-b52b-ef357c6b9bad" />












