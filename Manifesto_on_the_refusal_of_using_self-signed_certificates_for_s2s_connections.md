
# Manifesto on the refusal to use self-signed certificates for s2s connections

In the past, the certificates were worth the money. In the past, obtaining certificates was a difficult task.This forced the use of self-signed certificates in self-signed connections to preserve the federation.

Currently, certificates have become free and anyone can get them. We believe that the time has come to stop supporting self-signed certificates to increase user security.


## Servers in this list pledge not to accept connections with self-signed certificates.

- [404.city](https://404.city)
- [jabberon.ru](https://jabberon.ru)


## Servers in this list refused to support the manifest

Servers that fail to verify certificates in cross-server connections

## Servers violated the execution of the manifest

Servers that accepted the manifest, but did not use it


## Setup Instructions


**Warning!** Remember the correct cipher list, otherwise you will not be able to connect to the servers.
Do not try to enumerate ciphers yourself, because certificates can be used in the future by other ciphers

**Correct:**
```
'TLS_CIPHERS': "HIGH:!aNULL:!eNULL:!3DES:@STRENGTH"
```
**Wrong:**

This set includes **ECC (ECDHE-ECDSA) and RSA (ECDHE-RSA)** ciphers. This is right now, but will not work in the future!
In the future, new ciphers will appear and the setting will be incorrect. To upgrade the certificate class, use the ECC certificate instead of RSA, and not guessing with cipher suites!
 ```
 'TLS_CIPHERS': "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-CAMELLIA256-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA"

 ```
 
**Ejabberd (ejabberd.yml)**
```
s2s_use_starttls: required
```
Change to
```
s2s_use_starttls: required_trusted
```


## Feedback

XMPP: support@404.city

If you have a public server, you can include it in an independent server list.

