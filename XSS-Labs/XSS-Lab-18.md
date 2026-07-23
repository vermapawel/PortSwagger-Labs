**XSS || Lab #18 Reflected XSS into HTML context with all tags blocked except custom ones**

<img width="850" height="511" alt="image" src="https://github.com/user-attachments/assets/34e075f0-e5ec-417c-a1bc-05fd90cf0ae1" />

Goal of this Lab is to perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie.

Lets start the Lab

<img width="1006" height="627" alt="image" src="https://github.com/user-attachments/assets/f8988712-eb0d-45a7-b972-b2348362845c" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

We have a search parameter in the application. Lets check

<img width="1045" height="400" alt="image" src="https://github.com/user-attachments/assets/c7ca3e7e-26e1-4994-ac2a-f127921112a5" />

We can see that the string that we have put in the search parameter got reflected back. So this search parameter needs to check if it has XSS vulnerability.

Lets put a small script and check

<img width="1083" height="390" alt="image" src="https://github.com/user-attachments/assets/2152a212-1144-42e0-926a-4c9cf6815deb" />

<img width="1100" height="409" alt="image" src="https://github.com/user-attachments/assets/e5af52bb-8105-4e0c-aa9f-0706b96abd7a" />

We got an message that this tag is not allowed.

So we need to find out which Tags are allowed.

Lets intercept the traffic is Burp suite

<img width="1100" height="284" alt="image" src="https://github.com/user-attachments/assets/6fa52c2e-53af-4032-9ad3-f6479b571660" />

We will brute force all and check which Tags are allowed. Lets move this traffic to Intruder

<img width="1100" height="381" alt="image" src="https://github.com/user-attachments/assets/6d935ad0-33fe-441c-a27c-ab0d6087ba15" />

We need to add our payload list here

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

<img width="1100" height="586" alt="image" src="https://github.com/user-attachments/assets/320d40d7-84da-4f03-9579-dba361f47f5e" />

We will copy all the tags and put in the payload

<img width="1100" height="457" alt="image" src="https://github.com/user-attachments/assets/cd2ae951-a1f3-467b-aee5-58114836416e" />

Lets start the attack

<img width="1100" height="308" alt="image" src="https://github.com/user-attachments/assets/253a67b6-cfb2-443b-98bd-2f89b72b1b78" />

We get some 200 response means these tags are allowed.

In the lab description it all HTML tags are blocked except custom ones. However we can see that multiple tags has 200 response.

We will solve this lab with custom tags.

Lets go back to the XSS cheat sheet and select custom tags

<img width="1100" height="518" alt="image" src="https://github.com/user-attachments/assets/fff457ac-06a3-4079-8154-136a237bd492" />

It will give lots of payload that we can use.

Lets try onfocus

&lt;xss autofocus tabindex=1 onfocus=console.log("hello")&gt;&lt;/xss&gt;


<img width="1100" height="425" alt="image" src="https://github.com/user-attachments/assets/e207d3c2-ae96-4eb8-b00d-9d51c3da960b" />

The script is not reflected back to the screen. Looks like it works.

<img width="1100" height="289" alt="image" src="https://github.com/user-attachments/assets/a4936940-2917-41c4-98ab-423daf474e5d" />

We can see hello message on the console. So this payload is working.

Now we need to deliver this exploit to the victim user

To solve this lab we need to generate alert document.cookie.

Lets create the payload

&lt;xss autofocus tabindex=1 onfocus=alert(document.cookie)&gt;&lt;/xss&gt;

We need to URL encode it

<img width="1100" height="483" alt="image" src="https://github.com/user-attachments/assets/266dce54-dec3-47a4-9c8c-11a9c4fc31b2" />

<img width="1100" height="337" alt="image" src="https://github.com/user-attachments/assets/c3117fdf-97b4-43f2-a674-4309eaea22c9" />

<img width="1100" height="575" alt="image" src="https://github.com/user-attachments/assets/79032c8b-b961-4fec-9083-d446b2adf45b" />

Lets Deliver exploit to victim

<img width="1100" height="328" alt="image" src="https://github.com/user-attachments/assets/50aee45d-4408-482c-8150-f23cb6e3a7e8" />

And Lab is solved !!!
