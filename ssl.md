ami-0f3c7d07486cad139

centos-8

self-Signed Certificates using OpenSSL
==========================================
```
yum install httpd -y
```
```
systemctl status httpd
```
```
systemctl start httpd
```
```
systemctl enable httpd
```
==================================

```
yum install mod_ssl openssl -y
```

- mod_ssl – this is used to configure Apache with SSL
- openssl – is for creating SSL Certificate

Create a Key
cd /etc/httpd ## APACHE_HOME
mkdir ssl
cd ssl

Create a key

```
openssl genrsa -out gbala.key 2048
```

Create a Certificate Request - CSR

```
openssl req -new -key gbala.key -out gbala.csr

```


Create a Certificate crt

```
openssl x509 -req -days 365 -in gbala.csr -signkey gbala.key -out gbala.crt

```


Country Name (2 letter code) [XX]:IN
State or Province Name (full name) []:Hyd
Locality Name (eg, city) [Default City]:miyapur
Organization Name (eg, company) [Default Company Ltd]:lwplabs
Organizational Unit Name (eg, section) []:training
Common Name (eg, your name or your server's hostname) []:awsclass123.com
Email Address []:mailrahulsre@gmail.com
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
You can now pass on the CSR to Certificate Authority and they will give you below 3 files –
I’ll raise a ticket to SSL team, who will send a mail to Digicert Certificate Authority to give me below 3
files –
[root@ip-172-31-38-150 ssl]#
Custom singed certificate – Digicert/Verisign will give you
USERTrustRSAAddTrustCA.CCC
TrustedSecureCertificateAuthority5.ccc
302880581.ccc - This name will change for every request - Server certificate
SSLCertificateFile /etc/ssl/certificate.crt
SSLCertificateKeyFile /etc/ssl/private/private.key


Go to directory – /etc/httpd/conf.d
1. edit ssl.conf and edit the SSL certificate path where we have created the crt and key file
2. Change ServerName parameter to our Common Name which we gave earlier while creating
the csr file above.
3. DocumentRoot "/var/www/html/aws"
4. Save it



