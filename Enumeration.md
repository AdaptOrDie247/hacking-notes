# Active Directory

User enumeration via RID cycling when SMB null sessions allowed
`impacket-lookupsid anonymous@domain -no-pass`

Look for any vulnerable AD certificate templates (Part of Active Directory Certificate Services - AD CS)
`certipy-ad find -u username@domain -p 'password' -dc-ip ipaddress -vulnerable`

Get Machine Account Quota using crackmapexec (Show max # accounts allowed)
`crackmapexec ldap targetip -u username -p 'password' -M MAQ`

## SharpHound Collection

Collect All Info
`SharpHound.exe -C All`

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
`ffuf -u http://url/FUZZ -e .asp,.aspx,.config,.php -w wordlist -o outfile`

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

Get LDAP Naming Contexts, Unauthenticated
`ldapsearch -H ldap://ipaddress -x -s base namingcontexts`

List LDAP Info
`ldapsearch -H ldap://ipaddress -x -b "dc=name,dc=tld"`

Enumerate Users (impacket)
`impacket-GetADUsers domain/ -dc-ip ipaddress -debug`

Enumerate SPNs (impacket)
`impacket-GetUserSPNs domain/user:pass -dc-ip ipaddress -debug`

Enumerate SPNs with Kerberos Auth
`impacket-GetUserSPNs domain/user:pass -dc-ip ipaddress -request -k -debug`

Request TGS for Users
`impacket-GetUserSPNs domain/username:password -dc-ip ipaddress -debug -request`

Enumerate Users (windapsearch)
`python3 windapsearch.py -d domain --dc-ip ipaddress -U`

Enumerate All Objects (windapsearch)
`python3 windapsearch.py -d domain --dc-ip ipaddress --custom "objectClass=*"`

# MS SQL

Connect to MS SQL server
`impacket-mssqlclient windomainname/username:password@fqdn -windows-auth`

Browser remote file system
`xp_dirtree path`

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

## impacket-smbclient

Connect to Target using account with Kerberos auth
`impacket-smbclient -k domain/user:pass@targetfqdn -dc-ip dcipaddress`

## smbclient

List Shares (" " username and pass)
`smbclient -U ' '%' ' -L //ipaddress`

List Shares (send username, but no pass)
Sometimes sending blank creds doesn't work, but this does.
`smbclient -NL //ipaddress`

Connect to Share
`smbclient -U ' '%' ' //ipaddress/sharename`

Connect to Share with username/creds
Works sometimes when sending blank creds fails
`smbclient -N //ipaddress/sharename`

Recursively Download Files From Share
```
smb: \> prompt off
smb: \> recurse on
smb: \> mget *
```

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

Bash Port Scanner
```
for PORT in {0..1000}; do timeout 1 bash -c "</dev/tcp/ipaddress/$PORT
&>/dev/null" 2>/dev/null && echo "port $PORT is open"; done
```

Famous HTB Nmap Voodoo
```
ports=$(sudo nmap -sS -p- --min-rate=1000 -T4 ipaddress | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
sudo nmap -sSCV -p$ports ipaddress
```

Quickly Scan All Ports
`sudo nmap -sS --min-rate 1000 -T4 -p- -v -oA nm-tcp-prt ipaddress`

UDP Scan Common 1000 Ports (Add -p- to scan all, but VERY slow)
`sudo nmap -sU -v -oA nm-udp-prt ipaddress`

Enumerate Services
`sudo nmap -sSVC -p22,80,445 -v -oA nm-tcp-dtl ipaddress`

Check for Vulns on Port
`sudo nmap --script vuln -p port -v -oA nm-tcp-port-vuln ipaddress`

# WordPress

Check the plugins directory
`/wp-content/plugins`
