**Command Injection || Lab#3 ||Blind OS command injection with output redirection**

<img width="787" height="470" alt="image" src="https://github.com/user-attachments/assets/23b8ac9c-a888-402d-8c79-8cc0df946460" />

To solve the lab, we have to execute the whoami command and retrieve the output

Lets start the lab

<img width="910" height="612" alt="image" src="https://github.com/user-attachments/assets/386cb2fb-977c-4817-b558-1280eb176f9e" />

As per lab description, OS command injection vulnerability is in the feedback function.

<img width="911" height="627" alt="image" src="https://github.com/user-attachments/assets/97f1949b-7ea1-4b2b-a53b-3800b9c860bc" />

Lets intercept the traffic with Burpsuite

<img width="1100" height="299" alt="image" src="https://github.com/user-attachments/assets/bde1c33b-d482-4849-9fb9-3889fdac5696" />

Lets move this traffic to Repeater

<img width="1011" height="415" alt="image" src="https://github.com/user-attachments/assets/d3bb3cfa-1544-4034-9a1f-8bb601f63424" />

Here we have multiple parameters. We have to check one by one.

**Step 1: Finding the vulnerable parameter.**

Like in last lab, lets check delay in each parameter one by one.

Lets start with name parameter.

csrf=VSxbtF024sepgmPTLNhX3YN2m7Il3n6V&name=test&sleep 10 #&email=test%40test.com&subject=test&message=test

Lets URL decode to the payload test&sleep 10 # and forward the traffic.

<img width="1100" height="376" alt="image" src="https://github.com/user-attachments/assets/2120d694-de7c-43a1-878a-c72c29720b70" />

There is no delay of 10 seconds in response, it means name parameter is not vulnerable.

Lets check email parameter

csrf=VSxbtF024sepgmPTLNhX3YN2m7Il3n6V&name=test&email=test%40test.com&sleep 10 # &subject=test&message=test

We will URL encode the payload &sleep 10 # and forward the traffic.

<img width="1100" height="503" alt="image" src="https://github.com/user-attachments/assets/cea3195a-ec30-4734-9d26-a05f3fdbcb28" />

This time there is a delay of 10 seconds in response, it means email parameter is vulnerable to command injection

Step 2:

Lets go to the Home page.

There are multiple traffic for images.

<img width="1100" height="205" alt="image" src="https://github.com/user-attachments/assets/e68870b8-c787-4ad9-92ac-7d5f0af5d4a1" />

These images are stored somewhere on the application.

Lets move one traffic to Repeater.

<img width="1100" height="388" alt="image" src="https://github.com/user-attachments/assets/ade297d8-0cbc-4546-90a5-83c59bb5a18b" />

We understand that these images are stored in images directory.

Directory structure should be like /var/www/image

So if we can write to image folder, we can save the output of the commands that I can run.

Now, the submit traffic, we found that email parameter is vulnerable to command injection.

csrf=VSxbtF024sepgmPTLNhX3YN2m7Il3n6V&name=test&email=test%40test.com&whoami > /var/www/image/file.txt# &subject=test&message=te

In this payload, we are saving the output of whoami to a file called output.txt which will be created in image directory.

Lets URL encode the payload and forward the traffic.

<img width="1100" height="484" alt="image" src="https://github.com/user-attachments/assets/7b658337-754f-414f-809b-83148cc3c151" />

We got a 200 OK response. It means the output of whoami should be stored in a file named file.txt inside image folder.

Lets go to the any of the traffic that is showing an image on the web page.

Now, we have saved the output of whoami in image folder.

Here filename parameter is brining the content of image folder.

<img width="725" height="357" alt="image" src="https://github.com/user-attachments/assets/bf744bfd-158b-46a7-b83b-7970e378976a" />

Lets try to read the content of the output.txt file.

<img width="1100" height="407" alt="image" src="https://github.com/user-attachments/assets/c1846be5-64a5-43b7-8d76-f5e31e45fd6b" />

And we got the username i.e peter

Our lab is solved

<img width="837" height="337" alt="image" src="https://github.com/user-attachments/assets/3494e979-e843-44ff-836c-0b8fe648f3b6" />
