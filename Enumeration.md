
# Android

Connect to ADB (Android Debug Bridge), Default Port TCP 5555
`adb connect ipaddress:port`

List Connected Devices
`adb devices`

Get Shell
`adb shell`

Get Root Shell
`adb root`

# DNS

Get Records
`nslookup host [dns-server]`

Zone Transfer
`dig axfr @dns-server host`

# FTP

Anonymous Login
`ftp anonymous@ipaddress`

# HTTP/S

Check domain info via TLS cert

Directory Traversal
`../` or `....//`

Directory Fuzzing
`ffuf -u http://url/FUZZ -w wordlist -o outfile`

File Fuzzing
`ffuf -u http://url/FUZZ -e .php -w wordlist -o outfile`

VHOST Fuzzing
`ffuf -u http://url -H "Host: FUZZ.url" -w wordlist -o outfile`

Nikto Vuln Scan
`nikto -host ipaddress`

## Execution After Redirect (EAR)

Capture request in Burp, send to repeater, and disable following redirects. This can be used when applications rely solely on redirects to limit access to pages that get loaded even momentarily.

## Wordpress

wpscan
`wpscan --url wordpressurl`

# LDAP

List LDAP Info
`ldapsearch -H ldap://ipaddress -x -b "dc=name,dc=tld"`

Enumerate Users
`python3 windapsearch.py -d fqdn --dc-ip ipaddress -U`

Enumerate All Objects
`python3 windapsearch.py -d fqdn --dc-ip ipaddress --custom "objectClass=*"`

# NFS

Show NFS server export list
`showmount -e ipaddress`

Mount directory
`sudo mount -t nfs [-o vers=2] ipaddress:/directory ./directory -o nolock`

# RPC

rpcinfo
`rpcinfo ipaddress`

nmap RPC Port via UDP with Script (E.g., Port 111)
`sudo nmap -sUC -p 111 -oA nm-udp-111 ipaddress`

# SMB

## enum4linux

Enumerate common SMB info
`enum4linux ipaddress`

## smbclient

List Shares (" " username and pass)
`smbclient -U " "%" " -L //ipaddress`

Connect to Share
`smbclient -U " "%" " //ipaddress/sharename`

## smbmap

List Shares
`smbmap -H ipaddress --no-banner`

Recursively List Share Contents (Did not work last time)
`smbmap -H ipaddress -R sharename --no-banner`

Download File
`smbmap -H ipaddress --download 'sharename\\folder\\subfolder\\file' --no-banner`

## crackmapexec

Brute Force
`crackmapexec smb ipaddress -u users.txt -p passwords.txt`

RID Brute Force
`crackmapexec smb ipaddress -u username -p password --rid-brute`

# SNMP

Scan SNMP v1 Service, Output to File
`snmpwalk -v 1 -c public ipaddress > snmp.log`

# TCP/IP

Famous HTB Nmap Voodoo
```
ports=$(sudo nmap -p- --min-rate=1000 -T4 ipaddress | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
sudo nmap -sC -sV -p$ports ipaddress
```

Quickly Scan All Ports
`sudo nmap -sS --min-rate 1000 -T4 -p- -v -oA nmap-tcp ipaddress`

UDP Scan Common 1000 Ports (Add -p- to scan all, but VERY slow)
`sudo nmap -sU -v -oA nmap-udp ipaddress`

Enumerate Services
`sudo nmap -sSVC -p22,80,445 -oA nmap-tcp-services ipaddress`

# WordPress

Check the plugins directory
`/wp-content/plugins`
