**Command Injection || Lab#2 ||Blind OS command injection with time delays**

<img width="771" height="350" alt="image" src="https://github.com/user-attachments/assets/84901615-e2e0-44b7-82d3-045c20e5315f" />

To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay.

Lets start the Lab

<img width="942" height="462" alt="image" src="https://github.com/user-attachments/assets/7362865b-5e86-45a6-b1dc-a61975d2e417" />

As per lab description, OS command injection vulnerability is in the feedback function.

<img width="792" height="611" alt="image" src="https://github.com/user-attachments/assets/4302cb9b-8f46-47fb-b1f7-5ba2f82a70d7" />

We got a response from the application that our feedback have been submitted.

<img width="747" height="586" alt="image" src="https://github.com/user-attachments/assets/c3b1d14e-11f7-45c5-9bdc-47f0786542b2" />

Lets intercept the traffic with Burpsuite

<img width="1100" height="529" alt="image" src="https://github.com/user-attachments/assets/c8120ed0-4120-4778-88c0-2a80a5154e99" />

There are multiple parameters. We have to check one by one.

As per lab description, we have to solve labs by time delay. We will inject command sleep 10 which will slow down the response for 10 seconds

Lets start with name parameter.

csrf=lzRbA98CE4SHybP65HCqwtrYhUyH82xZ&name=test&sleep10#&email=test%40test.com&subject=test&message=test

Lets URL encode &sleep10# and froward the traffic

<img width="1100" height="389" alt="image" src="https://github.com/user-attachments/assets/a4667509-633c-4367-b56f-c362ecb1739f" />

We got the response instantaneously. It means this name parameter is not vulnerable to command injection.

Lets check the email parameter

csrf=lzRbA98CE4SHybP65HCqwtrYhUyH82xZ&name=test&email=test%40test.com& sleep 10 # &subject=test&message=test

Lets URL encode &sleep 10 #

<img width="1100" height="444" alt="image" src="https://github.com/user-attachments/assets/75eab1b9-9b0e-40c4-9311-3fa1852c4b79" />

At the bottom right we can see that there is a 10 sec delay. It means our payload got executed usefully.

It confirms that email parameter is vulnerable to command injection.

The Lab is solved

<img width="1100" height="245" alt="image" src="https://github.com/user-attachments/assets/d3af5158-fa43-444e-b309-70a6e5b284c6" />
