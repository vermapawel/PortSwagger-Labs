**XSS || Lab #13 Stored DOM XSS**

<img width="843" height="432" alt="image" src="https://github.com/user-attachments/assets/1c6cad66-6425-4684-9864-aba36e9b82e7" />

Goal of this Lab is to perform DOM XSS attack in the blog comment section to call alert() function.

Lets start the lab

<img width="1100" height="743" alt="image" src="https://github.com/user-attachments/assets/19b27659-adf1-4595-bed5-954fdf79524d" />

On the comment section there are some fields to take the data from the user

<img width="885" height="688" alt="image" src="https://github.com/user-attachments/assets/ed9afeb9-1fc6-41df-999b-3fa6d7c716ac" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

Lets put some strings in the data field.

<img width="930" height="696" alt="image" src="https://github.com/user-attachments/assets/5a660786-4f06-4638-b00f-e03e7a1247c9" />

<img width="1100" height="395" alt="image" src="https://github.com/user-attachments/assets/282a6a96-b173-4836-9668-dcb07ee2c117" />

We can see that Name and comment field are reflecting the data that we have entered. So we need to check these two fields if there is any XSS vulnerability.

Lets check Developers tool

<img width="841" height="292" alt="image" src="https://github.com/user-attachments/assets/d40114c6-4d01-418f-b78a-7d96936e36e2" />

We can see that our comment got added under &lt;p&gt;

&lt;p&gt;test&lt;/p&gt; is the comment and the author name is added under href which is not directly visible in the application itself.

<img width="847" height="193" alt="image" src="https://github.com/user-attachments/assets/7db83d2b-392b-486f-9f4a-09cc64dbaec5" />

Now, one thing we noticed that there is a custom <script> tag that calls one .js file.

Lets check that file.

<img width="1100" height="528" alt="image" src="https://github.com/user-attachments/assets/bb3d31ce-deab-48f6-8d75-fbd84e9294d8" />

In the source code, a function is used called escapeHTML for comment, author and all other section of the user input field.

Lets check what this escapeHTML function dose.

<img width="823" height="108" alt="image" src="https://github.com/user-attachments/assets/e476e88b-cd96-4853-b024-60032e30a053" />

escapeHTML function replaces < and > sigh with the URL encoded versions of these signs &lt and &gt to filter the input.

However, it filters only 1st instance of the string and not all the instances.

Lets test

<img width="855" height="667" alt="image" src="https://github.com/user-attachments/assets/5462a84f-7d98-4448-8382-66210b276283" />

<img width="945" height="444" alt="image" src="https://github.com/user-attachments/assets/2b54a572-7f32-41a7-9932-e06dfbbb0cfd" />

We can see that only 1st < and > got URL encoded, thats why it get posted as comment and &lt;test&gt; is treated as code of the JavaScript. Its not got URL encoded.

<img width="858" height="300" alt="image" src="https://github.com/user-attachments/assets/f2383f10-4a11-4b60-8ec3-8383dbeec94d" />

<> is under &lt;p&gt; which is for comment but &lt;test&gt;&lt;/test&gt; is read as code.

So this is vulnerable to XSS.

Lets create the payload

&lt;&gt;&lt;img src=1 onerror=alert(1)&gt;

The 1st < and > will be URL encoded but the rest part will be treated as JavaScript code and it will generate an alert.

<img width="862" height="670" alt="image" src="https://github.com/user-attachments/assets/b6a92e6d-5d0f-4928-aafc-434be3d76ac7" />

<img width="1100" height="351" alt="image" src="https://github.com/user-attachments/assets/8700c610-8849-4c1c-84b5-1c5272c28535" />

<img width="1100" height="506" alt="image" src="https://github.com/user-attachments/assets/a967b321-3b24-40e6-bcdf-0e5c774c89c3" />

We got an alert pop-up which display1.

<img width="1100" height="253" alt="image" src="https://github.com/user-attachments/assets/439da11c-f2b2-4b6f-9b32-4c1f93b8b67c" />

And Lab is solved !!



