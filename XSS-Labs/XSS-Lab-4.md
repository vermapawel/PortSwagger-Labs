**XSS || Lab #4 DOM XSS in innerHTML sink using source location.search**

<img width="720" height="450" alt="image" src="https://github.com/user-attachments/assets/273cfc27-d45d-4c5a-a2ed-2d0acfcfd95a" />

Goal of this lab is to perform XSS attack to call the alert function.

Lets start the lab

<img width="640" height="382" alt="image" src="https://github.com/user-attachments/assets/69062d0f-a59b-40e8-b60c-3d0094bef839" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

Lets put a string in Search parameter and check.

<img width="640" height="271" alt="image" src="https://github.com/user-attachments/assets/d4d2791d-c76b-4d04-8085-546ae8632abe" />

We can see that the string that we have put got reflected back. So this parameter could be vulnerable to XSS.

Lets check the Developer tool to understand better

Right Click → Inspect

We need to check if any other location this string is getting stored or not.

<img width="640" height="328" alt="image" src="https://github.com/user-attachments/assets/24d632b0-7ccf-4104-88e4-911198f32ae1" />

We can see that our string is stored only in one location which is span element.

Now lets check the source code of the application and check if any JavaScript that is generating this span element.

<img width="640" height="160" alt="image" src="https://github.com/user-attachments/assets/ddc7f7c9-dee4-4ea9-804e-4b6475fc78d4" />

In this code, there is a variable called **query** that takes the input that we put in the search parameter.

If the query parameter is not empty, doSearchQuery() function will be executed. This function take element that has element ID searchMessage and it uses innerHTML to populate the value that search parameter has.

Here we can see that user controllable input that change the Document Objct Model. So whatever this search field has, it being used to change the content of the page hence its looks like its vulnerable to DOM based XSS.

To confirm we need to break out of the **Span** element

<img width="640" height="258" alt="image" src="https://github.com/user-attachments/assets/ab66bb70-a800-4954-85f6-3374b775a65b" />

<span id=”searchMessage”>12345</span>

So if we want to create a XSS payload that alerts a user with a random string, we can create an image element and say the source =1 (could be anything) and when it does not find the source, it will display an error with in the form of an alert

&lt;span id="searchMessage"&gt;&lt;img src=1 onerror=alert(1)&gt;&lt;/span&gt;

So our payload is ***&lt;img src=1 onerror=alert(1)&gt;***

Lets try

<img width="640" height="243" alt="image" src="https://github.com/user-attachments/assets/d122b09d-828f-4363-9ea1-0b71b763cf9f" />

We got a pop-up error alert that displays 1

<img width="640" height="238" alt="image" src="https://github.com/user-attachments/assets/2488a8e5-9c31-4107-90f3-1e86810388d0" />

And the Lab is solved

<img width="640" height="331" alt="image" src="https://github.com/user-attachments/assets/219e19b4-d355-4c68-a65e-a2936e551de5" />

Lets check how the payload interacted with DOM

<img width="640" height="252" alt="image" src="https://github.com/user-attachments/assets/0e75dc9d-ed05-49a2-9318-41ddc2b7a50e" />

Lets take help of Copilot to understand the payload better:-

<img width="640" height="161" alt="image" src="https://github.com/user-attachments/assets/ffa80339-1ec3-4ccd-9202-6cfcf107bb1c" />

<img width="640" height="192" alt="image" src="https://github.com/user-attachments/assets/a2c14cf0-4ce1-4612-9672-1151f0e80a64" />



