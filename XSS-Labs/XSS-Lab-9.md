**XSS || Lab #9 Reflected XSS into a JavaScript string with angle brackets HTML encoded**

<img width="720" height="408" alt="image" src="https://github.com/user-attachments/assets/05a21548-6254-47dd-97c5-625f720119e1" />

End Goal of this lab is to perform XSS attack to call alert function.

Lets access the Lab

<img width="640" height="452" alt="image" src="https://github.com/user-attachments/assets/6d99ce28-246d-499c-b3b6-a121bcc6f517" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

There is a search parameter in the application. Lets check

<img width="640" height="356" alt="image" src="https://github.com/user-attachments/assets/99b01c10-89a4-4b38-908a-d3d5582fbb6f" />

We can see that our string got reflected back on the application. It may be reflected at some other part of the code that is not visible here.

Lets intercept the traffic with Burp suite

<img width="640" height="285" alt="image" src="https://github.com/user-attachments/assets/9592b17f-f272-432b-a687-a113844e2720" />

We can see that out string appears at two places. 1st in the &lt;h1&gt; header which we saw in the application itself. 2nd one is in a <script> tag.

There is a variable called searchTerms which has the string. And then searchTerms is being processed in the JavaScript.

So there are two locations where we need to check if the application is vulnerable to XSS.

Lets check one by one.

Lets search <

<img width="640" height="249" alt="image" src="https://github.com/user-attachments/assets/1e5a9eb6-c8db-4eba-ab7e-d0dfa4e80030" />

Lets check at Burp suite

<img width="640" height="257" alt="image" src="https://github.com/user-attachments/assets/a3228d81-9064-4f48-ab5a-020596e34c2d" />

It seems that the < is encoded at first location, so we cannot use search parameter as XSS attach.

On the 2nd location, it also encoded.

<img width="640" height="328" alt="image" src="https://github.com/user-attachments/assets/0c7a15e7-e6dc-4478-8705-dec2aae3b392" />

Now, as this is in JavaScript inside a tag, we might be able to break it.

var searchTerms = ‘&lt;’;

Lets create the payload

var searchTerms = ‘’;alert(1);’’;

We are adding ‘ to close the 1st ‘ and then ; will indicate the end of the line. Then we put the alert(1) with ; and then ‘ so that there is no syntax error

<img width="640" height="249" alt="image" src="https://github.com/user-attachments/assets/5b61b4a1-4538-4a56-82f4-60b1705279e2" />

So our payload is ’;alert(1);’ Lets search it on search parameter.

<img width="640" height="301" alt="image" src="https://github.com/user-attachments/assets/9bd54d02-0561-4d5b-9b16-4ec1d33f2d06" />

We got an alert with message 1.

<img width="640" height="217" alt="image" src="https://github.com/user-attachments/assets/f2b056a2-d041-40dd-93d0-00ecd8430fc6" />

And our Lab is solved !!!

We can see that our payload is treated as JavaScript code and therefore XSS vulnerability is executed.

<img width="640" height="310" alt="image" src="https://github.com/user-attachments/assets/8dd80749-4ae7-426c-b3db-1549dcd36ccb" />
















