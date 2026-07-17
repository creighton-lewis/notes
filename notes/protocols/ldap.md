ldapsearch -x -H ldap://target.com \
  -D "cn=admin,dc=example,dc=com" -w password \
  -b "dc=example,dc=com" \
  "(&(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=4194304))" \
  sAMAccountName
