# Scans
##  Nmap Scan 
```
53/tcp   open  domain       Simple DNS Plus
88/tcp   open  kerberos-sec Microsoft Windows Kerberos (server time: 2026-07-17 15:49:51Z)
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=7/17%OT=53%CT=1%CU=37523%PV=Y%DS=2%DC=T%G=Y%TM=6A5A4DB
OS:6%P=aarch64-unknown-linux-gnu)SEQ(TI=RI%TS=A)SEQ(SP=101%GCD=1%ISR=100%TI
OS:=I%CI=RD%II=I%SS=S%TS=A)SEQ(SP=102%GCD=1%ISR=10D%TI=I%CI=RD%TS=A)SEQ(SP=
OS:107%GCD=1%ISR=10C%TI=I%CI=I%II=I%SS=S%TS=A)SEQ(SP=107%GCD=1%ISR=10E%TI=I
OS:%CI=I%II=I%SS=S%TS=A)OPS(O1=M542NW8ST11%O2=M542NW8ST11%O3=M542NW8NNT11%O
OS:4=M542NW8ST11%O5=M542NW8ST11%O6=M542ST11)WIN(W1=2000%W2=2000%W3=2000%W4=
OS:2000%W5=2000%W6=2000)ECN(R=N)ECN(R=Y%DF=Y%T=80%W=2000%O=M542NW8NNS%CC=Y%
OS:Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T2(R=Y%DF=Y%T=80%W=0%S=
OS:Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=
OS:Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=A
OS:R%O=%RD=0%Q=)T6(R=N)T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=N)T
OS:7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=N)U1(R=Y%DF=N%T=80%IPL
OS:=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=80%CD=Z)

Network Distance: 2 hops
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
|_clock-skew: mean: 2h26m35s, deviation: 4h02m30s, median: 6m34s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2026-07-17T08:50:11-07:00
| smb2-time: 
|   date: 2026-07-17T15:50:12
|_  start_date: 2026-07-17T15:47:54

TRACEROUTE (using port 21/tcp)
HOP RTT      ADDRESS
1   72.17 ms 10.10.16.1
2   72.19 ms 10.129.95.210
```

## Nuclei-scan 
- Was unsuccessful, twice 
## Rustscan 
```
53/tcp    open  domain           syn-ack
88/tcp    open  kerberos-sec     syn-ack
135/tcp   open  msrpc            syn-ack
139/tcp   open  netbios-ssn      syn-ack
389/tcp   open  ldap             syn-ack
445/tcp   open  microsoft-ds     syn-ack
464/tcp   open  kpasswd5         syn-ack
593/tcp   open  http-rpc-epmap   syn-ack
636/tcp   open  ldapssl          syn-ack
3268/tcp  open  globalcatLDAP    syn-ack
3269/tcp  open  globalcatLDAPssl syn-ack
5985/tcp  open  wsman            syn-ack
9389/tcp  open  adws             syn-ack
47001/tcp open  winrm            syn-ack
49664/tcp open  unknown          syn-ack
49665/tcp open  unknown          syn-ack
49666/tcp open  unknown          syn-ack
49668/tcp open  unknown          syn-ack
49671/tcp open  unknown          syn-ack
49680/tcp open  unknown          syn-ack
49681/tcp open  unknown          syn-ack
49685/tcp open  unknown          syn-ack
49700/tcp open  unknown          syn-ack

Read data files from: /home/linuxbrew/.linuxbrew/Cellar/nmap/7.99/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.18 seconds
```
# Notes 
- running windows server 2016
- may be vulnerable to ms-10?
- unable to connect it sems like to http website; not public facing
- LDAp can be used to find crucial information about a domain without authentication
- Guided activity says that ldap allows for anonymous authentication can provide valuable information about the machine. Need to take notes on that was not covered or I just didn't take notes on it
```
ldapsearch -x -H ldap://10.129.95.210 -b "dc=htb,dc=local" "(objectClass=person)" #if domain is htb.local, you split it in two so that one dc is equal to the first part and hte other is equal to the second part 
```
# Exploit Information & Links 
Cntrl+D to stop recording
```
vulnx search windows server 2016 smb
```
```
vulnx search windows server 2016 --poc
```
## CVE-2017-0147 
```
CVE-2017-0147] High - Microsoft Windows SMB - Information Disclosure
  ↳ Priority: IMMEDIATE | EXPLOITS AVAILABLE | Vuln Age: 3409d
  ↳ CVSS: 7.5 | EPSS: 0.9969 (HIGH) | KEV: ✔ (CISA, VULNCHECK)
  ↳ Patch: ✔ | POCs: 9 | Template: ✘ | HackerOne: ✘

Summary 📝
  ↳ Microsoft Windows Vista SP2, Windows Server 2008 SP2 and R2 SP1, Windows 7 SP1, Windows 8.1, Windows Server 2012 Gold and R2, Windows RT 8.1, Windows 10 versions, and Windows Server 2016 contain an information disclosure caused by crafted SMBv1 packets, letting remote attackers retrieve sensitive information from process memory, exploit requires network access.

Risk ⚠️
  ↳ Remote attackers can retrieve sensitive information from process memory, potentially leading to further exploits or data breaches.

Remediation 🔧
  ↳ Disable SMBv1 or update to a version with the fix, and consider applying security patches provided by Microsoft.

POCs 🔍
  → http://packetstormsecurity.com/files/156196/SMB-DOUBLEPULSAR-Remote-Code-Execution.html
        (nvd)
  → https://www.exploit-db.com/exploits/41891/ (nvd)
  → https://github.com/RobertoLeonFR-ES/Exploit-Win32.CVE-2017-0147.A (gh-nomi-sec)
  → http://packetstormsecurity.com/files/154690/DOUBLEPULSAR-Payload-Execution-Neutralization.html
        (nvd)
  → https://www.exploit-db.com/exploits/41987/ (nvd)
  → +4 more...

References 📚
  → https://www.ivanti.com/resources/v/doc/pr-survey-report/ransomware-quarterly-indexreport_q2-q3
        (vulncheck)
  → http://packetstormsecurity.com/files/154690/DOUBLEPULSAR-Payload-Execution-Neutralization.html
        (nvd)
  → https://cert-portal.siemens.com/productcert/pdf/ssa-966341.pdf (nvd)
  → https://www.enisa.europa.eu/sites/default/files/2025-10/ENISA%20Threat%20Landscape%202025.pdf
        (vulncheck)
  → https://www.cyfirma.com/research/apt-profile-mission2025/ (vulncheck)
  → +15 more...

Affected Products 🎯
  → windows_7 (microsoft)
  → windows_server_2012 (microsoft)
  → acuson_x700_firmware (siemens)
  → syngo_sc2000_firmware (siemens)
  → versant_kpcr_molecular_system_firmware (siemens)
  → +5 more...─────────────────────────────────────────────────────────────────
```
# Checklist 
- Check for public facing ports
http://10.129.95.210:5985/ # unresponsive
http://10.129.95.210:53 # unresponsive 
# Time to completion
- 2 + hours
- Needed write up?
Yes, for ldap enumeration and privilege escalation
