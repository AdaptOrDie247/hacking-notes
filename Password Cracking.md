# John

Crack GPG Keys
```
gpg2john key.asc > key.john

john --format=gpg --wordlist=wordlist key.john
```

Crack Hashes
`john --wordlist=wordlist hashes`

Crack SSH Keys
```
ssh2john id_rsa > id_rsa.john

john --wordlist=wordlist id_rsa.john
```

Crack zip files
```
zip2john file.zip > file.john

john --wordlist=wordlist file.john
```

Unshadow
```
echo -n passwduserline > passwd.txt
echo -n shadowuserline > shadow.txt
unshadow passwd.txt shadow.txt > unshadowed.txt
john --wordlist=wordlist unshadowed.txt
```

List Formats
`john --list=formats`
