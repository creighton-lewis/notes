/home/*
cat /root/.ssh/authorized\_keys 
cat /root/.ssh/identity.pub 
cat /root/.ssh/identity 
cat /root/.ssh/id\_rsa.pub 
cat /root/.ssh/id\_rsa 
cat /root/.ssh/id\_dsa.pub 
cat /root/.ssh/id\_dsa 
cat /etc/ssh/ssh\_config 
cat /etc/ssh/sshd\_config 
cat /etc/ssh/ssh\_host\_dsa\_key.pub 
cat /etc/ssh/ssh\_host\_dsa\_key 
cat /etc/ssh/ssh\_host\_rsa\_key.pub 
cat /etc/ssh/ssh\_host\_rsa\_key 
cat /etc/ssh/ssh\_host\_key.pub 
cat /etc/ssh/ssh\_host\_key
cat ~/.ssh/authorized\_keys 
cat ~/.ssh/identity.pub 
cat ~/.ssh/identity 
cat ~/.ssh/id\_rsa.pub 
cat ~/.ssh/id\_rsa 
cat ~/.ssh/id\_dsa.pub 
cat ~/.ssh/id\_dsa 
 
grep -ir "-----BEGIN RSA PRIVATE KEY-----" /home/*
grep -ir "BEGIN DSA PRIVATE KEY" /home/*

grep -ir "BEGIN RSA PRIVATE KEY" /*
grep -ir "BEGIN DSA PRIVATE KEY" /
