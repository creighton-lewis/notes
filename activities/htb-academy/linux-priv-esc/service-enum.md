# Service-Based Privilege Escalation 
## Linux Capabilities 
| Capability Name |Capability description |
|----------|----------|
| cap_dac_override  |  Can bypass permission checks on any file     |
| cap_sys_admin  |   Can perform actions with admin privileges  |
| cap_chown | Can make aribitrary changes to file UIDs and GIDs |
| cap_audit_control | Can enable/disable kernel auditing, change filters and retrieve status and filtering roles           |
| cap_audit_write  | Can write records to kernel auditing log   |

## Cron Job Abuse 
>[!NOTE]
>Attacker must have write access
>
>Script should be ran in shared directory
>
>Best if script is scheduled to run as root
>
>Capturing cron job in psspy output is encouraged & possible

> Where cron jobs are located

```
/etc/cron.hourly
/etc/cron.weekly
/etc/cron.monthly
```

```
crontab -e
crontab -l
```
## Containers
```
Process >> Identify containers that exist  >> Enumerate and exploit
                                           >> Identify operating system and import your own
```
### Docker 
>[!NOTE]
> How to find out if docker container exists on system

**Recon** 
```
nc -vn target.com 2375
nuclei -u http://site.com -tag docker
sudo nmap -sV  --script docker-version,docker-info url 
```
**Connecting**
```
export DOCKER_HOST="tcp://target.com:2375"
docker ps
```

```
export DOCKER_HOST="tcp://target.com:2376"
export DOCKER_TLS_VERIFY=1
docker --tlsverify ps
```
**Enumeration**
```
docker -H tcp://target.com:2375 ps

docker -H tcp://target.com:2375 ps

docker -H tcp://target.com:2375 inspect <container_id>

curl http://target.com:2375/containers/json?all=1

docker -H tcp://target.com:2375 version

docker -H tcp://target.com:2375 info

docker -H tcp://target.com:2375 system df 


```
