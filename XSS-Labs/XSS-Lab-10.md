**XSS || Lab #10 DOM XSS in document.write sink using source location.search inside a select element**

<img width="720" height="470" alt="image" src="https://github.com/user-attachments/assets/b7fae758-3c14-4ed5-bc8d-b2197e776c3d" />

Lets start the Lab

<img width="640" height="362" alt="image" src="https://github.com/user-attachments/assets/6968a947-970c-4e57-aa5f-61b2dc7d26e6" />

Now, the 1st thing we need to check if any of the parameter is user controllable that could be vulnerable to XSS.

Lets check the products.

<img width="640" height="471" alt="image" src="https://github.com/user-attachments/assets/3a1530de-b238-487a-af47-6541bd38911a" />

In the Check stock options, there are list of different cities and how many units of this product are available there. Like in London there are 378 units of this product available.

At first glance, it don't look like vulnerable to XSS however depending on how it is coded we may be able to exploit it.

Lets check the source code of the page.

<img width="640" height="233" alt="image" src="https://github.com/user-attachments/assets/3232d4f6-034a-4b70-81f4-a3510e089dcb" />

There is a custom JavaScript that is responsible for Stock check parameter.

Lets understand the Script.

There is a variable called var which takes input from an array that contains London, Paris and Milan as values.

There is another variable called Store and its taking its value from the URL parameter that is called StoreID.

However when we check the URL we don't see this StoreID

<img width="720" height="382" alt="image" src="https://github.com/user-attachments/assets/5b6fe4a4-241f-493d-b1e4-55f1d24bdffd" />

We only see ProductID =1

As per the Script, the value of StoreID is getting saved in &lt;select&gt; element.

Lets validate

<img width="640" height="162" alt="image" src="https://github.com/user-attachments/assets/300e53a4-82d2-46ba-b748-739fd092e5d2" />

Currently there are three locations available.

Lets add a new value to storeId in the URL and see how it reacts.

<img width="640" height="101" alt="image" src="https://github.com/user-attachments/assets/55c8c857-3765-49c2-b942-c7c8eb5879da" />

The value that we have entered in storeID, it got added in the Check stock.

So we got a user controllable parameter which is in URL its value get stored in the JavaScript of the Application.

So it could be vulnerable to DOM based XSS if the input is not properly validated.

Lets check the source code again

<img width="640" height="226" alt="image" src="https://github.com/user-attachments/assets/8844e769-6e21-47c0-b232-9d48c6c5b86a" />

Anything we put in the URL will get stored in storeID.

&lt;select name=”storeId”&gt;

Then we have bunch of <option> then </select> statement ends.

The idea over here is that we need to get out of the <select> statement.

Now, after the string that we have entered (Paris2) in the URL we will close the </select> statement and then we can add our payload.


&lt;option selected&gt;Paris2&lt;/select&gt;&lt;img src=1 onerror=alert(1)&gt;&lt;/option&gt;


we are putting an image element whose source value is could be anything, lets say 1. When that source is not found, it will throw an error in the form of an alert. Then we will close the &lt;/option&gt;

So our payload is Paris2&lt;/select&gt;&lt;img src=1 onerror=alert(1)&gt;

<img width="640" height="92" alt="image" src="https://github.com/user-attachments/assets/2905347b-776c-4049-a742-d34189ece7f7" />

When we hit enter, we got an error pop-up message

<img width="640" height="325" alt="image" src="https://github.com/user-attachments/assets/eb075f83-7f79-441e-b62b-1113a22bf6b8" />

And the Lab is solved !!!

<img width="640" height="208" alt="image" src="https://github.com/user-attachments/assets/9db173bd-17c8-403b-bd8a-3190f0f5d8e1" />











