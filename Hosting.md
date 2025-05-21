# Lets Scan our local network using arp-scan

![Screenshot from 2025-05-16 18-44-47](https://github.com/user-attachments/assets/8f738f0b-fcfa-45b2-929b-d044bec5f2d6)


# lets ping and determine our target

![Screenshot from 2025-05-16 18-45-02](https://github.com/user-attachments/assets/d14caa4d-e8ef-4278-95ec-63fc8271e6c6)

# lets check for openports
![Screenshot from 2025-05-16 18-55-56](https://github.com/user-attachments/assets/20fdb8e3-6a54-44f6-a1de-d0e26169d693)

![Screenshot from 2025-05-16 18-56-12](https://github.com/user-attachments/assets/445dc343-ce1a-4902-a2c5-3e8ac626ba80)

# lets check what services are running in the openports, version of those services and run default nmap scripts

![Screenshot from 2025-05-16 19-03-32](https://github.com/user-attachments/assets/d233fbbe-939b-4fce-b7dc-81039968f1b0)

![Screenshot from 2025-05-16 19-19-36](https://github.com/user-attachments/assets/a25b66f3-3cae-413d-82b3-12c9c32be0bc)

![Screenshot from 2025-05-16 19-19-49](https://github.com/user-attachments/assets/3b9762d2-2351-4f7a-a790-233372fd9412)

# lets scan for vulnerabilities

![Screenshot from 2025-05-16 19-21-19](https://github.com/user-attachments/assets/5e661dd9-489a-4741-a7a8-bbd74f664362)

![Screenshot from 2025-05-16 19-21-37](https://github.com/user-attachments/assets/60936fd7-50f3-4c7a-964c-f7abd161fa17)

# lets see what is running in the web-server

![Screenshot from 2025-05-19 14-25-09](https://github.com/user-attachments/assets/8cfa3e9a-f6af-4dc9-966f-0e34bf074071)

# lets scan for web vulnerablilites using nikto

![Screenshot from 2025-05-19 14-25-23](https://github.com/user-attachments/assets/95a7d967-13b5-474b-b3e3-6fef2cf00f04)

# lets bruteforce some directories

![Screenshot from 2025-05-19 14-36-30](https://github.com/user-attachments/assets/a7a31f8f-db6f-49ea-b28a-f987c60bcff9)

# lets check the directory that we got while bruteforcing

![Screenshot from 2025-05-19 16-03-45](https://github.com/user-attachments/assets/c95a0560-ca34-4ec0-9724-3a75be998838)

lets take all the members username on the email that they have, we can also save the email for phising
attack

![Screenshot from 2025-05-19 16-06-28](https://github.com/user-attachments/assets/f2d1f572-4e5b-4bc3-9ccb-9cfb4a7f017e)

# lets try to bruteforce the password of the users that we got

![Screenshot from 2025-05-19 16-08-51](https://github.com/user-attachments/assets/e57bfa44-c0dc-4cdf-9df4-f37f9574db4f)

![Screenshot from 2025-05-19 16-09-07](https://github.com/user-attachments/assets/0f3e1367-b510-42ad-a569-8573739c9d91)

# lets log in using the password that we got and see all the shares and users in the smb

![Screenshot from 2025-05-19 18-47-45](https://github.com/user-attachments/assets/257cff8d-8d00-4dd8-be86-c34e4519e9f3)

As you can see we got new users we can copy it into our users list. we also can see there is a description written in
whgich we can use to try and log in.
lets see if the description is the password for any of the users that we got

![Screenshot from 2025-05-20 11-56-04](https://github.com/user-attachments/assets/1fbfc29b-d299-48b8-893d-96f09c9fbeee)

now we got the username and password

# lets log in using the evil-winrm

![Screenshot from 2025-05-20 11-58-02](https://github.com/user-attachments/assets/0f6f9ac4-1f37-42e8-a549-1d6e225932ca)

# lets check for the permissions on this account

![Screenshot from 2025-05-20 12-06-12](https://github.com/user-attachments/assets/cf660fb7-db89-457c-aeb0-ed51539b973d)

We can see the all the permissions on this account, use the availoable translator to view the permissions.
# SebackupPrivilege
Please refer to the link below for further explanation of the SebackupPrivilige

'''
https://github.com/nickvourd/Windows-Local-Privilege-Escalation-Cookbook/blob/master/Notes/SeBackupPrivilege.md
'''

# Privilege escalation
We will need to get access to access the registry where the hashes are stored. normally we are not able to access it
but due to the sebackupprivilige enabled we can access the reistry and save it in a file and export it and use to pass
the hash.

![Screenshot from 2025-05-20 12-47-26](https://github.com/user-attachments/assets/6be91376-4d5b-4f91-bde2-447ac3303187)

![Screenshot from 2025-05-20 14-06-30](https://github.com/user-attachments/assets/392a9254-5218-4dbf-a5ce-e76492895b10)

![Screenshot from 2025-05-20 14-06-02](https://github.com/user-attachments/assets/43f675db-b404-4b84-8263-dba056a48191)

![Screenshot from 2025-05-20 14-14-59](https://github.com/user-attachments/assets/1242d2e9-d13b-4ff5-99d7-b6b12ce97961)
