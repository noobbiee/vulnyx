# Scan the network and look for the ipaddress

![Screenshot from 2025-05-23 11-39-09](https://github.com/user-attachments/assets/d853c7c6-83cd-4f4b-a33a-04beb37b8fd1)

# ping the target

![Screenshot from 2025-05-23 11-39-21](https://github.com/user-attachments/assets/89b20baf-7cce-43e9-a63c-478e8ccd670e)


ttl  suggests it is a windows machine
# lets look for the open ports

![Screenshot from 2025-05-23 11-40-11](https://github.com/user-attachments/assets/77438708-e8b7-4dfe-83e4-04a13f6d0f38)

![Screenshot from 2025-05-23 11-54-18](https://github.com/user-attachments/assets/61b798b5-a7c0-4ef6-ace5-52795cb66caf)

# lets see what services are running and run some scripts against them

![Screenshot from 2025-05-23 11-57-56](https://github.com/user-attachments/assets/4407a8be-3bcd-4b90-a9be-a185686c6ca0)

![Screenshot from 2025-05-23 12-06-57](https://github.com/user-attachments/assets/8c006441-f34f-4d8d-a825-adc62bbb21bd)

![Screenshot from 2025-05-23 12-07-09](https://github.com/user-attachments/assets/35de2317-193f-44b2-aa0d-b5b069b14ba5)

# lets look up for some vulnerabilities

![Screenshot from 2025-05-23 11-57-46](https://github.com/user-attachments/assets/dff0d628-f193-4eba-8720-5cd8a937573a)

![Screenshot from 2025-05-23 12-09-13](https://github.com/user-attachments/assets/57e25747-8cd2-4e45-8e8a-ced4ae234365)

# lets try to map the smb

![Screenshot from 2025-05-23 12-15-37](https://github.com/user-attachments/assets/9ea25a02-2291-4022-8b29-1216c1534754)


# check if you can bypass smb login and access the share

![Screenshot from 2025-05-23 12-23-02](https://github.com/user-attachments/assets/9c4e4a46-79fc-4f4b-9c26-543caaaab400)

![Screenshot from 2025-05-23 12-23-14](https://github.com/user-attachments/assets/3752b00a-c612-445e-a168-8369f8abc10a)

![Screenshot from 2025-05-23 12-23-24](https://github.com/user-attachments/assets/3f0e9418-f668-466c-b6c5-b8e71da8f942)

![Screenshot from 2025-05-23 12-23-38](https://github.com/user-attachments/assets/3c30560e-c76c-43a6-9cf5-eaca3273332d)


# lets look into the web server

![Screenshot from 2025-05-23 12-27-46](https://github.com/user-attachments/assets/efc52714-e743-4caf-95d1-e3400e1e0c69)


# lets try to bruteforce using the default credentials from the metasploit

We can use metasploit to see if there are any modules that can perform login attempt 

![Screenshot from 2025-05-23 12-29-46](https://github.com/user-attachments/assets/7ed89617-abcf-4610-bab6-872884678eb7)

![Screenshot from 2025-05-23 12-30-18](https://github.com/user-attachments/assets/2d813a44-57a9-4972-9cee-119626d5e6a1)

![Screenshot from 2025-05-23 12-31-16](https://github.com/user-attachments/assets/c7ede0a8-ae20-48b3-a240-df4d1fcaea44)

![Screenshot from 2025-05-23 12-31-55](https://github.com/user-attachments/assets/3e44d513-4911-4bdf-beb3-063d3c772bd2)

As you can see we got our username and password lets log in with the username and password

![Screenshot from 2025-05-23 14-29-54](https://github.com/user-attachments/assets/27d6f05d-faa7-48ec-a8ef-58270b777053)

![Screenshot from 2025-05-23 14-30-10](https://github.com/user-attachments/assets/9abbd373-98ff-450e-a74c-549fcf82c7a7)

![Screenshot from 2025-05-23 14-30-23](https://github.com/user-attachments/assets/dca0c80b-648f-4c94-987b-3997e3ef0354)

From the information we are allowed to upload a war file, we can can try to create a reverse shell connection
using that file


# Reverse_shell using war file

'''
https://book.hacktricks.wiki/en/generic-hacking/reverse-shells/msfvenom.html
'''

![Screenshot from 2025-05-23 14-27-59](https://github.com/user-attachments/assets/c1da7165-2667-4c2a-83d7-33cecf27a27a)

![Screenshot from 2025-05-23 14-33-36](https://github.com/user-attachments/assets/564f7adf-2677-4c60-9cc5-4ad444cf31fa)

![Screenshot from 2025-05-23 14-33-58](https://github.com/user-attachments/assets/b6e83268-a87e-48b9-985b-38416d5524ed)

![Screenshot from 2025-05-23 14-34-14](https://github.com/user-attachments/assets/c6f2421a-fd62-49ad-987f-b551dd03ca37)

![Screenshot from 2025-05-23 14-35-23](https://github.com/user-attachments/assets/8ed544cc-9086-4af3-b6d7-521ef8e00d31)

![Screenshot from 2025-05-23 14-35-58](https://github.com/user-attachments/assets/732b6f5c-fa8a-4884-b464-48f82659108a)

![Screenshot from 2025-05-23 14-36-11](https://github.com/user-attachments/assets/dcc7806c-6d6a-412f-8c32-5623196c125b)

we got access into the machine



