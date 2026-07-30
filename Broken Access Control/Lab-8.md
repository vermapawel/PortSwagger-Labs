**Broken Access Control ||Lab #8 User ID controlled by parameter, with unpredictable user IDs**

<img width="871" height="421" alt="image" src="https://github.com/user-attachments/assets/7f1b4e7a-93f7-4d76-b105-b4040fefd623" />

Goal of this lab is to get API key for carlos. 

Lets open the lab and login with the credentials

<img width="846" height="365" alt="image" src="https://github.com/user-attachments/assets/eac856a1-da36-483c-b11a-b4c5cf6994b8" />

Lets check this traffic in Burp suite

<img width="900" height="292" alt="image" src="https://github.com/user-attachments/assets/8b8c20c9-0b8e-4f67-9564-ac06b307f769" />

Here the id parameter is not something we can predict or brute force. This is what GUID means. Also to use other user account we need to find other users GUIDs. 

Now, lets go to the home page and check some articles

<img width="900" height="594" alt="image" src="https://github.com/user-attachments/assets/efefca21-7317-43bc-94cb-997ea153ce9a" />

This post is written by carlos. Let click on carlos and check

<img width="900" height="309" alt="image" src="https://github.com/user-attachments/assets/4208bf59-5e51-45d3-bd97-8351eff49219" />

We got the user-Id for carlos 498b5ad1–2d15–46c3–803f-878a7ef7eb48

Lets put carlos UID in the

<img width="900" height="446" alt="image" src="https://github.com/user-attachments/assets/0b8623ec-08e2-4b88-ad31-88df6d69a3c8" />

And we got the carlos API key

<img width="900" height="348" alt="image" src="https://github.com/user-attachments/assets/184fdbe8-83a9-4f77-8031-4703d42db7c9" />

And lab is solved

<img width="900" height="260" alt="image" src="https://github.com/user-attachments/assets/ab03b003-90f8-4201-99e8-d0a8e21c5e00" />
