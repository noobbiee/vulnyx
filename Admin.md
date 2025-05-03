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

![Screenshot from 2025-05-02 16-25-09](https://github.com/user-attachments/assets/a9040c69-c9dc-4fa2-b511-0d0aa7e30108)

![Screenshot from 2025-05-02 16-47-04](https://github.com/user-attachments/assets/8f2961b3-c5a3-478f-9072-7510cd850d01)

![Screenshot from 2025-05-02 16-47-37](https://github.com/user-attachments/assets/4ed5a57c-d7c5-4aa1-84eb-342b7561ae73)

![Screenshot from 2025-05-02 16-48-10](https://github.com/user-attachments/assets/0282f645-899e-4d5b-bd6d-c07c67d7a4fd)

![Screenshot from 2025-05-02 16-48-43](https://github.com/user-attachments/assets/e7b0cd18-c875-4acf-b7e4-69a04503b4e8)


# lets take a look into the port 80

![Screenshot from 2025-05-02 16-52-14](https://github.com/user-attachments/assets/2bee1c30-0f48-4b69-93b3-00b2f3968193)


![Screenshot from 2025-05-02 16-53-52](https://github.com/user-attachments/assets/4a52c65a-343c-42f3-87ff-604efaf8fb34)



# now lets try to see if we can bruteforce some of the directories/files in the websites
![Screenshot from 2025-05-02 16-57-35](https://github.com/user-attachments/assets/7b4e3d84-9856-47c4-bb62-adbf34d1bce0)


As you can see i have found files in the website lets take a look into it
![Screenshot from 2025-05-02 16-58-05](https://github.com/user-attachments/assets/309f1224-adb9-436b-b9f2-9740c1eee25b)


Looks like we got ourselves a username hope from the file 
lets try to bruteforce into the account hope

# Bruteforce the password using nxc

![Screenshot from 2025-05-02 14-51-32](https://github.com/user-attachments/assets/fcdf4b49-45d1-4765-b73d-06ac46864a6f)

![Screenshot from 2025-05-02 14-51-50](https://github.com/user-attachments/assets/82d93a3a-f612-4a00-83d4-43186a22ddd4)


