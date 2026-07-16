SMB Port open 

### Open ports
- Open ports:
  - 22
  - 21
  - 129
  - 445
### Nmap scan 
```
- Nmap Scan:
- ORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.3.4
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 10.10.17.27
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|WAP|remote management|webcam|printer
Running (JUST GUESSING): Linux 2.6.X|2.4.X (92%), Belkin embedded (90%), Control4 embedded (90%), Mobotix embedded (90%), Dell embedded (90%), Linksys embedded (90%), Tranzeo embedded (90%), Xerox embedded (90%)
OS CPE: cpe:/o:linux:linux_kernel:2.6.23 cpe:/h:belkin:n300 cpe:/o:linux:linux_kernel:2.6.30 cpe:/h:dell:remote_access_card:5 cpe:/h:linksys:wet54gs5 cpe:/h:tranzeo:tr-cpq-19f cpe:/h:xerox:workcentre_pro_265 cpe:/o:linux:linux_kernel:2.4
Aggressive OS guesses: Linux 2.6.23 (92%), Belkin N300 WAP (Linux 2.6.30) (90%), Control4 HC-300 home controller or Mobotix M22 camera (90%), Dell Integrated Remote Access Controller (iDRAC5) (90%), Dell Integrated Remote Access Controller (iDRAC6) (90%), Linksys WET54GS5 WAP, Tranzeo TR-CPQ-19f WAP, or Xerox WorkCentre Pro 265 printer (90%), Linux 2.4.21 - 2.4.31 (likely embedded) (90%), Linux 2.4.7 (90%), Citrix XenServer 5.5 (Linux 2.6.18) (90%), Linux 2.6.18 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 2h00m16s, deviation: 2h49m43s, median: 15s
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: lame
|   NetBIOS computer name: 
|   Domain name: hackthebox.gr
|   FQDN: lame.hackthebox.gr
|_  System time: 2026-07-16T16:25:20-04:00
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   85.46 ms  10.10.16.1
2   130.69 ms 10.129.30.74
```
