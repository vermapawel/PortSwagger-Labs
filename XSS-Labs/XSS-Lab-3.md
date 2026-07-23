**XSS || Lab #3 DOM XSS in document.write sink using source location.search**

<img width="720" height="433" alt="image" src="https://github.com/user-attachments/assets/aa986908-46e9-4dcc-9492-f11c28416baa" />

Lets start the Lab

<img width="640" height="474" alt="image" src="https://github.com/user-attachments/assets/549f73d9-7891-4903-ba8e-c52154b42662" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

<img width="640" height="258" alt="image" src="https://github.com/user-attachments/assets/e96bc669-fff4-4d17-94e5-3b9bfe3498f8" />

We have a search functionality. Lets put a string and check

<img width="640" height="277" alt="image" src="https://github.com/user-attachments/assets/09915994-a45c-4b87-8317-49f03a573fca" />

We can see that what we search got reflected back to us, it could be vulnerable to XSS.

Lets check the developer tool

Right click → Inspect

Lets search the string that we have entered.

<img width="640" height="315" alt="image" src="https://github.com/user-attachments/assets/e98d779b-f98c-48ec-8351-fd61504772a5" />

We can see there are two matches for this string. 1st one is in the Heading element where it got reflected back to the user.

Lets check the other match

<img width="640" height="279" alt="image" src="https://github.com/user-attachments/assets/7cfa03f1-56d6-4cfa-be79-6282d55fccf3" />

We can see that the string is inserted directly into the src attribute of an <img> tag.

Now lets try to find how this link got generated. Lets check the source code of the application.

<img width="640" height="126" alt="image" src="https://github.com/user-attachments/assets/1a7054ac-2b01-466d-8c66-3ace00a1745c" />

This is the JavaScript that is generating that URL.

It takes the search parameter from the user and saves in a variable called query.

Now, if query is not empty (someone out some string in the search parameter), it will call a function trackSearch

Now trackSearch function writes to the HTML page using document.write saying create an image that has the source /resources/images/tracker.gif?searchTerms= query (String that we have put in the search parameter)

This could be vulnerable to DOM based XSS because it taking a client supplied input and making changes to the document object model.

Lets create the payload

<img src=”/resources/images/tracker.gif?searchTerms=121323">

Now we need to add a double quote “ that will close the 1st double quote. Also we need to close the angle bracket of the img src.

<img src=”/resources/images/tracker.gif?searchTerms=121323">”>

Now we can add any XSS payload that we want. In this Lab we need to generate an alert. Lets add the alert function

<img src=”/resources/images/tracker.gif?searchTerms=121323"><script>alert(1)</script>”>

So our payload is ***“><script>alert(1)</script>***

<img width="640" height="322" alt="image" src="https://github.com/user-attachments/assets/1db5b6e3-f476-4670-93c4-ba5ea4ae6aa3" />

<img width="640" height="217" alt="image" src="https://github.com/user-attachments/assets/648a1013-ae5c-449f-b165-50d3eb151381" />

And the Lab is solved

<img width="640" height="211" alt="image" src="https://github.com/user-attachments/assets/d2996e9b-6df1-4cc1-8b7a-b65df7d58b3b" />

