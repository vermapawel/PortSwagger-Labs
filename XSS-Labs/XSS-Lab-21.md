**XSS || Lab #21 Reflected XSS into a JavaScript string with single quote and backslash escaped**

<img width="844" height="520" alt="image" src="https://github.com/user-attachments/assets/a8affc2a-d992-4582-8286-dc309187dcdd" />

The goal of this Lab is to perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

Lets start the Lab

<img width="1092" height="460" alt="image" src="https://github.com/user-attachments/assets/0515e045-f7e3-481e-931f-9580e2dc45c2" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

We have a search parameter in the application. Lets check

<img width="937" height="354" alt="image" src="https://github.com/user-attachments/assets/8d3d3cec-b538-4c60-8c1c-a91cbb53d967" />

We can see that the string that we have put in the search parameter got reflected back. So this search parameter needs to check if it has XSS vulnerability.

Lets check if this input is stored somewhere else in the source code.

<img width="1100" height="346" alt="image" src="https://github.com/user-attachments/assets/1b91f309-ed75-4e37-b882-02174c3519ad" />

We can see that our input test is stored in two places. 1st is in &lt;h1&gt; tag which is the heading. 2nd location is in </script> tag.

We need to test both these places if they are vulnerable to XSS

Lets put a <script> tag and see how the application behaves

<img width="1100" height="390" alt="image" src="https://github.com/user-attachments/assets/c89f8f19-304f-4316-ad53-7191f81bc4a0" />

Lets check the source code

<img width="1100" height="273" alt="image" src="https://github.com/user-attachments/assets/33b632c2-d333-463a-a474-fc39b7a47d33" />

Now, in the &lt;h1&gt; tag its the < and > are URL encoded. However in the <script> tag they are not URL encoded.

So we will focus on the <script> tag

Now 1st thing we will try is to break out of the string using a single quote ‘

<img width="1100" height="250" alt="image" src="https://github.com/user-attachments/assets/aa96dd9b-2bb8-4a12-b341-24c15f5b0761" />

<img width="1100" height="83" alt="image" src="https://github.com/user-attachments/assets/296b7df2-546a-4db0-a4ca-6e32a06d6280" />

We can see that our single quote got commented out using back slash \, so we cannot use ‘

Next we will try to break out from <script> tag

<img width="1100" height="204" alt="image" src="https://github.com/user-attachments/assets/376916fd-1758-4969-883e-7495ff65e7a6" />

<img width="1100" height="100" alt="image" src="https://github.com/user-attachments/assets/c239855c-9cee-460b-8f66-012dc27dfec3" />

So have break out from the <script> tag. Now we can add our exploit here

&lt;/script&gt;&lt;script&gt;alert(1)&lt;/script&gt;

<img width="960" height="391" alt="image" src="https://github.com/user-attachments/assets/6216439a-6a2b-424a-86ed-26dfc42d4dad" />

We got an alert in the form of Pop-up message

<img width="984" height="366" alt="image" src="https://github.com/user-attachments/assets/475f873a-dc80-4bb6-8bfc-25e4a5389c2b" />

And the Lab is solved !!!

<img width="1100" height="356" alt="image" src="https://github.com/user-attachments/assets/830e5548-ca6c-4b5a-b620-efb564176432" />
