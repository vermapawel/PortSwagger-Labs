**XSS || Lab #6 DOM XSS in jQuery selector sink using a hashchange event**

<img width="720" height="453" alt="image" src="https://github.com/user-attachments/assets/9f766e07-f6b6-4613-bbc7-282bf525eb3e" />

End Goal of this lab is to exploit DOM-based XSS vulnerability to call print () function.

Lets start the lab

<img width="640" height="442" alt="image" src="https://github.com/user-attachments/assets/95ee3e7b-e598-40c9-9869-c132609efe92" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

Lets check the source code. We are looking for any JavaScript that is taking any input from the client.

<img width="640" height="72" alt="image" src="https://github.com/user-attachments/assets/6f8426d3-b914-4d95-afc6-c7116970b9f6" />

The hashchange event is triggered if fragmented identifier changes.

hashchange event runs when the fragmented identifier of the URL has changed.

fragmented identifier is the part that begins and after the hash sign #. So in the URL everything after the # will be fragmented identifier

<img width="640" height="193" alt="image" src="https://github.com/user-attachments/assets/e64e52fc-1497-454e-b730-d1de72e0ae5c" />

So in this JavaScript code get executed when hashchange event occurs.

Variable post is looking for blog-list which looks for h2 element. h2 element is heading of the articles on the blog.

<img width="640" height="421" alt="image" src="https://github.com/user-attachments/assets/26247a5c-2c45-44bd-ac4f-8de5cb03070d" />

And then its running the function

**decodeURIComponent(window.location.hash.slice(1)**

This function splits the URL everything after the # and its output get saved into the variable post.

And if port is not empty, it will scroll to that article.

<img width="640" height="440" alt="image" src="https://github.com/user-attachments/assets/68395d9d-bf3b-4abd-acf9-37240e3c9f86" />

**Scams, The Peopleless Circus** is the h2 element.

So if we put any of the h2 element after the # in the URL, the function

decodeURIComponent(window.location.hash.slice(1) will run, it will slice the URL after # and the application will scroll to that article.

<img width="640" height="369" alt="image" src="https://github.com/user-attachments/assets/9cd4ac52-f260-494a-8656-d259c970b5f0" />

Anything thing after the hash # is client controllable, which can be vulnerable.

Now, to solve the lab we need to call the print().

Lets create a payload for the attack

***&lt;img src=1 onerror=print()&gt;***

We have created an image tag whose source could be anything. If image is not found, it will generate onerror which calls the print function.

<img width="640" height="358" alt="image" src="https://github.com/user-attachments/assets/af837a24-25a7-4eaf-a298-bb3eced37e55" />

Print function got called. However Lab is not solved yet.

Now, in the real world scenario when we send the URL to the victim, it will not call the Print function. This is because the script is only triggered when there is a change is the URL.

https://0a800065035f3c6480f3037700b00056.web-security-academy.net/#%3Cimg%20src=1%20onerror=print()%3E

So when we send this URL to the victim, it need to change first to execute the payload.

Lets go to the exploit server which is attacker controlled server

<img width="640" height="236" alt="image" src="https://github.com/user-attachments/assets/c397d69b-9f73-4d5a-a0c4-4bb98d1a98f2" />

First we will check if we are allowed to Frame this application or not.

<iframe src=”https://0a800065035f3c6480f3037700b00056.web-security-academy.net/#"></iframe>

<img width="640" height="189" alt="image" src="https://github.com/user-attachments/assets/d8c23c89-6e04-41fb-9812-7fc75fa346e7" />

<img width="640" height="208" alt="image" src="https://github.com/user-attachments/assets/4cd7d1a2-d6e8-4b02-98ef-1d93a1f63a97" />

This is the iframe and we have the application in the iframe. This will get loaded in the victim browser when he clicks the malicious link.

Lets create the payload.

<iframe src=”https://0a800065035f3c6480f3037700b00056.web-security-academy.net/#" onload=”this.src+=’&lt;img src=1 onerror=print()&gt;’”></iframe>

<img width="640" height="199" alt="image" src="https://github.com/user-attachments/assets/f1fa5ceb-9a2f-4606-9223-e4a4d96a3b64" />

The simulated bot will click on the link the payload will be executed.

<img width="640" height="170" alt="image" src="https://github.com/user-attachments/assets/4045b976-2805-4d48-bfa3-4f9c9f5cb669" />

And our Lab is solved !!


