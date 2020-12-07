# DNS enumeration

its computer or server on internet that resove domain name to ip address.

eg : if you type google.com in browser then a request is sent to dns server, dns server resolve google.com to its ip address and then request is sent to that ip address.

`host google.com`  what ip address google.com resolve to.

its also used to reverse dns lookup

`host 10.10.10.10`

name resolution with nslookup

`nsloopup <ip>`

#### dig

norlmal name resolution 
`dig google.com`

enum specific type of recored 

`dig google.com -t mx`

![digimg](/img/dig.png)

#### Zone transfer

zone transfer is a process of copying or replicating dns database from primary dns server to a secondary dns server.

```
dig axfr @<DNS_IP> #Try zone transfer without domain
dig axfr @<DNS_IP> <DOMAIN> #Try zone transfer guessing the domain
fierce -dns <DOMAIN> #Will try toperform a zone transfer against every authoritative name server and if this doesn'twork, will launch a dictionary attack
```