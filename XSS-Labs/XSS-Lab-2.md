**XSS || Lab #2 Stored XSS into HTML context with nothing encoded**

<img width="720" height="406" alt="image" src="https://github.com/user-attachments/assets/b4a01cde-539b-483e-9d17-983d8eaff3f7" />

Lets access the Lab

For XSS vulnerabilities we are looking for a client supplied input that is reflected or stored in the application and then reflected back to the user.

<img width="640" height="432" alt="image" src="https://github.com/user-attachments/assets/fb4c988a-02a9-4043-bb0b-1074c8fcac98" />

Click on View post.

<img width="640" height="495" alt="image" src="https://github.com/user-attachments/assets/e843418c-2f53-451b-bed4-d60710212f62" />

On the article, we have an option to put a comment and the comment got displayed back to us under comment section.

So if the application is not properly validating input and encoded on output, then it could be vulnerable to Cross-site Scripting.

So we need to put out XSS payload in the field of this port that is vulnerable and then when anyone will visit this post, that payload will be triggered in their browser.

So, Reflected XSS occurs when user input is immediately returned (“reflected”) by the server in the response, without being stored anywhere.

Stored XSS we need to put the payload in the application and it will get stored. And when anyone visit the application, it will get triggred.

<img width="640" height="269" alt="image" src="https://github.com/user-attachments/assets/0b0cc56b-35df-4f09-9d65-505a8c6a9264" />

Now, 1st we need to check if comment functionality is vulnerable to XSS. First we out the proper comment and check which one reflected back to us.

<img width="640" height="448" alt="image" src="https://github.com/user-attachments/assets/92394164-2be0-4287-975d-30bb3b4cd3f6" />

Lets post the comment.

<img width="640" height="213" alt="image" src="https://github.com/user-attachments/assets/3f64ed4d-a233-4ee1-9ab5-8f6589d07240" />

<img width="640" height="149" alt="image" src="https://github.com/user-attachments/assets/1aeafd30-fabb-47a0-9fd0-61be9b3df8d2" />

We can see the comment got reflected back. Also website (http://test.com) also got reflected back. So these two fields could be vulnerable to XSS.

Lets test the comment field first if its vulnerable to XSS.

<img width="640" height="413" alt="image" src="https://github.com/user-attachments/assets/6cc3b127-5413-4b41-b9ee-e694242ad5d9" />

Now, if the input is properly validated and encoded at the backend, the payload will be treated as a string instead of a client-side code.

If we do get an alert, it means it is interacting with the JavaScript and it is being viewed as a JavaScript code therefore it will call the alert function.

Lets post the comment

<img width="640" height="247" alt="image" src="https://github.com/user-attachments/assets/b8ab03fa-0a9f-4c2b-8042-99510674c70f" />

And we can see that Lab is solved. Lets revisit that blog again

<img width="640" height="249" alt="image" src="https://github.com/user-attachments/assets/149c2ca9-5619-47a4-97e4-8faaf2c4008c" />

<img width="640" height="350" alt="image" src="https://github.com/user-attachments/assets/ce70bc58-ee36-4dc1-ba5a-20b7a538bd81" />

We can see that our comment didn't got posted here as the application understand it as the client-side code and it got executed.

Lets check on Burp suite

<img width="640" height="358" alt="image" src="https://github.com/user-attachments/assets/394cebfc-df15-47ca-b55d-2fc83159cd8a" />

This is the traffic (POST). We can see that the alert function is viewed as the client-side code instead of a string.


