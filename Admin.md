# lets scan and try to find our target

![arp-scan](https://github.com/user-attachments/assets/681e45e7-ab0c-48c8-bc90-152bd2210410)


We have all the ip addresses in the network

lets ping and see if any targets respond

![ping](https://github.com/user-attachments/assets/c77082b2-4c6a-4e88-b38e-1dd6de486f09)


since the target responded it is alive and returned with the ttl value of 128, so it says that the target is a
windows machine

# Nmap scan
# open ports
![open_ports_scan](https://github.com/user-attachments/assets/e7610fa3-aefb-476c-9355-0b5462eeb2d0)


![Screenshot from 2025-05-02 15-00-59](https://github.com/user-attachments/assets/3e255f98-9884-41ce-863b-5adbe83bfafa)

we got all the open ports

# scv scan
![Screenshot from 2025-05-02 15-15-50](https://github.com/user-attachments/assets/04aced70-30b1-43f7-9885-b71cb7b8fc44)

![Screenshot from 2025-05-02 15-17-22](https://github.com/user-attachments/assets/70ad8698-86f4-4e9e-94ad-97364b24cbe7)

![Screenshot from 2025-05-02 15-17-41](https://github.com/user-attachments/assets/48acc45d-a230-48c0-b339-6364304b4c73)


# script vulnerability

![Screenshot from 2025-05-02 15-22-10](https://github.com/user-attachments/assets/083057c8-0718-4bad-a486-a1aa3520f3dd)


![Screenshot from 2025-05-02 15-29-38](https://github.com/user-attachments/assets/7d458517-fc18-4027-899a-dd9092450630)

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


