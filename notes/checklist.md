# 1. Enumeration 
## 1.1 
- Run nmap scan
- Run rustscan scan
- Run nuclei scan
- Run subdomain scan for ffuf
## 1.2 
- Navigate to each site in browser
- Utilize http and https 
- Attempt to crawl the web application
- Run full scan with owasp zap 
- Record what ports are open and technologies used
- Use vulnx to determine if there are any useful vulnerabilities that exist for system
## 1.3 A
- If application is web application
- Find out if files can be uploaded. If file can be uploaded
- Find out if there are any vulnerable parameters after walking web application 
- Find out if there are any interesting/useful cookies as a result of the application
- Identify additional subdomains using ffuf
- If ther is login panel, look for information in smb
- For remote command execution, 
## 1.3 B 
- If application is machine
- Identify machine operating system
- Run through enumeration workflow depending on the services that are available
- If ftp allows anonymous authentication, connect and download information
- If smb allows anonymous authentication connect and download information using spider module

# 2. Exploitation 
  
