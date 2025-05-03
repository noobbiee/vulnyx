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



As you can see i have found files in the website lets take a look into it



Looks like we got ourselves a username hope from the file 
lets try to bruteforce into the account hope

# Bruteforce the password using nxc

![Screenshot from 2025-05-02 14-51-32](https://github.com/user-attachments/assets/fcdf4b49-45d1-4765-b73d-06ac46864a6f)

![Screenshot from 2025-05-02 14-51-50](https://github.com/user-attachments/assets/82d93a3a-f612-4a00-83d4-43186a22ddd4)


