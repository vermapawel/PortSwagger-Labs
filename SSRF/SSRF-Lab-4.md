**SSRF || Lab#4 : SSRF with blacklist-based input filter**

<img width="865" height="437" alt="image" src="https://github.com/user-attachments/assets/101ef918-d733-4fb9-93cd-5edd1ddb38db" />

Vulnerable parameter → Stock Check functionality.

Goal of the lab is to change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos

Lets open the lab

<img width="847" height="652" alt="image" src="https://github.com/user-attachments/assets/c265ceca-3e06-4c9c-9fee-d4a234b048d4" />

When we click on Check stock, it will display how many units are available in that particular store.

Lets intercept this traffic in Burp suite

<img width="1100" height="327" alt="image" src="https://github.com/user-attachments/assets/41965044-2f9f-4298-b73e-dd6d20cf0643" />

Lets move this traffic to Repeater

<img width="1100" height="477" alt="image" src="https://github.com/user-attachments/assets/1c45b7e5-3d67-43b0-8b03-0bacdf5dc1a3" />

We can see there is a URL as it starts with http and have some parameter. Its seems its URL encoded. Lets decode it.

stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1

So, this application is talking to a different URL stock.weliketoshop on port 8080 to check the stock of an item. The path to the stock check feature is /product/stock/check

Lets check if any application is running in local host

<img width="1100" height="471" alt="image" src="https://github.com/user-attachments/assets/1bcf331b-439e-4652-98d5-3d079816ed6c" />

Looks like there might be an application that is running at localhost however we are not allowed to visit.

Lets try with IP address

<img width="1100" height="494" alt="image" src="https://github.com/user-attachments/assets/49b34e56-1d0e-4dc9-a5aa-f4d9b1239f06" />

127.0.0.1 is also blocked.

Lets try 127.1

<img width="1100" height="429" alt="image" src="https://github.com/user-attachments/assets/bfd02daa-cc9e-4b5e-836a-e59e8e39ccd8" />

This time we got a 200 OK response. It means keywords localhost and 127.0.0.1 was blocked by the application.

Lets try to access admin panel

<img width="1100" height="472" alt="image" src="https://github.com/user-attachments/assets/5f795d7a-a271-4196-abba-0a8a7d9c07b6" />

We are not able to access admin panel. It seems keyword admin is blocked.

Lets URL encode some of the characters of admin and try

<img width="1100" height="463" alt="image" src="https://github.com/user-attachments/assets/de6a7d70-8f51-40c3-81db-56dcaaa90e83" />

We have URL encoded characters ad but still getting the error. Lets URL encode one more time.

<img width="1100" height="416" alt="image" src="https://github.com/user-attachments/assets/04bca768-9e5f-435e-a793-f9ba2f246c03" />

And this time we got 200 OK response.

<img width="1100" height="485" alt="image" src="https://github.com/user-attachments/assets/4785c788-721f-40c2-be61-342fcabdb83c" />

We can see there are two users. To solve the lab we have to delete carlos.

Lets find its path

<img width="1100" height="445" alt="image" src="https://github.com/user-attachments/assets/54a97748-0f15-4360-8f3a-d758355e9537" />

/admin/delete?username=carlos

<img width="1100" height="475" alt="image" src="https://github.com/user-attachments/assets/f1bdf50f-df5d-4676-9102-9d37d183919c" />

We got a 302 response code. Lets follow the redirection.

<img width="1100" height="441" alt="image" src="https://github.com/user-attachments/assets/f9475224-1ceb-452e-a389-07d2b4ceac1a" />

And we don’t see carlos user anymore. To confirm lets go to the Admin page

<img width="1100" height="449" alt="image" src="https://github.com/user-attachments/assets/d3567af6-6e2f-4fc1-bba0-80a851def893" />

We see there is only one user. Lab is solved.

<img width="790" height="257" alt="image" src="https://github.com/user-attachments/assets/7f38ef52-66f2-4a9c-9115-5a0c380637f0" />
