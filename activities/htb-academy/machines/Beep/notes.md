# Scans 
## Nmap scan 
```
# Nmap 7.95 scan initiated Thu Jul 16 22:40:21 2026 as: nmap -sV -sC -A -T 4 -oN scan-1 10.129.229.183
Nmap scan report for 10.129.229.183
Host is up (0.13s latency).
Not shown: 988 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 4.3 (protocol 2.0)
| ssh-hostkey: 
|   1024 ad:ee:5a:bb:69:37:fb:27:af:b8:30:72:a0:f9:6f:53 (DSA)
|_  2048 bc:c6:73:59:13:a1:8a:4b:55:07:50:f6:65:1d:6d:0d (RSA)
25/tcp    open  smtp?
|_smtp-commands: Couldn't establish connection on port 25
80/tcp    open  http       Apache httpd 2.2.3
|_http-title: Did not follow redirect to https://10.129.229.183/
|_http-server-header: Apache/2.2.3 (CentOS)
110/tcp   open  pop3?
111/tcp   open  rpcbind    2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100024  1            853/udp   status
|_  100024  1            856/tcp   status
143/tcp   open  imap?
443/tcp   open  ssl/https?
|_ssl-date: 2026-07-16T22:44:38+00:00; -18s from scanner time.
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2017-04-07T08:22:08
|_Not valid after:  2018-04-07T08:22:08
993/tcp   open  imaps?
995/tcp   open  pop3s?
3306/tcp  open  mysql?
4445/tcp  open  upnotifyp?
10000/tcp open  http       MiniServ 1.570 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Device type: general purpose|media device|PBX|WAP|specialized|printer
Running (JUST GUESSING): Linux 2.6.X|2.4.X|3.X (97%), Star Track embedded (95%), Linksys embedded (94%), Riverbed RiOS (94%), HP embedded (94%), Osmosys embedded (93%)
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:2.6.27 cpe:/h:star_track:srt2014hd cpe:/o:linux:linux_kernel:2.6.18 cpe:/o:linux:linux_kernel:2.4.32 cpe:/h:linksys:wrv54g cpe:/o:linux:linux_kernel:3 cpe:/o:riverbed:rios
Aggressive OS guesses: Linux 2.6.18 - 2.6.24 (97%), Linux 2.6.18 (95%), Linux 2.6.9 - 2.6.24 (95%), Linux 2.6.9 - 2.6.30 (95%), Linux 2.6.27 (95%), Linux 2.6.30 (95%), Linux 2.6.8 (95%), Linux 2.6.9 (95%), Linux 2.6.5 - 2.6.12 (95%), Linux 2.6.18 - 2.6.32 (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: 127.0.0.1

Host script results:
|_clock-skew: -18s

TRACEROUTE (using port 8888/tcp)
HOP RTT      ADDRESS
1   80.21 ms 10.10.16.1
2   80.26 ms 10.129.229.183

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jul 16 22:50:09 2026 -- 1 IP address (1 host up) scanned in 587.63 second
```
## Nuclei scan 
 > Took much less time than nmap scan

```
[http-trace:trace-request] [http] [info] https://10.129.229.183
[cookies-without-secure] [javascript] [info] 10.129.229.183 ["elastixSession"]
[cookies-without-httponly] [javascript] [info] 10.129.229.183 ["elastixSession"]
[drupal-directory-listing] [http] [low] https://10.129.229.183/modules/
[waf-detect:apachegeneric] [http] [info] https://10.129.229.183
[INF] Skipped 10.129.229.183:9780 from target list as found unresponsive permanently: cause="port closed or filtered" address=10.129.229.183:9780 chain="connection refused; got err while executing https://10.129.229.183:9780/api/v1/user_assets/nfc"
[snmpv3-detect] [javascript] [info] 10.129.229.183:161 ["Enterprise: unknown"]
[rpc-udp-detect] [javascript] [info] 10.129.229.183:111 ["RPC Portmapper UDP Detected"]
[openssh-detect] [tcp] [info] 10.129.229.183:22 ["SSH-2.0-OpenSSH_4.3"]
[tls-version] [ssl] [info] 10.129.229.183:443 ["tls10"]
[weak-cipher-suites:tls-1.0] [ssl] [low] 10.129.229.183:443 ["[tls10 TLS_RSA_WITH_AES_128_CBC_SHA]"]
[deprecated-tls:tls_1.0] [ssl] [info] 10.129.229.183:443 ["tls10"]
[deprecated-tls:ssl_3.0] [ssl] [info] 10.129.229.183:443 ["ssl30"]
robots-txt] [http] [info] https://10.129.229.183/robots.txt
[robots-txt-endpoint] [http] [info] https://10.129.229.183/robots.txt
[CVE-2023-37599] [http] [high] https://10.129.229.183/modules/
[http-missing-security-headers:strict-transport-security] [http] [info] https://10.129.229.183
[http-missing-security-headers:content-security-policy] [http] [info] https://10.129.229.183
[http-missing-security-headers:permissions-policy] [http] [info] https://10.129.229.183
[http-missing-security-headers:x-frame-options] [http] [info] https://10.129.229.183
[http-missing-security-headers:referrer-policy] [http] [info] https://10.129.229.183
[http-missing-security-headers:cross-origin-opener-policy] [http] [info] https://10.129.229.183
[http-missing-security-headers:x-content-type-options] [http] [info] https://10.129.229.183
[http-missing-security-headers:x-permitted-cross-domain-policies] [http] [info] https://10.129.229.183
[http-missing-security-headers:cross-origin-embedder-policy] [http] [info] https://10.129.229.183
[http-missing-security-headers:cross-origin-resource-policy] [http] [info] https://10.129.229.183
****
```
```
searchsploit openssh 4.3
SSH-2.0-OpenSSH_4.3
multiple/dos/2444.sh
```

# Notes 
- Several open ports
- Not sure what exploit would be the best or if any even exist that work well
- Looks like webpage
- Ssl is expired, consistent issue 

```
- > enumerate live services -> determine attack path 
```
>[!NOTE] the CVE code mentioned can do the following: 
>issabel-pbx version 4.0.0-6 contains a Broken Access Control vulnerability that manifests as unauthenticated Directory Listing on the web interface. Any remote, unauthenticated attacker >can browse the application's modules directory and directly access sensitive source files, configuration files, and internal application logic without any credentials or authorization.

>[!NOTE]
>Exploitation
>Note - It might be possible that the webpage cannot be loaded due to Firefox and other browsers
>changing their min TLS version to a number higher than what the box supports. The workaround
>to this is to edit the “security.tls.version.min” to 1.
>To modify the minimum TLS version in Firefox, follow these steps:
>1. Open a new tab in Firefox.Enter "about:config" in the address bar and hit Enter/Return.
>2. In the search box located above the list, enter "security.tls.version.min".
>3. Locate the preference with the name "security.tls.version.min" and modify its value to ‘1’.
