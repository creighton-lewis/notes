# Subdomain
### Enumeration 
## Kerbrute 
- Download
- Rename
- Move to bin so it can be ran anywhere
```
mv kerberute_vers kerberute
chmod +x kerberute 
sudo mv kerbrute /usr/local/bin
```
## Subfinder 
```
subfinder -d website.com -o site.com 
```
```
ffuf -H "Host: FUZZ.titanic.htb" -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt -u http://10.129.31.123
```
### Exploitation 
# Directories 
```

ffuf -w usr/share/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt  -u http://$ip 
ffuf -w usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt  -u http://$ip 
ffuf -w usr/share/seclists/Discovery/Web-Content/small-medium-directories-lowercase.txt  -u http://$ip 
ffuf -w /usr/share/seclists/DirBuster-2007_directory-list-2.3-big.txt -u http://$ip 
ffuf -w /Discovery/Web-Content/DirBuster-2007_directory-list-lowercase-2.3-big.txt  -u http://$ip 
```

