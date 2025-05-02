# lets scan and try to find our target

![arp-scan](https://github.com/user-attachments/assets/088f841f-7c3a-4619-9b22-edceb41861b8)

We have all the ip addresses in the network

lets ping and see if any targets respond

![ping](https://github.com/user-attachments/assets/420d4c23-3d29-4575-9a43-864a11dad9d8)

since the target responded it is alive and returned with the ttl value of 128, so it says that the target is a
windows machine

# Nmap scan
# open ports
![Screenshot from 2025-05-01 18-54-58](https://github.com/user-attachments/assets/733ab5dd-dc89-46b9-98a4-6dbec9319693)

![Screenshot from 2025-05-01 18-56-32](https://github.com/user-attachments/assets/d5627ba2-b738-4604-ab8d-1e7a20f131fb)

we got all the open ports

# scv scan
![scv](https://github.com/user-attachments/assets/742efe0e-1fa5-4c6b-b2f0-cbcdb2b5e76d)

![Screenshot from 2025-05-01 20-54-40](https://github.com/user-attachments/assets/e4cbd540-52ff-4035-89c6-545fbe872f40)

![Screenshot from 2025-05-01 20-55-01](https://github.com/user-attachments/assets/1d91506b-3bea-4ed6-b41b-9e1ff8f7b346)


# script vulnerability

![script_vuln](https://github.com/user-attachments/assets/6b6c6756-7ad0-4165-84a6-636bdd85cffa)

![Screenshot from 2025-05-01 20-59-19](https://github.com/user-attachments/assets/c834cecf-a4a9-4d90-9f06-b162deafc0f5)

# lets check if we can access the smb without username and password

![Screenshot from 2025-05-02 10-48-53](https://github.com/user-attachments/assets/c08074b8-92bf-461f-ab1f-21b8f7e3cff1)

![Screenshot from 2025-05-02 10-49-07](https://github.com/user-attachments/assets/ba72ec21-1b8f-4223-b3e4-0eed704d87d5)

![Screenshot from 2025-05-02 10-49-17](https://github.com/user-attachments/assets/46f84e33-051d-4f9e-82b6-5c2663c64c27)

![Screenshot from 2025-05-02 10-49-27](https://github.com/user-attachments/assets/8c3153bb-46b4-452b-9d27-0571f474b0ae)

# lets take a look into the port 80

![Screenshot from 2025-05-02 11-09-27](https://github.com/user-attachments/assets/a714c7e5-83a7-4994-abd9-b66633c8f76a)

![Screenshot from 2025-05-02 10-52-12](https://github.com/user-attachments/assets/431fb516-4d1f-4927-8983-74d0f79cbaa5)

# now lets try to see if we can bruteforce some of the directories/files in the websites

![Screenshot from 2025-05-02 11-40-20](https://github.com/user-attachments/assets/0749538e-1d0c-4531-aa7d-9b13d27ce14f)

As you can see i have found files in the website lets take a look into it

![Screenshot from 2025-05-02 11-43-19](https://github.com/user-attachments/assets/df4aa0b2-227d-4811-9c1d-51bc9e1a6722)

Looks like we got ourselves a username hope from the file 
lets try to bruteforce into the account hope

# Bruteforce the password using nxc

![Screenshot from 2025-05-02 14-51-32](https://github.com/user-attachments/assets/fcdf4b49-45d1-4765-b73d-06ac46864a6f)

![Screenshot from 2025-05-02 14-51-50](https://github.com/user-attachments/assets/82d93a3a-f612-4a00-83d4-43186a22ddd4)


