# lets scan the network and look for the target

![Screenshot from 2025-05-24 12-11-24](https://github.com/user-attachments/assets/62554c4d-6c35-4e71-9beb-7a9eb428f8d7)

![Screenshot from 2025-05-24 12-11-38](https://github.com/user-attachments/assets/9f816008-45c1-40e4-9ae6-324800ab244b)

The host is active and seems to be running windows. ttl=128

# lets look for open ports

![Screenshot from 2025-05-24 12-20-14](https://github.com/user-attachments/assets/cda823ba-41d3-4269-bb32-69aaac03cd2e)

![Screenshot from 2025-05-24 12-20-50](https://github.com/user-attachments/assets/76f052b6-a204-424d-b38f-0166ba6e3b90)

# lets chech what services and versions are running in those open ports

![Screenshot from 2025-05-24 12-21-06](https://github.com/user-attachments/assets/83862e61-116d-4922-a021-75c04005ca17)

![Screenshot from 2025-05-24 12-21-49](https://github.com/user-attachments/assets/98cb101c-7e01-4c8b-9594-fd998578a0e1)

![Screenshot from 2025-05-24 12-21-59](https://github.com/user-attachments/assets/733eac3b-566c-4485-85ee-6c4bdba6203d)

# lets look for vulnerabilities that are crittical that can be exploited

![Screenshot from 2025-05-24 12-22-45](https://github.com/user-attachments/assets/5156dcd3-5905-4b81-b544-748278c7d01a)

![Screenshot from 2025-05-24 12-23-05](https://github.com/user-attachments/assets/c3e1b747-e662-4c21-8251-03a6cdaafe42)

# smb enumeration

![Screenshot from 2025-05-24 12-52-39](https://github.com/user-attachments/assets/f588f171-4cf0-40a8-8f07-be2811bbf0d5)

# lets seeif we can access any shares without login

![Screenshot from 2025-05-24 12-56-28](https://github.com/user-attachments/assets/39758443-f505-4ccd-9aa9-2c0e279e2f53)

![Screenshot from 2025-05-24 12-56-38](https://github.com/user-attachments/assets/7bcea0ec-de51-432a-81f4-65771ddd1a84)

![Screenshot from 2025-05-24 12-56-52](https://github.com/user-attachments/assets/87cd9794-6061-4d33-9705-dd2c8b3ecfce)

![Screenshot from 2025-05-24 12-59-58](https://github.com/user-attachments/assets/e597dacc-5080-4c3e-b98c-c4acd479b7b2)

![Screenshot from 2025-05-24 13-19-04](https://github.com/user-attachments/assets/2fe1c2f9-3ad7-45e0-9a53-289333a8417e)

![Screenshot from 2025-05-24 13-19-13](https://github.com/user-attachments/assets/c4ee60b3-2dc4-46dc-981e-dfcb6554d4d5)

We couldnot get any users or shares, lets bruteforce to get some usernames 

# kerbrute
# lets try to bruteforce some users using the kerbrute 

![Screenshot from 2025-05-24 13-28-29](https://github.com/user-attachments/assets/f25950b5-eb5e-42aa-9c00-8116213f9cc9)

Since administrator is the system account, we will use another wordlist

![Screenshot from 2025-05-24 13-26-24](https://github.com/user-attachments/assets/0473c974-a0b7-4060-9468-dc7b0689e904)

![Screenshot from 2025-05-24 13-28-42](https://github.com/user-attachments/assets/460e7ea9-e346-4b14-b1b1-6328b983b154)

We got a new username

# AS-REP Roasting

![Screenshot from 2025-05-24 18-22-43](https://github.com/user-attachments/assets/70e2d529-0466-497a-aa6a-eccec7efb950)

![Screenshot from 2025-05-24 18-23-47](https://github.com/user-attachments/assets/fb7cd616-ebed-482c-9901-dd4858659be3)

We will use python script of impacket GetNPUsers.py

![Screenshot from 2025-05-24 16-38-14](https://github.com/user-attachments/assets/3e9546fe-1ff2-4e6d-8aed-540aa3a655ba)

![Screenshot from 2025-05-24 16-38-34](https://github.com/user-attachments/assets/b660091d-ff8b-4404-878b-46ee50181abf)

our machine cannot resolve the control.nyx, we can just add it into the list of host and and resolve it.

![Screenshot from 2025-05-24 16-40-03](https://github.com/user-attachments/assets/97e5be60-c13b-4ace-ae35-d9d6d1ac7246)

![Screenshot from 2025-05-24 16-41-39](https://github.com/user-attachments/assets/b206b14e-55ef-4417-98b2-70f8e8bc3790)

We were succesfully able to perform kerberaoasting and get the hash. we can crack the hash and get the password.

# Cracking the hash

![Screenshot from 2025-05-24 17-00-39](https://github.com/user-attachments/assets/659e12ee-9fc7-4945-b48a-ad0917a1fb90)

Now we have the password for the account 

# lets check the username and password and use it to login to the target machine

![Screenshot from 2025-05-24 18-43-36](https://github.com/user-attachments/assets/ddb31cff-b0fb-428b-8e36-f496d2be5bfb)

![Screenshot from 2025-05-24 18-45-06](https://github.com/user-attachments/assets/972f76fd-d0db-4816-9bf2-8332c30ad1da)

We are not able to login into the domain using these credentials, lets try dump data from ldap using these 
credentials

# ldapdomaindump

![Screenshot from 2025-05-24 19-06-07](https://github.com/user-attachments/assets/838610a1-2170-4e88-8d79-2930dcb261ba)

![Screenshot from 2025-05-24 19-06-29](https://github.com/user-attachments/assets/c8c4db28-72e4-47c3-9a4e-e8781f361cf0)

Lets host these data in the pyhton server so we can view it from the web browser

![Screenshot from 2025-05-24 19-10-03](https://github.com/user-attachments/assets/3887d715-ca20-4b64-96a5-6321eb62299d)

lets check into the users

![Screenshot from 2025-05-24 19-03-48](https://github.com/user-attachments/assets/6fdef489-bb96-4fc3-8d18-ad7c36969ef3)

Only three account are enabled and since the account we had access to was not the part of the Remote management
users, we couldnot access the target using it.

we will copy all the users and put it into the file users.txt
Lets try to bruteforce to account which is part of remote management user

# bruteforce the remote management user

![Screenshot from 2025-05-24 19-37-25](https://github.com/user-attachments/assets/94aff37d-c79d-4a06-b0d1-65da5914823d)

![Screenshot from 2025-05-24 19-26-12](https://github.com/user-attachments/assets/d6cc0884-a29f-453b-b69b-4fdcb7835c2c)

![Screenshot from 2025-05-24 19-26-33](https://github.com/user-attachments/assets/4160e27b-9126-4315-a33a-a0693c47459b)

![Screenshot from 2025-05-24 19-29-53](https://github.com/user-attachments/assets/68dfb8f5-8244-49f8-8022-bb85bd62fa75)

![Screenshot from 2025-05-24 19-30-29](https://github.com/user-attachments/assets/13fb4023-e041-47e7-8816-b3e8ded28692)

# Privilige Escalation

We are going to upload SharpHound into the window and map the entire domain as winPEAS binary was not able to
find us any useful information.

![Screenshot from 2025-05-24 21-15-10](https://github.com/user-attachments/assets/00ac002f-ed1c-4000-9656-50b1cf93dbe5)

We are going to open up the python server which will share the Sharphound and winPeas into the system we compromised

![Screenshot from 2025-05-24 21-15-50](https://github.com/user-attachments/assets/1bace549-defa-4035-a4f1-ca2c89a5e7a5)

![Screenshot from 2025-05-24 21-16-06](https://github.com/user-attachments/assets/1090fd40-baa8-44ba-b125-b7002ccfe2d0)

We also have downloaded the zip file, lets unzip it

![Screenshot from 2025-05-24 21-47-57](https://github.com/user-attachments/assets/b553ef3a-6507-4923-814a-33a1283c73b5)

lets start the bloodhound

![Screenshot from 2025-05-24 21-48-09](https://github.com/user-attachments/assets/714296c0-ce60-4ed8-b5dd-c362dd8cc9a7)

login and upload the data from the sharphound

![Screenshot from 2025-05-24 21-08-01](https://github.com/user-attachments/assets/c421ebd0-c242-456d-b600-f88de3732108)

![Screenshot from 2025-05-24 21-12-09](https://github.com/user-attachments/assets/7ccfaad5-8755-48c1-8e61-38481250d670)

![Screenshot from 2025-05-24 21-14-08](https://github.com/user-attachments/assets/96305f32-7758-498b-a4cd-688903aa8d11)

![Screenshot from 2025-05-24 21-14-24](https://github.com/user-attachments/assets/f72a7859-7d4e-4e6d-8c48-f7c3c148ba99)

![Screenshot from 2025-05-24 21-56-13](https://github.com/user-attachments/assets/ca0bdef5-9b60-4660-b2b3-55d16c9385f0)


![Screenshot from 2025-05-24 21-56-40](https://github.com/user-attachments/assets/5047961c-e5ab-41bb-8f88-085f7b39e1af)

![Screenshot from 2025-05-24 21-57-10](https://github.com/user-attachments/assets/429e6350-bba2-403d-ad66-530bb1c5abc7)

We have successfully exploited the Controller.
Thank you!!
