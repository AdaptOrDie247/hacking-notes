# Downloads

Apache Directory Studio https://directory.apache.org/studio/downloads.html
Avalonia ILSpy https://github.com/icsharpcode/AvaloniaILSpy/releases
BloodHound https://github.com/BloodHoundAD/BloodHound/releases
Chisel https://github.com/jpillora/chisel/releases
CyberChef https://cyberchef.io/
ffuf https://github.com/ffuf/ffuf
Genymotion https://www.genymotion.com/download/
git-dumper https://github.com/arthaud/git-dumper
gRPCurl https://github.com/fullstorydev/grpcurl
jsfinder https://github.com/kacakb/jsfinder
JWT https://jwt.io/
Kubeletctl https://github.com/cyberark/kubeletctl/releases
Mono https://www.mono-project.com/download/stable/
Nishang PowerShell Revshell https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1
PowerSploit https://github.com/PowerShellMafia/PowerSploit
ProcDump https://learn.microsoft.com/en-us/sysinternals/downloads/procdump
Pspy https://github.com/DominicBreuker/pspy/releases
Rubeus https://github.com/GhostPack/Rubeus
# Linux

`apktool` Extract APK source code.
`awk` Pattern scanning/processing.
`base64` Base64 encode/decode.
`chisel` Tunnel connections.
`chmod` Grant execute permission or create SUID binaries.
`curl` Interact with web services.
`dig` DNS recon.
`docker` Docker client.
`evil-winrm` Exploit WinRM service.
`exiftool` View and modify image metadata.
`ffuf` Web fuzzing.
`ghidra` Reverse engineer binary files.
`git` Inspect commit history.
`gpg2john` Crack GPG keys with john.
`ifconfig` Old ip command alternative.
`ip` Get interface IP info.
`iw` Get wifi IP info.
`iwconfig` Old iw command alternative.
`john` Crack passwords.
`jq` Pretty JSON.
`kubectl` Kubernetes client.
`kubeletctl` Exploit Kubernetes.
`ldapsearch` Searches LDAP data.
`mech-dump` Get all website links.
`msfconsole` Easy exploitation.
`msfvenom` Craft payloads.
`nc` Send/receive connections.
`nmap` Port scanning.
`nslookup` DNS recon.
`python` Format strings and convert numbers.
`scp` Copy remote files.
`sed` Stream editor.
`smbclient` SMB operations.
`ss` Check open ports.
`ssh` Remote access and tunneling.
`ssh2john` Crack SSH keys with john.
`ssh-keygen` Generate SSH keys.
`strings` Filter out strings from binary.
`su` Switch user.
`telnet` Interact with services directly.
`tcpdump` Traffic capture/analysis.
`wine` Run windows apps in Linux.
`wireshark` Traffic capture/analysis.
`wpscan` Enumerate WordPress sites.
`xxd` Convert to/from hex.

## Improvised

Bash Port Scanner
```
for PORT in {0..1000}; do timeout 1 bash -c "</dev/tcp/ipaddress/$PORT
&>/dev/null" 2>/dev/null && echo "port $PORT is open"; done
```

# Windows

`Get-ADDomain` Confirm if a system is a DC (comes preinstalled on DCs).
`Get-Process` List processes.
`rubeus` Kerberos exploitation.
`whoami` Get user and user groups info.
