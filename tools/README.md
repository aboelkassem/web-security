# Pentesting Tools and helper websites

## Data leaks

- [Haveibeenpwned.com](https://haveibeenpwned.com/)

## Vulnerabilities

- [exploit-db.com](http://exploit-db.com) ⇒ exploits/framework versions database archive

## Information Gathering

- [pipl.com](http://pipl.com)    //
- archive.org
- Shodan.io
- netcraft site report
- [Google search controls](https://www.makeuseof.com/tag/best-google-search-tips-pdf/)
- [Google hacking database](https://www.exploit-db.com/google-hacking-database)

## Hash finder

- [hashkiller.co.uk](https://www.researchgate.net/figure/The-rainbow-table-attack-by-http-hashkillercouk_fig2_317172584)
- https://forum.hashkiller.io/index.php?threads/insidepro-alternatives-wordlists-etc.31629/
- https://cmd5.org/
- [crackstation.net](http://crackstation.net)

## DNS

- dnschef tool ⇒ DNS cache position attack
- https://www.virustotal.com ⇒ Don’t use google DNS in your internal company
- dig
    - dig @8.8.8.8 [www.google.com](http://www.google.com) ⇒ Get the DNS records of this domain
    - dig @8.8.8.8 MX [www.google.com](http://www.google.com) ⇒ Get the MX DNS records of this domain
    - dig +noall +answer [company.com](http://company.com) A ⇒ Display only answer section in the console
    - dig +noall +answe [company.com](http://company.com) NS ⇒ DNS server
    - dig +noall +answe [company.com](http://company.com) MX ⇒ Mail Server
    - dig +noall +answe [company.com](http://company.com) ANY ⇒ get any information about the target from your custom DNS
    - dig +noall +answe @ns1.msft.net [company.com](http://company.com) ANY ⇒ ask microsoft dns server (ns1.msft.net) about any information about company.com

## Mail

- [mxtoolbox.com](http://mxtoolbox.com) ⇒ get DNS mx records

### Nmap

- Used to scan server’s ports
- commands
    - nmap [www.yahoo.com](http://www.yahoo.com) ⇒ by default scan most famous 1000 tcp ports
    - nmap -n -sn target.com ⇒ scan only ping (live IPs) not port scan
    - nmap -n -sn 192.168.43.0/24 ⇒ scan only ping (live IPs) not port scan for full network
    - nmap -iL target.txt -sn ⇒ get the live IPs (ping)
    - nmap -n -Pn -sS 192.168.43.0/24 ⇒ scan only ports not host discovery
    - nmap -n -Pn -T {0|1|2|3|4|5} 192.168.43.0/24 ⇒ scan only ports not host discovery with speed specification, default is 3, 5 is faster but not accurate
    - nmap -sT -sU [www.yahoo.com](http://www.yahoo.com) ⇒ scan famous 1000 tcp and udp ports
    - nmap -sT -sU —top-ports 2000 [www.yahoo.com](http://www.yahoo.com) ⇒ scan famous 2000 ports
    - nmap -sT -sU -p 80,443,22 [www.yahoo.com](http://www.yahoo.com) ⇒ scan only ports 80, 443, 22
    - nmap -s{S|T|U} [target.com](http://target.com) ⇒ scan type. S (SYN) first two steps in ThreeWayHandShake (preferred), T(Connect) all three steps, U(UDP)
    - nmap -sT -sU -p 1-65535 [www.yahoo.com](http://www.yahoo.com) ⇒ scan all 65535 ports
    - nmap -p 80,443 -A [www.yahoo.com](http://www.yahoo.com) ⇒ -A enable nmap to test different test cases/scenarios to know which service use this port to know more info about the service (-A = -sV(service scan) -O (OS scan) -sC (vuln scan))
    - nmap -iL target.txt ⇒ scan ports of a list of IPs at the same time
    - /usr/share/nmap/scripts ⇒ the path of common nmap scripts
    - nmap [www.yahoo.com](http://www.yahoo.com) -p 21 -A —script=ftp-brute.nse ⇒ will apply this script at this port (brute force to guess the username/password)
    - nmap -A www.yahoo.com —oA yahoo ⇒ —oA Save the output of nmap to this file
    - nmap —reason [yahoo.com](http://yahoo.com) ⇒ print reason of why this port is open or close
    - nmap —badsum [yahoo.com](http://yahoo.com) ⇒ send with bad data payload (can bypass firewall)
    - nmap -O [yahoo.com](http://yahoo.com) ⇒ OS fingerprint , know the operating system version
    - nmap -sV [yahoo.com](http://yahoo.com) ⇒ know runing applications in this host and its version
    - https://nmap.org/mailman/listinfo/fulldisclosure ⇒ subscribe to get new updated exploits

## Sqlmap

- Used for automate SQLi for GET paramters
- sqlmap -u <URL>
    - sqlmap -u “[http://test.com/users?id=2](http://192.168.1.2/sqli-labs/Less-1/?id=2)”
- If there is login redirect, you can give it your cookies
    - sqlmap -u <URL> —cookie=”<loginKeyValue>”
- if for specific paramater
    - sqlmap -u <URL> -p <injection param> [option]
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id --banner
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id --users
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id --is-dba
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id --dbs ⇒ show all databases
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id -D <databasename> --tables
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id -D <databasename> -T <table name> --column
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id -D <databasename> -T <tablename> -C <columns names> --dump
- sqlmap -u "http://192.168.1.2/sqli-labs/Less-1/?id=2" -p id --dbms=mysql ⇒ define database type
- sqlmap -u "http://192.168.1.2/sqli-labs/Less-1/?id=2" -p id --dbms=mysql --technique=UNION
- sqlmap -u "http://192.168.1.2/sqli-labs/Less-1/?id=2" -p id --dbs --dbms=mysql
- sqlmap -u "http://192.168.1.2/sqli-labs/Less-8/?id=2" -p id --technique=B --banner
- sqlmap -u "http://192.168.1.2/sqli-labs/Less-8/?id=2" -p id --technique=B --banner --dbs
- sqlmap -u “[http://192.168.1.2/sqli-labs/Less-1/?id=2”](http://192.168.1.2/sqli-labs/Less-1/?id=2%E2%80%9D) -p id --dump >> for all thing

### Metasploit

- auxiliary ⇒ some scripts for enumeration, scanning, ONSIT
- exploits ⇒ code to exploit vuln and payload example
- payloads ⇒ code to execute on the victim
- encoders ⇒ encode the payload
- post ⇒ post exploitation scripts
- nops ⇒ add nops bytes (on operation)
- evasion ⇒ scripts for evasion (bypass antivirus)
- commands
    - help
    - show {all |exploits| payloads| auxiliary}
    - search serviceName1 serviceName2 ⇒ search vsftpd
    - use moduleName ⇒ from search, you can use the module name to exploit it, you can run the following inside the module
        - show info
        - set $variable $value ⇒ set rhosts targetIP ⇒ set the hosts value to for this value to start apply this module on this host
        - exploit ⇒ start exploit
- msfvenom ⇒ create a payload
    - crea

### Nessus

- GUI

### hydra

- Used to guess username and passwords
- commands
    - hydra -L usernames.txt -P passwords.txt [ftp://www.google.com](ftp://www.google.com) ⇒ brute force attack on this target

## BurpSuite

- 

## Acunetix

- 

## netsparker

- 

## OWASP ZAP

- 

## Nikto

- 

# Fuzz directories

## Dirb

- 

## Dirsearch

- 

## gobuster

- 

## **ffuf**

- 

## Project Discovery

https://github.com/projectdiscovery

### Nuclei

- https://github.com/projectdiscovery/nuclei

## Subdomains
- [subfinder](https://github.com/projectdiscovery/subfinder)
- [assetfinder](https://github.com/tomnomnom/assetfinder)

# Books

- CISSP All-in-One Exam Guide ⇒ General Overview
- The Web Application Hacker's Handbook ⇒ beginning Web security (author of portswagger academy) ⇒ a llittle bit deprecated and old
- Browser hackers handbook ⇒ advanced Web security
- Rtfm: Red Team Field Manual ⇒ Red teaming

## SSL

- https://certbot.eff.org/ ⇒ create free SSL (Let’s encrypt)

## Helper links/tools

- [https://offsec.tools](https://offsec.tools/)
- [regex101.com](https://regex101.com/)
- [temp-mail.org](http://temp-mail.org)
