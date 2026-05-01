# Task 2: Nmap Scan Assessment - Metasploitable2This report explains the Nmap scan carried out on the Metasploitable2 virtual machine
for Task 2: Network Security & Scanning under the ApexPlanet internship program. The aim of the scan was to identify active ports, running network services, service versions, and the probable operating system of the target host.

**Target IP Address:** 192.168.56.4 (Metasploitable2 VM) 
* **Attacking Machine:** Kali Linux VM (example: 192.168.56.x)The command used for scanning was:```bashnmap -sS -sV -O 192.168.56.4
Command Explanation


-sS : Performs a TCP SYN (Stealth) Scan to quickly identify open ports.
-sV : Detects service names and version information.
-O : Attempts operating system fingerprinting.


## Raw Nmap Output

┌──(kali㉿kali)-[~]
└─$ nmap -sS -sV -O 192.168.56.4

Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-01 13:20 IST
Nmap scan report for 192.168.56.4
Host is up (0.021s latency).
Not shown: 976 closed tcp ports (reset)

PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 2.3.4
22/tcp    open  ssh         OpenSSH 4.7p1 Ubuntu
23/tcp    open  telnet      Linux telnetd
25/tcp    open  smtp        Postfix smtpd
53/tcp    open  domain      ISC BIND 9.4.2
80/tcp    open  http        Apache httpd 2.2.8
111/tcp   open  rpcbind     2
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X
445/tcp   open  microsoft-ds Samba smbd 3.X - 4.X
512/tcp   open  exec        rexecd
513/tcp   open  login
514/tcp   open  shell       rshd
1099/tcp  open  java-rmi    GNU Classpath grmiregistry
1524/tcp  open  bindshell   root shell
2049/tcp  open  nfs
2121/tcp  open  ftp         ProFTPD 1.3.1
3306/tcp  open  mysql       MySQL 5.0.51a
5432/tcp  open  postgresql  PostgreSQL 8.3.x
5900/tcp  open  vnc         VNC protocol 3.3
6000/tcp  open  X11
6667/tcp  open  irc         UnrealIRCd
8009/tcp  open  ajp13       Apache Jserv
8180/tcp  open  http        Apache Tomcat
44176/tcp open  status

MAC Address: 08:00:27:EF:74:9B (Oracle VirtualBox)
Device type: general purpose
Running: Linux 2.6.X
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop

Nmap done: 1 IP address (1 host up) scanned in 31.84 seconds


Analysis of Findings
The Nmap scan on the Metasploitable2 system successfully identified many open ports and outdated services, confirming that the machine is intentionally vulnerable for security testing.
Key Open Ports and Services:
The target system was running multiple network services. Important findings include:


Port 21 (FTP): Running vsftpd 2.3.4, a version known for a backdoor vulnerability.
Port 22 (SSH): Running OpenSSH 4.7p1, an outdated SSH service that may contain security weaknesses.
Port 23 (Telnet): Running Linux telnetd. Telnet is insecure because it sends usernames and passwords in plaintext.
Port 80 (HTTP): Running Apache 2.2.8, an old web server version vulnerable to several attacks.
Ports 139 & 445 (SMB): Samba file-sharing services were active and may allow enumeration or remote exploits.
Port 1524 (Bindshell): A root shell service was found, which is a critical security risk.
Port 3306 (MySQL): An outdated MySQL database server was running.
Port 5432 (PostgreSQL): PostgreSQL database service was also available.
Port 8180 (Tomcat): Apache Tomcat was running and may have weak default settings.


**Operating System Detection**:
Nmap identified the target as running Linux Kernel 2.6.x, which matches the known Metasploitable2 operating system.
This helps penetration testers choose relevant exploits and attack techniques.


**Security Implications**:
The system contains several outdated and insecure services such as Telnet, old FTP servers, weak SMB services, and a direct bindshell.
These weaknesses may allow attackers to:

Gain unauthorized access
Capture credentials
Exploit vulnerable services
Access databases
Obtain root shell privileges

This makes the target highly insecure and ideal for penetration testing practice.

**Conclusion**
The Nmap scan was successful in identifying the open ports, active services, and operating system details of the Metasploitable2 target machine.
The results clearly demonstrate the weak security posture of the host and provide a strong foundation for further vulnerability analysis using tools such as OpenVAS or Nessus.
