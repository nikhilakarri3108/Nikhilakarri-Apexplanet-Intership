Passive Reconnaissance:
Passive reconnaissance involves gathering information without directly interacting with the target's systems. This information is publicly available.

Whois: A command-line tool used to query a public database for information about a domain, such as the owner, contact details, and registration dates.

How to use:

┌──(kali㉿kali)-[~]
└─$ whois google.com

Domain Name: GOOGLE.COM
Registry Domain ID: 2138514_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.markmonitor.com
Registrar URL: http://www.markmonitor.com
Updated Date: 2026-04-30T12:15:22Z
Creation Date: 1997-09-15T04:00:00Z
Registry Expiry Date: 2028-09-14T04:00:00Z
Registrar: MarkMonitor Inc.
Registrar IANA ID: 292
Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
Registrar Abuse Contact Phone: +1.2086851750
Domain Status: clientDeleteProhibited
Domain Status: clientTransferProhibited
Domain Status: clientUpdateProhibited
Domain Status: serverDeleteProhibited
Domain Status: serverTransferProhibited
Domain Status: serverUpdateProhibited
Name Server: NS1.GOOGLE.COM
Name Server: NS2.GOOGLE.COM
Name Server: NS3.GOOGLE.COM
Name Server: NS4.GOOGLE.COM


Nslookup: A tool used to query DNS records such as domain IP address, MX records, and name servers.

How to use:

┌──(kali㉿kali)-[~]
└─$ nslookup google.com

Server:         49.205.72.130
Address:        49.205.72.130#53

Non-authoritative answer:
Name:   google.com
Address: 142.250.183.174
Address: 2404:6800:4007:815::200e


Google Dorking: A technique that uses advanced Google search operators to discover hidden files, login pages, open directories, or sensitive information indexed by search engines.

Examples:
site:example.com filetype:pdf
intitle:"index of"
inurl:admin login


Shodan: A search engine for internet-connected devices that helps find public servers, webcams, routers, IoT devices, and exposed services.

Website:
https://www.shodan.io


Active Reconnaissance: Direct interaction with the target system or network to collect information.

Examples:
- Port Scanning
- Ping Sweep
- Banner Grabbing
- Service Enumeration

Ping Sweep: Sending ICMP echo requests to a subnet range to identify live hosts.

How to use:

┌──(kali㉿kali)-[~]
└─$ nmap -sn 192.168.56.0/24
Starting Nmap 7.94
Nmap scan report for 192.168.56.1
Host is up
Nmap scan report for 192.168.56.101
Host is up

Nmap done: 256 IP addresses (2 hosts up) scanned

Banner Grabbing: Connecting to a service and reading its banner to identify software name/version.

How to use:

┌──(kali㉿kali)-[~]
└─$ nc -nv scanme.nmap.org 80
(UNKNOWN) [45.33.32.156] 80 (http) open
HTTP/1.1 400 Bad Request
Server: nginx
