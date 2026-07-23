**XSS || Lab #5 DOM XSS in jQuery anchor href attribute sink using location.search source**

<img width="720" height="475" alt="image" src="https://github.com/user-attachments/assets/88429469-0214-4887-a1af-947119ef6191" />

The Goal of this lab is to exploit the XSS vulnerability to make the “back” link alert document.cookie.

Lets start the Lab

<img width="640" height="441" alt="image" src="https://github.com/user-attachments/assets/654de0de-a7d2-48a5-b7a4-dd02c954e08d" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

Lets check Submit Feedback parameter

<img width="640" height="458" alt="image" src="https://github.com/user-attachments/assets/9a9bd819-d8ef-4704-a2cc-7871968ec57d" />

Click on Submit feedback

<img width="640" height="560" alt="image" src="https://github.com/user-attachments/assets/3026bb57-2c23-4f41-8511-1a0fa493a13f" />

However we don't see any reflected messages that we have put as inputs

We can confirm that by checking Developers tool

<img width="640" height="284" alt="image" src="https://github.com/user-attachments/assets/76d4ff0b-d675-4c69-b352-26bbc6aa82ba" />

Here we don't find any input stored in the application.

So it seems that the Submit feedback fields are not vulnerable to XSS.

Lets check the source code to find any JavaScript that is writing to the Document Object Model.

On the source code there is some JavaScript that is specifically to the ID backLink

<img width="640" height="132" alt="image" src="https://github.com/user-attachments/assets/87b62230-69c4-4df9-a838-6876dbd166a9" />

This id backLink is for the Back button

<img width="640" height="447" alt="image" src="https://github.com/user-attachments/assets/78e99bda-4c2e-48e6-a2a6-b5c657451574" />

The javascript is applied on the Back button

<img width="640" height="126" alt="image" src="https://github.com/user-attachments/assets/93a9ded6-6072-447e-96ef-7da287c0282e" />

Now the attribute href of the element ID backLink is getting its value from returnPath.

Lets check where this returnPath is

<img width="640" height="90" alt="image" src="https://github.com/user-attachments/assets/66909ae1-c32e-45cf-9f07-cc429397bd02" />

The return path is equal to whatever is set in the URL.

The URL input is user controllable so anything we put after the = will get added as the backLink.

In the real word an attacker can add a malicious website after = and he will be redirected to that website. Or an attacker can execute JavaScript in the user’s browser.

As we can control the value in the URL, we will add a malicious JavaScript code that outputs the users cookies and then when this application runs, it will enter that code in returnPath and it will be saved in the href of the Back button (backLink). So everything someone clicks the Back button, the JavaScript code will get executed.

Now, to solve the Lab we need to generate an alert on document.cookie.

Lets create the payload

***javascript:alert(document.cookie)***

Now we need to put this payload on the URL and hit enter

<img width="640" height="391" alt="image" src="https://github.com/user-attachments/assets/444cf9c6-a495-457c-9133-2182948b17d0" />

<img width="640" height="484" alt="image" src="https://github.com/user-attachments/assets/ac34bc5f-f931-402d-ab78-06aab81c443c" />

We can see that the Lab is solved.

So the payload that we have created is stored on the Back button. So every time when someone clicks the Back button, the payload will execute and it will display in the form of alert the cookie used by this application.

Lets click the back button at the bottom.

<img width="640" height="342" alt="image" src="https://github.com/user-attachments/assets/44b4a975-45ca-4d65-9eb6-f951bbd777d7" />

Since we have not logged in the application and therefore there is not cookie, in the real world, cookie will be displayed.
