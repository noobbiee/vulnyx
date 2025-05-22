# look for the target ip address

![Screenshot from 2025-05-21 10-33-34](https://github.com/user-attachments/assets/c67dcc95-eab3-4a14-918c-f58b520a0f2c)

![Screenshot from 2025-05-21 10-34-01](https://github.com/user-attachments/assets/c7a7adae-2d80-49ca-ae6c-3c7ee790974e)

As you can see we got the target ip address, it is online and is running windows.

# open ports scan

![Screenshot from 2025-05-21 14-36-30](https://github.com/user-attachments/assets/2392e759-b2f9-4d0a-b871-e7229dadbe57)

![Screenshot from 2025-05-21 14-37-10](https://github.com/user-attachments/assets/aa789000-04a6-430d-9def-89295da50ae0)

# lets scan for the services and vulnerabilities

![Screenshot from 2025-05-21 17-54-39](https://github.com/user-attachments/assets/80df24eb-2e84-4111-a03c-80e8b7702ef8)

![Screenshot from 2025-05-21 18-17-38](https://github.com/user-attachments/assets/369cbe1c-4081-4563-b2c2-895271589ae2)

![Screenshot from 2025-05-21 18-17-46](https://github.com/user-attachments/assets/89c65823-ca95-45a6-8cfb-e4f43ab3302b)

![Screenshot from 2025-05-21 17-54-14](https://github.com/user-attachments/assets/8a884c46-50ab-43b1-aebb-a57b4cdd22e4)

![Screenshot from 2025-05-21 18-18-54](https://github.com/user-attachments/assets/0067d582-2120-4e3e-a0aa-eacba7e0064b)

# smb enumeration

![Screenshot from 2025-05-21 19-54-40](https://github.com/user-attachments/assets/66000ae7-e589-479c-b40c-8ae3964ee9f5)


# lets see if we can any shares 

![Screenshot from 2025-05-21 19-55-04](https://github.com/user-attachments/assets/8974ce9e-cb57-4823-8ff1-e4f3842f527e)

![Screenshot from 2025-05-21 19-55-26](https://github.com/user-attachments/assets/064c6b64-1417-418b-9e78-6073011dd9c6)

# lets try to get some usernames from the domain

![Screenshot from 2025-05-22 13-00-41](https://github.com/user-attachments/assets/da370914-0762-436e-a363-4d6a9029efc2)

# lets try to bruteforce into the accont alfredo

![Screenshot from 2025-05-22 13-00-27](https://github.com/user-attachments/assets/ea7a8d72-854c-4345-a3e7-b39be489fe61)

![Screenshot from 2025-05-22 13-00-00](https://github.com/user-attachments/assets/6e369e16-719e-4feb-a4b6-5b4e67212f1c)

# lets try to map the active directory using the bloodhound

![Screenshot from 2025-05-22 19-36-06](https://github.com/user-attachments/assets/2ec03925-31af-4c3a-8cf6-5b8ea3b15651)

![Screenshot from 2025-05-22 19-41-48](https://github.com/user-attachments/assets/e86f4e6b-6c5e-463a-adc1-76a75da3a594)

Go to the link and login and change the password

Then updater the bhapi.json file

![Screenshot from 2025-05-22 19-45-22](https://github.com/user-attachments/assets/eea2bc11-b6bc-44dd-be3d-92739f689609)

# lets use  bloodhound-python to map the domain

![Screenshot from 2025-05-22 20-01-51](https://github.com/user-attachments/assets/44e230bd-faed-439e-9a6d-8ac8fc474987)

lets extract all the data we can get our hands into from the domain using the account alfredo

![Screenshot from 2025-05-22 20-05-37](https://github.com/user-attachments/assets/7732aa53-4b7c-4a2e-8c45-4847017f57af)

# lets start the bloodhound and look into the data we got our hand into

![Screenshot from 2025-05-22 20-08-06](https://github.com/user-attachments/assets/a51f7dc0-b4ea-4327-bea8-4213780ec7bd)

![Screenshot from 2025-05-22 19-50-02](https://github.com/user-attachments/assets/004816f8-30b8-4b64-a5b8-a7ffc1fff678)

log in with admin;admin and you will be prompted to change the password 

after you log into the bloodhound and upload all the data we got using bloodhound-python

![Screenshot from 2025-05-22 20-11-28](https://github.com/user-attachments/assets/2be380cd-a1fa-4b15-a740-8d8313e576dc)

![Screenshot from 2025-05-22 20-13-42](https://github.com/user-attachments/assets/922c87c0-1482-4a7b-be56-4a3374dec8c2)

![Screenshot from 2025-05-22 20-14-44](https://github.com/user-attachments/assets/bca667df-f8cf-4361-a655-d26dafc1e943)

![Screenshot from 2025-05-22 20-15-22](https://github.com/user-attachments/assets/0401f23a-2b68-4b07-9288-2a9262142aae)

![Screenshot from 2025-05-22 20-28-32](https://github.com/user-attachments/assets/948bf39b-823b-4618-b9d2-d42ff4b13544)


We found something interesting we are able to force change password from the alfredo to sysadmin which we
can use to login to the windows system.

# change the password on the sysadmin

![Screenshot from 2025-05-22 20-29-50](https://github.com/user-attachments/assets/f280483d-930e-4d54-b427-cea004125bbb)

![Screenshot from 2025-05-22 20-31-31](https://github.com/user-attachments/assets/74872910-bce4-4c3a-86f3-8ac2b43c275e)

![Screenshot from 2025-05-22 20-32-06](https://github.com/user-attachments/assets/766afbd9-40c6-44ae-b677-2f81aed7fe1b)

We have succesfully changed the password from the alfredo and used it to sign into the windows domain

# Privilege escalation

