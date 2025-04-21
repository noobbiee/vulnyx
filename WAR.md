# the machine is at:
https://vulnyx.com/#war

# First of all we have to find the ip-address of our target machine
```
sudo arp-scan -I eth0 --localnet --ignoredups
```
we will get all the ip address in our localnet
```
sudo arp-scan -I eth0 --localnet --ignoredups
Interface: eth0, type: EN10MB, MAC: 08:00:27:82:1c:68, IPv4: 192.168.0.58
Starting arp-scan 1.10.0 with 256 hosts (https://github.com/royhills/arp-scan)
192.168.0.1	80:20:da:72:ff:d2	Sagemcom Broadband SAS
192.168.0.8	02:0f:b5:4a:c5:3c	(Unknown: locally administered)
192.168.0.18	68:54:5a:4c:27:b9	Intel Corporate
192.168.0.2	bc:14:ef:ed:09:cb	ITON Technology Limited
192.168.0.3	d4:f5:47:89:0e:44	Google, Inc.
192.168.0.16	44:27:45:51:57:76	(Unknown)
192.168.0.56	08:00:27:ea:bb:98	PCS Systemtechnik GmbH
192.168.0.59	08:00:27:fc:7e:ee	PCS Systemtechnik GmbH

9 packets received by filter, 0 packets dropped by kernel
Ending arp-scan 1.10.0: 256 hosts scanned in 2.009 seconds (127.43 hosts/sec). 8 responded
```
now we can ping and check our target 
```
ping -c 1 192.168.0.59
```
we got response from the target
```
ping -c 1 192.168.0.59
PING 192.168.0.59 (192.168.0.59) 56(84) bytes of data.
64 bytes from 192.168.0.59: icmp_seq=1 ttl=128 time=0.401 ms

--- 192.168.0.59 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.401/0.401/0.401/0.000 ms
```
From the scan ttl=128 we found the target is the windows machine

# Open ports
We use the nmap to check all the open ports on the system
```
sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.0.59 -oN openports
```
we will save the openports on the file openports
```
 Some closed ports may be reported as filtered due to --defeat-rst-ratel
       │ imit
   7   │ PORT      STATE SERVICE      REASON
   8   │ 135/tcp   open  msrpc        syn-ack ttl 128
   9   │ 139/tcp   open  netbios-ssn  syn-ack ttl 128
  10   │ 445/tcp   open  microsoft-ds syn-ack ttl 128
  11   │ 5040/tcp  open  unknown      syn-ack ttl 128
  12   │ 8080/tcp  open  http-proxy   syn-ack ttl 128
  13   │ 49664/tcp open  unknown      syn-ack ttl 128
  14   │ 49665/tcp open  unknown      syn-ack ttl 128
  15   │ 49666/tcp open  unknown      syn-ack ttl 128
  16   │ 49667/tcp open  unknown      syn-ack ttl 128
  17   │ 49668/tcp open  unknown      syn-ack ttl 128
  18   │ 49669/tcp open  unknown      syn-ack ttl 128
  19   │ 49671/tcp open  unknown      syn-ack ttl 128
  20   │ MAC Address: 08:00:27:FC:7E:EE (Oracle VirtualBox virtual NIC)
  21   │ 
  22   │ Read data files from: /usr/share/nmap
```
# lets check the services and versions running on those open ports
```
sudo nmap -sCV -p 135,139,445,5040,8080,49664,49665,49666,49667,49668,49669,49671 -vvv 192.168.0.59 -oN service_scan
```
we got the services and versions running on the ports
```
 │ Host is up, received arp-response (0.00064s latency).
   4   │ Scanned at 2025-04-21 15:46:54 AEST for 171s
   5   │ 
   6   │ PORT      STATE  SERVICE       REASON          VERSION
   7   │ 135/tcp   open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
   8   │ 139/tcp   open   netbios-ssn   syn-ack ttl 128 Microsoft Windows netbios-ssn
   9   │ 445/tcp   open   microsoft-ds? syn-ack ttl 128
  10   │ 5040/tcp  open   unknown       syn-ack ttl 128
  11   │ 8080/tcp  open   http          syn-ack ttl 128 Apache Tomcat (language: en)
  12   │ | http-methods: 
  13   │ |_  Supported Methods: GET HEAD POST OPTIONS
  14   │ |_http-favicon: Apache Tomcat
  15   │ |_http-title: Apache Tomcat/11.0.1
  16   │ 49664/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  17   │ 49665/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  18   │ 49666/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  19   │ 49667/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  20   │ 49668/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  21   │ 49669/tcp open   msrpc         syn-ack ttl 128 Microsoft Windows RPC
  22   │ 49671/tcp closed unknown       reset ttl 128
  23   │ MAC Address: 08:00:27:FC:7E:EE (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
  24   │ Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
│ Host script results:
  27   │ | p2p-conficker: 
  28   │ |   Checking for Conficker.C or higher...
  29   │ |   Check 1 (port 48853/tcp): CLEAN (Couldn't connect)
  30   │ |   Check 2 (port 42406/tcp): CLEAN (Couldn't connect)
  31   │ |   Check 3 (port 54068/udp): CLEAN (Timeout)
  32   │ |   Check 4 (port 64330/udp): CLEAN (Failed to receive data)
  33   │ |_  0/4 checks are positive: Host is CLEAN or ports are blocked
  34   │ | smb2-security-mode: 
  35   │ |   3:1:1: 
  36   │ |_    Message signing enabled but not required
  37   │ |_clock-skew: -10s
  38   │ | smb2-time: 
  39   │ |   date: 2025-04-21T05:49:20
  40   │ |_  start_date: N/A
  41   │ | nbstat: NetBIOS name: WAR, NetBIOS user: <unknown>, NetBIOS MAC: 08:00:27:fc:7e:ee (PCS Systemtechn
       │ ik/Oracle VirtualBox virtual NIC)
  42   │ | Names:
  43   │ |   WAR<00>              Flags: <unique><active>
  44   │ |   WORKGROUP<00>        Flags: <group><active>
  45   │ |   WAR<20>              Flags: <unique><active>
  46   │ | Statistics:
  47   │ |   08:00:27:fc:7e:ee:00:00:00:00:00:00:00:00:00:00:00
  48   │ |   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
  49   │ |_  00:00:00:00:00:00:00:00:00:00:00:00:00:00
  50   │ 
  51   │ Read data files from: /usr/share/nmap

```
# lets look into the smb 
lets check if smbv1 is enabled, if enabled we can exploit using eternalblue
```
nxc smb 192.168.0.59
SMB         192.168.0.59    445    WAR              [*] Windows 10 / Server 2019 Build 19041 x64 (name:WAR) (domain:WAR) (signing:False) (SMBv1:False)
```
now lets check if we can access any shares into smb without loging in
 -N, --no-pass                                Don't ask for a password
 -L, --list=HOST                              Get a list of shares available on a host
```
smbclient -NL 192.168.0.59
session setup failed: NT_STATUS_ACCESS_DENIED
```
```
smbmap --no-banner -H 192.168.0.59
[\] Checking for open ports...                                                                                [*] Detected 1 hosts serving SMB
[|] Authenticating...                                                                                         [*] Established 1 SMB connections(s) and 0 authenticated session(s)
[!] Something weird happened on (192.168.0.59) Error occurs while reading from remote(104) on line 1015
[/] Closing connections..                                                                                     [-] Closing connections..                                                                                     [\] Closing connections..                                                                                     [|] Closing connections..                                                                                     [/] Closing connections..                                                                                     [-] Closing connections..                                                                                     [*] Closed 1 connections                                                                            
```
                       

