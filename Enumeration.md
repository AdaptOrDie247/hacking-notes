# DNS

Get Records
`nslookup host [dns-server]`

Zone Transfer
`dig axfr @dns-server host`

# FTP

Anonymous Login
`ftp anonymous@ipaddress`

# HTTP

Directory Traversal
`../` or `....//`

Directory Fuzzing
`ffuf -u http://url/FUZZ -w wordlist -o output`

VHOST Fuzzing
`ffuf -u http://url -H "Host: FUZZ.url" -w wordlist -o output`

# SMB

## enum4linux

Enumerate common SMB info
`enum4linux ipaddress`

## smbclient

List Shares (" " username and pass)
`smbclient -U " "%" " -L \\\\ipaddress\\`

Connect to Share
`smbclient -U " "%" " \\\\ipaddress\\sharename`

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

Quickly Scan All Ports
`sudo nmap -sS --min-rate 1000 -T4 -p- -v -oA nmap-tcp ipaddress`

UDP Scan Common 1000 Ports (Add -p- to scan all, but VERY slow)
`sudo nmap -sU -v -oA nmap-udp ipaddress`

Enumerate Services
`sudo nmap -sSVC -p22,80,445 -oA nmap-tcp-services ipaddress`

# WordPress

Check the plugins directory
`/wp-content/plugins`
