# lets scan and try to find our target

![arp-scan](https://github.com/user-attachments/assets/e5e4f865-1a97-4d9d-822f-a3ba2b101c14)



We have all the ip addresses in the network

lets ping and see if any targets respond
![ping](https://github.com/user-attachments/assets/3604ee9b-569e-4084-8bf4-7074f1e16c25)



since the target responded it is alive and returned with the ttl value of 128, so it says that the target is a
windows machine

# Nmap scan
# open  ports

![Screenshot from 2025-05-03 10-01-24](https://github.com/user-attachments/assets/6ca82070-9162-40a4-b52e-658c3b4ed75c)

![Screenshot from 2025-05-03 10-07-42](https://github.com/user-attachments/assets/bcbf99ea-2157-412a-a896-9f4d5a3fd035)



we got all the open ports

# scv scan
![Screenshot from 2025-05-03 10-03-57](https://github.com/user-attachments/assets/346186e8-8b7e-4ff0-b001-5ac7b9d591db)

![Screenshot from 2025-05-03 10-06-12](https://github.com/user-attachments/assets/669824df-048e-47a0-b6a9-c1e25b4759ef)

![Screenshot from 2025-05-03 10-06-23](https://github.com/user-attachments/assets/058cf2c2-bed9-4e65-a6e4-f5fb092148f7)



# script vulnerability

![Screenshot from 2025-05-03 10-23-31](https://github.com/user-attachments/assets/89b2f4e6-a3d9-491e-8a76-f16010298a0e)


# lets check if we can access the smb without username and password
![Screenshot from 2025-05-03 10-28-04](https://github.com/user-attachments/assets/a50633e4-2f85-4078-ae00-2d3b56d4b904)

![Screenshot from 2025-05-03 10-28-16](https://github.com/user-attachments/assets/b5f260dd-fa39-4a7a-89c5-9d6942d84bb6)

![Screenshot from 2025-05-03 10-28-36](https://github.com/user-attachments/assets/ea17b08c-48db-4d02-b3f3-2b1e35cc6ef2)

![Screenshot from 2025-05-03 10-28-50](https://github.com/user-attachments/assets/28c96074-9115-4422-9f1d-a6949498258f)

![Screenshot from 2025-05-03 10-29-05](https://github.com/user-attachments/assets/9fbf4866-f76d-4a0b-a657-b2299dbb45ea)


# lets take a look into the port 80

![Screenshot from 2025-05-03 10-33-03](https://github.com/user-attachments/assets/ffa60ac2-b232-418f-9d9b-b8dde4f726c0)

![Screenshot from 2025-05-03 10-30-55](https://github.com/user-attachments/assets/63999672-cf80-46e3-aa3b-961548c9be66)


# now lets try to see if we can bruteforce some of the directories/files in the websites

![Screenshot from 2025-05-03 10-47-08](https://github.com/user-attachments/assets/a048f341-c33f-4eb6-a814-dd9d8334b752)


As you can see i have found files in the website lets take a look into it

![Screenshot from 2025-05-03 10-47-50](https://github.com/user-attachments/assets/220e6034-9737-432f-8ce8-d1c345d0d2e9)



Looks like we got ourselves a username hope from the file 
lets try to bruteforce into the account hope

# Bruteforce the password using nxc

![Screenshot from 2025-05-03 10-50-28](https://github.com/user-attachments/assets/bfd09bc8-4a47-4a57-a670-06f63106ff10)

![Screenshot from 2025-05-03 10-50-45](https://github.com/user-attachments/assets/c2097799-d1b1-4c86-ab27-e268dfc45a6f)

We were able to get the password to the account hope
lets check the username and password
evil
![Screenshot from 2025-05-03 12-49-26](https://github.com/user-attachments/assets/9d95e0dd-9626-4dcc-8123-93bbcfbf5042)

# logging into the user account
# evil-winrm

![Screenshot from 2025-05-03 12-52-51](https://github.com/user-attachments/assets/89c831e3-7a35-4b19-9aca-6db9ce1411e5)

![user_flag](https://github.com/user-attachments/assets/8769221c-6631-4596-9e1d-fff2a506d9e2)


We have successfully got the flags for the user 
lets try to see if we have access to the administrator account

![Screenshot from 2025-05-03 12-56-41](https://github.com/user-attachments/assets/df4f9c6d-b4d6-407b-b3e2-7d7bd5f717f2)

we can get into the directory but we dont have any permissions. lets try to escalate our privilege

# Privilege escalation

We will use the winpeas.bat and execute it for privilige escaltion
```
https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS/winPEASbat
```
i will clone the repo and use it 
The script looks for possible way to escalate privilege windows host. the details explanation on how it works are provided in the 
```
https://book.hacktricks.wiki/en/windows-hardening/windows-local-privilege-escalation/integrity-levels.html
```

![Screenshot from 2025-05-03 13-03-58](https://github.com/user-attachments/assets/ab8b92a0-4fbe-4640-b2f2-bd8f5cca5738)

move the script in your working directory where you started the evil-winrm
you can upload it and execute in the window host

![Screenshot from 2025-05-03 13-07-01](https://github.com/user-attachments/assets/b1cac7d6-0e8a-4f6c-b2a1-2a3564fc6022)

Since the output is on the spanish we will need to translate it. i translated the output using chatgpt
use the resources at your disposal.

![Screenshot from 2025-05-03 13-10-07](https://github.com/user-attachments/assets/a77598c9-ae37-42c1-ba43-5400e58d4a89)

lets try to navigate into the directory to view the file.

![Screenshot from 2025-05-03 13-12-45](https://github.com/user-attachments/assets/12b19876-dc40-4e58-9423-a3f964ed12d7)


We found some information that are very interesting. we got the username and password for the administrator account
Lets try to log in to the account using the credentials we got in our hands

![Screenshot from 2025-05-03 13-25-15](https://github.com/user-attachments/assets/2aa142b8-4b7d-4ef9-8a7e-b7c22fab02c6)

we can navigate and get our hands into the flags

![admin_flag](https://github.com/user-attachments/assets/7d81062c-e948-48fd-bd9c-21581206d897)



![Screenshot from 2025-05-03 13-27-55](https://github.com/user-attachments/assets/9da09871-a3f8-4a7b-ab97-685b26522d1b)

![admin_flag2](https://github.com/user-attachments/assets/6db33c2a-68a3-4973-b37a-6301bcc979f1)


We have successfully been able to compromise our host and performed data exfiltration. 


