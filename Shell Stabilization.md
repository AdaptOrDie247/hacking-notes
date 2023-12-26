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
