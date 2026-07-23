**XSS || Lab #1 Reflected XSS into HTML context with nothing encoded**

<img width="720" height="383" alt="image" src="https://github.com/user-attachments/assets/97b52cc6-03c7-4fec-b26f-776dbb385457" />

Lets open the Lab

<img width="640" height="402" alt="image" src="https://github.com/user-attachments/assets/0f6f2331-6b92-4c43-8575-336e0de7bcc4" />

When if comes to Cross-Site Scripting first thing we are looking for input that get stored or reflected back to the user in the application.

We can see there is a search functionality. Lets search anything and see how application reacts

<img width="640" height="231" alt="image" src="https://github.com/user-attachments/assets/5ae7d471-1464-43ee-a8ec-a450c9f8281d" />

Click on search

<img width="640" height="238" alt="image" src="https://github.com/user-attachments/assets/daf0692b-af1d-4861-8e5a-2388de9306c3" />

We can see the input that we have entered into the search functionality, got reflected back to us.

It gives us a hint that the application could be vulnerable to XSS.

<img width="640" height="279" alt="image" src="https://github.com/user-attachments/assets/f614a05a-cbc4-420b-bd49-87d4da14dfba" />

Lets check the traffic in Burp suite

<img width="640" height="384" alt="image" src="https://github.com/user-attachments/assets/700cc5ec-1a20-4cec-845b-83c6143ab9f4" />

Lets move this traffic to Repeater

<img width="640" height="343" alt="image" src="https://github.com/user-attachments/assets/0dcee5a3-0e34-419c-93cd-14ab34727f3f" />

We can see the string that we have entered, it reflected to only one location.

Lets put < in the search bar

<img width="640" height="262" alt="image" src="https://github.com/user-attachments/assets/7877db8d-40df-4635-afac-65e06a04eb7a" />

< got reflected back.

<img width="640" height="363" alt="image" src="https://github.com/user-attachments/assets/f55a0dcb-f78a-4271-ac81-0fef928313d2" />

< got reflected directly into the HTML code. It means this application is vulnerable to XXS.

To complete the Lab we need to call the alert function.

Lets create the payload

***<script>alert(1)</script>***

The alert() function is a built‑in JavaScript function that displays a simple popup message box in the browser.

<script> is an HTML tag used to embed or reference JavaScript code inside a webpage.

<img width="640" height="279" alt="image" src="https://github.com/user-attachments/assets/1c7c8c76-8d6e-47ac-8d57-308370b9295e" />

<img width="640" height="241" alt="image" src="https://github.com/user-attachments/assets/c62ae0f3-9fcc-4578-a672-ad033ba816a6" />

<img width="640" height="348" alt="image" src="https://github.com/user-attachments/assets/0538ae78-317b-4fe1-b9e5-7d4597d2f268" />

We got a pop-up window with 1.

<img width="640" height="270" alt="image" src="https://github.com/user-attachments/assets/bf2ffeb3-53bf-4a15-9ea7-a2d93c8bc2dc" />

And the Lab is solved !!!














