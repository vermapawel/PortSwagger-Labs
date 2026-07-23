**XSS || Lab #12 Reflected DOM XSS**

<img width="826" height="492" alt="image" src="https://github.com/user-attachments/assets/dc2847bb-fe82-4bea-85ff-57bc7f962ba8" />

Goal of this Lab is to perform DOM XSS to call alert function.

Lets start the Lab

<img width="1100" height="766" alt="image" src="https://github.com/user-attachments/assets/b28b1242-b8b7-45d0-b9c3-5c99489983d9" />

Now, the 1st thing we need to check if any of the parameter could be vulnerable to XSS. We can put a string in the parameter and see if it reflected back to us or potentially even interacting with the document object model (DOM).

There is a search parameter in the application. Lets check

<img width="943" height="406" alt="image" src="https://github.com/user-attachments/assets/d45b48ff-c2a0-4536-99cb-f073c38a6107" />

We can see that the string that we have put in the search parameter got reflected back.

Now, we need to find where this string got stored.

<img width="1077" height="592" alt="image" src="https://github.com/user-attachments/assets/89659328-87ba-4264-a67f-4f9e356520cb" />

Our input is stored only at one place that is in the heading element.

However there is a <script> that is called and processed under **/resources/js/searchResults.js** folder. So it seems this script is involved in displaying the search string on the application.

Lets open this scrip and see if we can find anything

<img width="838" height="340" alt="image" src="https://github.com/user-attachments/assets/58777ee7-0db4-4cf3-bc9b-7fa14ee5ddd6" />

<img width="1100" height="685" alt="image" src="https://github.com/user-attachments/assets/706b96b9-3c2d-40ad-9723-e0f9dc4e73d4" />

We have a function called search that take one input parameter called path.

Now, important thing to notice here is that eval () function is being called here. If eval () takes input from client, it could be vulnerable as it allows to run JavaScript and we can take advantage of it.

**eval(‘var searchResultsObj = ‘ + this.responseText);**

It seems that eval() is creating a searchResultsObj and its saving the response.text in that object.

Most likely response.text is coming from client side and then it calls a function displaySearchResults which takes in the content of the variable searchResultsObj

Lets check the request in Burp suite

<img width="1100" height="509" alt="image" src="https://github.com/user-attachments/assets/08aa8d57-86be-409c-ba07-9f8b602db2a8" />

We can see that the response of the search is in a simple JSON text.

This is the response.text in the eval function.

So if we can change the responce.text, we can exploit the vulnerability.

Now, when we put anything in the search filed, we get the seatchTerm and the content of the search field is in the JSON string.

<img width="538" height="136" alt="image" src="https://github.com/user-attachments/assets/546747a4-3a22-4cd3-9d23-a5af145d83e6" />

So we will try to break out of this string and add another command that will be stored in the eval()

Lets put a “ and check

<img width="1100" height="466" alt="image" src="https://github.com/user-attachments/assets/5f634479-7dad-406c-a0ed-17f994a9761e" />

We can see that the double quote is escaped or commented out using a \

Lets check if it escapes \

<img width="1100" height="502" alt="image" src="https://github.com/user-attachments/assets/b73b5cc7-f256-4b25-8450-4e9b0c8edc8c" />

And the application is not escaping the \

Lets understand that happening here

When we put a double quote after search i.e 12345" the application escaped the double quote using a backslash 12345\”

Now, when we put a backslash \ its escaping the \” that application has put automatically to escape double quote “

So the \ that we have put is escaping the \ that was put by application and “ is not getting escaped.

Now we will close the JOSN string

<img width="1100" height="344" alt="image" src="https://github.com/user-attachments/assets/8e76d437-a306-4cd1-b7b8-c192b2b366e6" />

Now we can put some other commands that we want to get stored in the eval()

<img width="1100" height="363" alt="image" src="https://github.com/user-attachments/assets/635e3a0e-9147-4f8f-8eee-f3e4764eb9fb" />

**12345\”};+alert(1);//**

We will add a semi-colon (;) to close the code block, add a + for URL encoding and alert function. Then we will add // to comment out rest of the code.

<img width="996" height="337" alt="image" src="https://github.com/user-attachments/assets/db85229f-bab1-46a2-870c-9df7bf5001ea" />

Lets put this payload in the search parameter.

We get an alert pop-up.

<img width="1100" height="577" alt="image" src="https://github.com/user-attachments/assets/0e5bdaed-6514-4f23-9b70-40f39e625131" />

And the Lab is solved.

<img width="1100" height="488" alt="image" src="https://github.com/user-attachments/assets/c4ddd7b3-ae58-4e28-af0c-87333bcab197" />

