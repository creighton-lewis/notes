# LDAP Summary 
```
ldapsearch -x -H ldap://target.com \
  -D "cn=admin,dc=example,dc=com" -w password \
  -b "dc=example,dc=com" \
  "(&(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=4194304))" \
  sAMAccountName
```


```
ldapsearch -Q -Y GSSAPI -H ldap://10.129.95.210 -b 'DC=htb,local' '(objectClass=user)'
```

```
ldapsearch -X -H ldap://ip -b "dc=authority,dc=htb"
```
