# LDAP Summary 
```
ldapsearch -x -H ldap://target.com \
  -D "cn=admin,dc=example,dc=com" -w password \
  -b "dc=example,dc=com" \
  "(&(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=4194304))" \
  sAMAccountName
```

```
ldapsearch -X -H ldap://ip -b "dc=authority,dc=htb"
```

```
nxc ldap 10.129.232.88 -u $uname -p $pass --bloodhound --dns-server $ip # adding dns-server was crucial in recent activity
```
