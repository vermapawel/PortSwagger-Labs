<img width="1100" height="441" alt="image" src="https://github.com/user-attachments/assets/d1e24021-6230-4fff-80c8-b0f20af5ae8e" />**XSS || Lab #11 DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded**

<img width="871" height="634" alt="image" src="https://github.com/user-attachments/assets/b1274a66-8caa-47de-b8ad-8e5026dd8bf6" />

Goal of this lab is to perform DOM based XSS attack to call the alert function.

Lets start the Lab

<img width="1054" height="636" alt="image" src="https://github.com/user-attachments/assets/2d6e344a-ab5c-4d21-8056-3cd2914cca5f" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

There is a search parameter in the application. Lets check

<img width="970" height="454" alt="image" src="https://github.com/user-attachments/assets/1a0356d3-40c7-44e1-85b3-efca285e6d9d" />

<img width="970" height="454" alt="image" src="https://github.com/user-attachments/assets/718a4f7c-5f10-48a0-ab4d-986ffdb69f59" />

We can see that the string that we have put in the search parameter got reflected back.

Now, we need to find where this string got stored.

Lets check Developers tool

<img width="891" height="382" alt="image" src="https://github.com/user-attachments/assets/65a91b3d-a6e0-4e36-a6f9-1d495b1ad9ab" />

So our input is stored only at one place that is in the heading element.

Now, we notice that application is using AngularJS

<img width="843" height="439" alt="image" src="https://github.com/user-attachments/assets/a0419fe4-6386-4ff5-a046-51611626a0eb" />

Now, important thing here to notice is that ng-app is a directive that tells AngularJs that this is the root element of the AngularJS application and the content inside the ng-app element can contain AngularJS code.

Now we need to use the syntax of the AngularJS to perform the attack.

***{{$on.constructor(‘alert(1)’)()}}***

$on is an event handler function in AngularJS and the constructor is a function when called it executes its argument. Here its argument is to call the alert function.

Lets put this payload in the search parameter.

<img width="1100" height="537" alt="image" src="https://github.com/user-attachments/assets/6116bf8c-3d8f-4c19-85cd-ab8cd3e86368" />

We can an alert pop-up.

And the Lab is solved.

<img width="1100" height="441" alt="image" src="https://github.com/user-attachments/assets/81ec63f9-026d-4fae-a764-50910fd4d53f" />





