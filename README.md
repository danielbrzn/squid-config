# Squid configuration file

This is a configuration file for the Squid proxy server. You may use the following bash script on CentOS based machines to deploy a proxy server:

```
#!/bin/bash

# Change the username and password to your liking
yum install squid wget httpd-tools openssl openssl-devel -y && touch /etc/squid/passwd && htpasswd -b /etc/squid/passwd username password
wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/danielbrzn/squid-config/master/proxyconf --no-check-certificate
touch /etc/squid/blacklist.acl
systemctl restart squid.service && systemctl enable squid.service
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
iptables-save
```