**XSS || Lab #17 Reflected XSS into HTML context with most tags and attributes blocked**

<img width="856" height="592" alt="image" src="https://github.com/user-attachments/assets/30327bcd-8e51-4cf8-8954-f6153af16872" />

Goal of this lab is to perform XSS attack to bypass the WAF and call print() function.

Lets start the Lab

<img width="988" height="657" alt="image" src="https://github.com/user-attachments/assets/f6f79554-26ba-44c8-a4e4-bd007f334d11" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

We have a search parameter in the application. Lets check

<img width="1042" height="408" alt="image" src="https://github.com/user-attachments/assets/116dced6-6c46-4123-adb8-9bf03035db31" />

We can see that the string that we have put in the search parameter got reflected back. So this search parameter needs to check if it has XSS vulnerability.

Lets put a small script and check

<img width="924" height="348" alt="image" src="https://github.com/user-attachments/assets/3dd5a426-0306-4429-80a9-46a3334b074d" />

<img width="1100" height="374" alt="image" src="https://github.com/user-attachments/assets/69063a8b-ea77-448f-85c1-7a385a88c661" />

As the Lab describe, there is a WAF that is filtering common XSS vectors.

So we need to find out which Tags are allowed.

Lets intercept the traffic is Burp suite

<img width="967" height="334" alt="image" src="https://github.com/user-attachments/assets/42ba6c85-8e57-4558-ab42-c94f443f053d" />

<img width="1100" height="516" alt="image" src="https://github.com/user-attachments/assets/88525b3e-52df-4fbc-8c10-7b11ee5e4a57" />

This is the traffic. Lets move this traffic to Intruder.

We will brute force all and check which Tags are allowed.

<img width="1100" height="413" alt="image" src="https://github.com/user-attachments/assets/c100f4b1-f0bf-4d31-b3db-2bebffe7018b" />

We need to add our payload list here

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

<img width="1100" height="352" alt="image" src="https://github.com/user-attachments/assets/963c5d7e-0d56-4b30-9ccd-8b254b0ec922" />

We will copy all the Tags and put in the Payload and start the attack

<img width="1100" height="428" alt="image" src="https://github.com/user-attachments/assets/9f551aca-49f8-45f5-91c6-80196003c6da" />

We are looking for responce code 200

<img width="1100" height="296" alt="image" src="https://github.com/user-attachments/assets/ee0a9f8b-8bf6-48fb-976f-54cfd88e4120" />

So body and xss tags are allowed.

Lets check

<img width="826" height="321" alt="image" src="https://github.com/user-attachments/assets/eb1b2245-826a-4411-a5f7-f68419dab739" />

This time we dont get any error. Also its not reflected back to us which means its getting used as a script.

Now, next we will find which events are allowed.

<img width="1100" height="347" alt="image" src="https://github.com/user-attachments/assets/fe5a33b6-f34a-4006-a332-6022bdbd67f5" />

<img width="1100" height="452" alt="image" src="https://github.com/user-attachments/assets/8409b831-62fb-4eff-a0d7-80fea8e76c5e" />

<img width="1100" height="254" alt="image" src="https://github.com/user-attachments/assets/45c36e1b-869e-4958-b44e-5f640678ce97" />

We can see multiple events are allowed. Lets try onresize

<img width="1100" height="562" alt="image" src="https://github.com/user-attachments/assets/d0e8ff80-96e0-4ca9-a3a5-6685d84e1246" />

On the Cheat sheet, when we select onresize, it will give code for XSS vulnerability.

Lets use this code

<img width="1100" height="357" alt="image" src="https://github.com/user-attachments/assets/905e989b-d5ac-42e9-9fcc-bd91efcbc612" />

After clicking search, we need to resize the window and we will see Print options appears.

<img width="1100" height="537" alt="image" src="https://github.com/user-attachments/assets/ea840b8f-71ea-406d-a9d6-284393b3b181" />

Now when we are using this attack to a victim, we are using following link

<img width="1100" height="620" alt="image" src="https://github.com/user-attachments/assets/cf814e45-dbfc-462d-80bc-09071b5e32c6" />

https://&lt;host&gt;&lt;payload&gt;

https://0a8700a4043ae9fc81da4de40024003b.web-security-academy.net/?search=%3Cbody+onresize%3D%22print%28%29%22%3E

When we send this link to the target, it will not pop-up the print option.

Lets check this URL

<img width="1100" height="493" alt="image" src="https://github.com/user-attachments/assets/9ea38021-8e3e-480a-adce-fe9884ff771e" />


The user will not get the print functionality unless he resize the window. So we need to add some extra code to resize the browser itself.

Lets go to the exploit server which is attacker controlled server

<img width="1100" height="514" alt="image" src="https://github.com/user-attachments/assets/84f472b4-cef2-494f-8c24-5ad7935ecfe8" />

<img width="1100" height="428" alt="image" src="https://github.com/user-attachments/assets/c6ca1484-42ec-4bf8-9b4e-fc83fd6d0258" />

Lets view the exploit

<img width="736" height="235" alt="image" src="https://github.com/user-attachments/assets/c2b9106b-3a5b-4e50-8593-f9ffac8accc0" />

So we have an iframe and we are loading the page inside the iframe.

Now we will use resizing option in the iframe so that it will automatically resize the browser and user dont have to do it by themselves.

We will put the complete URL in the body

<img width="1100" height="330" alt="image" src="https://github.com/user-attachments/assets/271bd908-47d9-4417-950d-640b3e152144" />

Click Store and then Click Deliver exploit to victim

<img width="1100" height="338" alt="image" src="https://github.com/user-attachments/assets/e5cf5182-6335-4918-8e68-a461a33919a8" />

And Lab is solved !!!!












