
# Scans 
## Rustscan 
- only ports open are 22 and 80
## Nmap 
```
# Nmap 7.95 scan initiated Sat Jul 18 20:15:55 2026 as: nmap -sV -sC -T 4 -oN scan-1 10.129.31.123
Nmap scan report for 10.129.31.123
Host is up (0.15s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE    SERVICE VERSION
22/tcp filtered ssh
80/tcp open     http    Apache httpd 2.4.52
|_http-title: Did not follow redirect to http://titanic.htb/
|_http-server-header: Apache/2.4.52 (Ubuntu)
Service Info: Host: titanic.htb

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done a
```
# Obervartions 
- Web application
- When someone submits a form, they werceive information about their stay
- The phone number parametr is not checked, as you can add a phone number with more than 10 characters and it is still executed
- vulnx search
```

- [CVE-2022-22719] High - Apache HTTP Server - Denial of Service
  ↳ Priority: MEDIUM | No exploits | Vuln Age: 1585d
  ↳ CVSS: 7.5 | EPSS: 0.6980 (MED) | KEV: ✘
  ↳ Exposure: ~14276.2K | Vendors: apple, apache +3 | Products: mac_os_x, macos +4
  ↳ Patch: ✔ | POCs: ✘ | Nuclei Template: ✘ | HackerOne: ✔
─────────────────────────────────────────────────────────────────────────

[CVE-2022-22720] Critical - Apache HTTP Server - HTTP Request Smuggling
  ↳ Priority: HIGH | EXPLOITS AVAILABLE | Vuln Age: 1587d
  ↳ CVSS: 9.8 | EPSS: 0.2819 | KEV: ✘
  ↳ Exposure: ~14279.7K | Vendors: oracle, apple +3 | Products: zfs_storage_appli..., mac_os_x +5
  ↳ Patch: ✔ | POCs: 1 | Nuclei Template: ✘ | HackerOne: ✔
─────────────────────────────────────────────────────────────────────────

[CVE-2022-22721] Critical - Apache HTTP Server - Integer Overflow
  ↳ Priority: MEDIUM | No exploits | Vuln Age: 1587d
  ↳ CVSS: 9.1 | EPSS: 0.4186 (MED) | KEV: ✘
  ↳ Exposure: ~14279.7K | Vendors: oracle, apple +3 | Products: enterprise_manage..., http_server +5
  ↳ Patch: ✔ | POCs: ✘ | Nuclei Template: ✘ | HackerOne: ✔
─────────────────────────────────────────────────────────────────────────

[CVE-2022-23943] Critical - Apache HTTP Server - Out of Bounds Read/Write
  ↳ Priority: URGENT | No exploits | Vuln Age: 1587d
  ↳ CVSS: 9.8 | EPSS: 0.5040 (MED) | KEV: ✘
  ↳ Exposure: ~14279.7K | Vendors: debian, oracle +2 | Products: debian_linux, http_server +2
  ↳ Patch: ✔ | POCs: ✘ | Nuclei Template: ✘ | HackerOne: ✔
```


- Email is validated
-  Phone number is validated
-  
