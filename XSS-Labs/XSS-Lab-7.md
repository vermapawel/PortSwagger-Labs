**XSS || Lab #7 Reflected XSS into attribute with angle brackets HTML-encoded**

<img width="720" height="463" alt="image" src="https://github.com/user-attachments/assets/ad0013a9-5893-46b2-bac7-ad95e877f8c6" />

End goal of this Lab is to perform XSS attack to call the alert function.

Lets start the Lab

<img width="640" height="504" alt="image" src="https://github.com/user-attachments/assets/9f97cdde-93c3-4267-8e96-e66324ec6948" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

There is a search parameter in the application. Lets check

<img width="640" height="273" alt="image" src="https://github.com/user-attachments/assets/6274b986-b843-41ca-83f6-c5415630a4d5" />

We can see that the input got reflected back to the application. Lets check at Burp suite

<img width="640" height="375" alt="image" src="https://github.com/user-attachments/assets/e43d5e90-0cf5-4b30-b3f0-7744c4fa55f8" />

We can see that the string test got reflected back to the &lt;h1&gt; element that is heading. Its also got reflected back in the value attribute of the <input> element.

So, there are two places the string got reflected back, so we need to check these two places for XSS vulnerability.

Lets start with Search functionality

<img width="640" height="259" alt="image" src="https://github.com/user-attachments/assets/855a9ce2-dd4b-4578-b03f-1d809f3e4f85" />

Lets intercept with Burp suite

<img width="640" height="352" alt="image" src="https://github.com/user-attachments/assets/0f56a3ec-193c-45d6-aa8c-ae8726822d3a" />

Our input character < is URL encoded in both locations. It means we cannot use < or > characters for XSS. So it will be difficult to exploit it in the header of the application.

However at the second place, value attribute, we might be able to exploit it.

**name=search value=” ”>**

So we need to put the payload here in such a way that it does not break the JavaScript code.

**name=search value=”” onmouseover=”alert(1)”>**

We have added one double quote that will close the 1st one.

onmouseover is an HTML event attribute that runs JavaScript when the user moves their mouse cursor over an element.onmouseover = “Run this JavaScript when the mouse hovers over this element.”

So our payload is ” onmouseover=”alert(1)

Lets put this payload in the search parameter.

<img width="640" height="359" alt="image" src="https://github.com/user-attachments/assets/4840b4ed-1c0c-45c4-8150-eb321a5354a5" />

We can see that an alert function is called and the lab is solved

<img width="640" height="300" alt="image" src="https://github.com/user-attachments/assets/a01eab1f-5fdb-4975-a175-b74691ee64d9" />














