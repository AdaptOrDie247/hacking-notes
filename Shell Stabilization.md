# Linux
## Script

```
script /dev/null -c /bin/bash
ctrl+z
stty raw -echo; fg
export TERM=xterm
```
## Python

```
python -c 'import pty; pty.spawn("/bin/bash")'
ctrl+z
stty raw -echo; fg
export TERM=xterm
```

## Generate SSH Keys (Assuming SSH Accessible)

Shell must be "stable" first, e.g., by using script or python.
```
ssh-keygen
cat id_rsa.pub > ~/.ssh/authorized_keys
```
