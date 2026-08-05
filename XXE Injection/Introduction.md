**XXE Injection || Introduction**

<img width="1000" height="552" alt="image" src="https://github.com/user-attachments/assets/1ca6cb84-e4aa-4041-b241-d16a31c4d36f" />

It is similar to HTML where HTML is about data representation, XML is more about data transportation and storage.

<img width="1000" height="575" alt="image" src="https://github.com/user-attachments/assets/4c63458c-cc3c-414b-9ce3-1bfab1b26ebd" />

The about XML is used for managing a book store application.

The 1st part is XML Declaration which contains necessary  details that an XML processor needs to parse the XML document. It includes version and character encoding used in the document. XML declaration is optional, however if we decided to use it, it must be the 1st line of the XML document.

Root Element:- Each document can have only one root element. Here its <bookstore>

Inside Root Element, we have Nested Tags or Child Element. Here we have two child element <book> and each child element contains three Nested Element <title> <author> <year>

There are some rules we need to follow while writing XML document.

1. Every element that has a start tag should have an end tag.
   
2. XML tags are case sensitive.
   
3. XML tags must be closed in an appropriate order.

**XML entities**

XML entities are similar to variables that stores data and can be used multiple times. There are multiple pre-defined XML entities that we can use as per our need.

<img width="1000" height="492" alt="image" src="https://github.com/user-attachments/assets/f45cd0b2-462a-49d4-926b-c5d7761f3a27" />

XML Entities are defined in a separate part of the XML document called Document Type Definition (DTD). DTD contains the declaration of an XML document and types of data value it can contain.

Here we have created a custom ENTITY name and assigned a value "Peter kim". Every time we want the name "Peter Kim" we can use this entity name by using &name;.

There are many types of XML entities.

<img width="1000" height="550" alt="image" src="https://github.com/user-attachments/assets/d3dd6cdd-5635-41fa-b597-a5007d42e7d9" />

Internal and External Entities are called General Entities.

**Internal Entities:-**

<img width="1000" height="350" alt="image" src="https://github.com/user-attachments/assets/2bc11249-d8da-43ca-9406-a382104f9955" />

Here **name** is an internal entity which has been created locally under bookstore.

**External Entities**

<img width="1000" height="282" alt="image" src="https://github.com/user-attachments/assets/cdac1cff-57cf-4762-8f20-506edbb801e5" />

External Entities are defined outside the DTD. Here product is the external entity. SYSTEM is a keyword to indicate that this is the external entity and the resource that we need to fetch is an external resource product.txt with the help of file protocol

**Parameter Entities**

<img width="1000" height="309" alt="image" src="https://github.com/user-attachments/assets/12a2630a-4377-4b8f-8688-064e74eb1755" />

A Parameter entity starts with % that instruct the XML that a Parameter entity is defined and not a General entity. We can reference a parameter entity by using %name; and that can only be done in DTD.

XXE Injection is a vulnerability that allows an attacker to interfere with an application's processing of XML data.

Lets say there is an online store that has the functionality that allows to check if an item is in stock. When we click 'Check Stock' the application makes a request to /product/stock endpoint and in the body of the request it sends an XML document for the specific product.

<img width="1000" height="414" alt="image" src="https://github.com/user-attachments/assets/92c55667-9430-45ae-8884-9c3fb3ab7be3" />

In this example the product ID is 17 and we are checking the available stock in Store ID 1. This request is coming from the client side to the backend and the XML processor process the request and display the output. 

This is how the application is intended to function.

<img width="1000" height="348" alt="image" src="https://github.com/user-attachments/assets/c0819c2d-f42c-4349-8f87-8953e686ac7e" />

An attacker can exploit this functionality by using XML external entity.

Here we are using an external XML entity xxe to get /etc/passwd. 

If the application is configured to allow arbitrary external entity, when the backend receives the request and output the content of the /etc/passwd file.

<img width="1000" height="555" alt="image" src="https://github.com/user-attachments/assets/95e2c2de-74d9-4045-a728-b1a59f591a3c" />


**Out-Of-Band XXE Injection**

<img width="1000" height="409" alt="image" src="https://github.com/user-attachments/assets/ca26e542-b379-4e63-b866-ca89f37eee5f" />

Let say a user is checking the stock availability of a product having ID 17. It sends a POST request for the to get the information. There is some validation done by the application to check if the output of the request is in integer (as number of available unit will be in integer). Now if its not integer, it will send a generic error like product ID is not valid.

<img width="1000" height="370" alt="image" src="https://github.com/user-attachments/assets/ae21ca79-a62e-4296-b6c6-f37f6edae95d" />

So if an attacker will request to get output of /etc/passwd file, as the output will be not integer and in strings, the application will block the output and send an error like Invalid product ID. 

In this type of setting, we cannot display the output on the screen.

<img width="1000" height="514" alt="image" src="https://github.com/user-attachments/assets/89ed0c22-7e90-4808-8baa-40786b4e5694" />

In this case the attacker can use http protocol in the external entity to try to ping an external server that is controlled by the attacker. We will still get the generic error on the screen, but if the application is vulnerable to XXE, we will get a ping back to the external server.

**Error-Based XXE injection**

It occurs when the attacker manipulate the application to generate an error

<img width="1000" height="496" alt="image" src="https://github.com/user-attachments/assets/e84b0f6b-b040-4233-b399-d4ef08a04518" />

