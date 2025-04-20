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
│ Host is up, received arp-response (0.00037s latency).
   4   │ Scanned at 2025-04-20 20:36:09 AEST for 172s
   5   │ 
   6   │ PORT      STATE SERVICE       REASON          VERSION
   7   │ 135/tcp   open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
   8   │ 139/tcp   open  netbios-ssn   syn-ack ttl 128 Microsoft Windows netbios
       │ -ssn
   9   │ 445/tcp   open  microsoft-ds? syn-ack ttl 128
  10   │ 5040/tcp  open  unknown       syn-ack ttl 128
  11   │ 8080/tcp  open  http          syn-ack ttl 128 Apache Tomcat 11.0.1
  12   │ | http-methods: 
  13   │ |_  Supported Methods: GET HEAD POST OPTIONS
  14   │ |_http-title: Apache Tomcat/11.0.1
  15   │ |_http-open-proxy: Proxy might be redirecting requests
  16   │ |_http-favicon: Apache Tomcat
  17   │ 49664/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  18   │ 49665/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  19   │ 49666/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  20   │ 49667/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  21   │ 49668/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  22   │ 49669/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  23   │ 49671/tcp open  msrpc         syn-ack ttl 128 Microsoft Windows RPC
  24   │ MAC Address: 08:00:27:FC:7E:EE (Oracle VirtualBox virtual NIC)
```
# now let's if we can find any vulnerabilities that can be exploited
```
sudo nmap --script vuln 192.168.0.59 -oN script_vuln_scan
```
We got the results of the scan
```
 Pre-scan script results:
   3   │ | broadcast-avahi-dos: 
   4   │ |   Discovered hosts:
   5   │ |     224.0.0.251
   6   │ |   After NULL UDP avahi packet DoS (CVE-2011-1002).
   7   │ |_  Hosts are all up (not vulnerable).
   8   │ Nmap scan report for 192.168.0.59
   9   │ Host is up (0.00030s latency).
  10   │ Not shown: 996 closed tcp ports (reset)
  11   │ PORT     STATE SERVICE
  12   │ 135/tcp  open  msrpc
  13   │ 139/tcp  open  netbios-ssn
  14   │ 445/tcp  open  microsoft-ds
  15   │ 8080/tcp open  http-proxy
  16   │ | http-slowloris-check: 
  17   │ |   VULNERABLE:
  18   │ |   Slowloris DOS attack
  19   │ |     State: LIKELY VULNERABLE
  20   │ |     IDs:  CVE:CVE-2007-6750
  21   │ |       Slowloris tries to keep many connections to the target web serv
       │ er open and hold
  22   │ |       them open as long as possible.  It accomplishes this by opening
│ |       the target web server and sending a partial request. By doing s
       │ o, it starves
  24   │ |       the http server's resources causing Denial Of Service.
  25   │ |       
  26   │ |     Disclosure date: 2009-09-17
  27   │ |     References:
  28   │ |       http://ha.ckers.org/slowloris/
  29   │ |_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
  30   │ | http-enum: 
  31   │ |   /manager/html/upload: Apache Tomcat (401 )
  32   │ |_  /manager/html: Apache Tomcat (401 )
  33   │ MAC Address: 08:00:27:FC:7E:EE (Oracle VirtualBox virtual NIC)
  34   │ 
  35   │ Host script results:
  36   │ |_smb-vuln-ms10-061: Could not negotiate a connection:SMB: Failed to re
       │ ceive bytes: ERROR
  37   │ |_samba-vuln-cve-2012-1182: Could not negotiate a connection:SMB: Faile
       │ d to receive bytes: ERROR
  38   │ |_smb-vuln-ms10-054: false
```

