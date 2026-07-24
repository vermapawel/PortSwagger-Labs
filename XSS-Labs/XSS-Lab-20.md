**XSS || Lab #20 Reflected XSS in canonical link tag**

<img width="850" height="613" alt="image" src="https://github.com/user-attachments/assets/a114268d-7bc5-47fe-ba5d-f38a20849dce" />

Goal of this Lab is to perform a cross-site scripting attack on the home page that injects an attribute that calls the alert function when user users the key combinations.

Lets start the lab

<img width="880" height="652" alt="image" src="https://github.com/user-attachments/assets/bb63a4b5-5661-4e1b-af60-24e745ddc4c2" />

Now in this case we have tested the application and don't find any parameter that is reflected back to us and is vulnerable to XSS.

In that case we will check if the URL accepts random parameters.

<img width="1100" height="534" alt="image" src="https://github.com/user-attachments/assets/4bac0d7a-28f5-445b-a2ca-ba49921d1c60" />

Now we still dont see test getting reflected back to us.

<img width="906" height="610" alt="image" src="https://github.com/user-attachments/assets/b671105d-f5f9-4716-bcfa-476b02cf767b" />

Lets check the source code if we find any location where our input got stored.

<img width="1100" height="251" alt="image" src="https://github.com/user-attachments/assets/a573dfd7-37e7-472d-8796-be1fe0a14743" />

Now we will check if this link is vulnerable to XSS

&lt;link rel=&rdquo;canonical&rdquo; href=&rsquo;https://0aa6000904d4bfd280a117e000d70098.web-security-academy.net/?random=test&rsquo;/&gt;

Lets add an attribute onclick that generate an alert

&lt;link rel=”canonical” href=’https://0aa6000904d4bfd280a117e000d70098.web-security-academy.net/?random=test’ onclick=’alert(1)

<img width="1100" height="267" alt="image" src="https://github.com/user-attachments/assets/25788227-654b-4712-92e9-88af5ccd87e7" />

We can see that the space between test’ and onclick got URL encoded.

We need to find a way to allow space in the payload. We can use URL encode of Tab key

Lets google URL encode for Tab

<img width="718" height="159" alt="image" src="https://github.com/user-attachments/assets/557f5799-c002-488b-b877-2adaa6436cbc" />

For horizontal tab its %09. Lets try this

&lt;link rel=”canonical” href=’https://0aa6000904d4bfd280a117e000d70098.web-security-academy.net/?random=test’%09onclick=’alert(1)

Lets put this in the URL

<img width="1100" height="309" alt="image" src="https://github.com/user-attachments/assets/045ee5bb-93ff-4ee0-abf0-d46d67bf6283" />

And now we can see that we have a space and oneclick element is applied.

Now, This link is not displayed on the Application page so that user can click on it and alert get generated.

That’s why in the description of the Lab is said that user will press certain keys to trigger the exploit.

<img width="1008" height="304" alt="image" src="https://github.com/user-attachments/assets/f3b66482-bc27-42c3-9534-8290c222666e" />

Now, in all of the keys combination, X is common.

So we will set an access key that will trigger the payload. accesskey is an HTML global attribute that assigns a keyboard shortcut to an element.
When pressed, the shortcut gives focus to that element or activates it

&lt;link rel=”canonical” href=’https://0aa6000904d4bfd280a117e000d70098.web-security-academy.net/?random=test’%09onclick=’alert(1)’%09accesskey=’x’

<img width="1100" height="265" alt="image" src="https://github.com/user-attachments/assets/2fe85887-8078-4664-9e2b-93c2a7927841" />

Now our oneclick and accesskey are set. Now remove view-source and hit Enter key.

<img width="1100" height="116" alt="image" src="https://github.com/user-attachments/assets/b354a5b7-290a-421c-b428-0b010c5395be" />

And Lab is solved !!!

<img width="1100" height="320" alt="image" src="https://github.com/user-attachments/assets/adf23c29-f11c-456c-9974-664fb21f5b75" />







