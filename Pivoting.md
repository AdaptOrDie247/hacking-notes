# Tools

`chisel` Tunneling.
`impacket-psexec` Remote access.
`nc` Connections.
`proxychains` Tunneling.
`socat` Tunneling.
`ssh` Remote connections, tunneling.
`sshuttle` Tunneling.

# Chisel

Server
`chisel server -p port --reverse`

Client
`chisel client server_ip:server_port R:local_port:client_ip:client_port`

# PsExec

`impacket-psexec 'user:pass@ipaddress'`

# Socks Proxy

## Method 1

Metasploit
```
search socks
use auxiliary/server/socks_proxy
run
```

Edit attacker /etc/proxychains.conf
```
[ProxyList]
socks5 127.0.0.1 1080
```

Enable autoroute in Metasploit to automatically route all internal networks of the remote system back to us through Socks Proxy
```
search autoroute
use post/multi/manage/autoroute
set session sessionnumber
run
```

# SSH

Connect Using SSH Key
```
chmod 600 id_rsa
ssh -i id_rsa user@host
```

Local Port Forwarding
`ssh [-fNT to run in bg] -L [local_addr:]:local_port:remote_addr:remote_port [user@]gateway_addr`

Remote Port Forwarding
`ssh [-fNT to run in bg] -R [remote_addr:]remote_port:local_addr:local_port [user@]gateway_addr`

Dynamic Port Forwarding
```
ssh -D port user@target

Can configure browser proxy, e.g., FoxyProxy, for web access.

To proxychains this, edit /etc/proxychains4.conf:
socks5 127.0.0.1 port username password
```

# WinRM

Evil-WinRM
`evil-winrm -i ipaddress -u username -p password`

CrackMapExec
`crackmapexec winrm ipaddress -u username -p password`
