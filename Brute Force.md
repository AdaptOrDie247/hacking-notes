# Hydra

Brute Force Service
`hydra -l username -P passwordlist ipaddress servicename`

File user:pass Format
`hydra -C userpass.txt ipaddress servicename`

# Username Anarchy

Generate Usernames From Full Names
`./username-anarchy --input-file ../fullnames.txt --select-format first,flast,first.last,firstl > ../unames.txt`
