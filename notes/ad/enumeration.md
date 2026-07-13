# External 
```
 nmap -n -sV --script "ldap* and not brute" -p 389 <DC IP>`
```

# Internal 
> Get-Module -ListAvailable -Name ActiveDirectory
> Install-WindowsFeature -Name RSAT-AD-PowerShell

```
