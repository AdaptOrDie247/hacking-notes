# ID Hash

hashid (-j shows corresponding JohnTheRipper format)
`echo -n 'hash' | hashid -j`

# John

## Important Note
John is not perfect at detecting hashes. For example, unless you specify --format=NT for NTLM hashes, it will not successfully crack them.

Crack NTLM Hash
`john --format=NT --wordlist=wordlist user.hash`

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

Note: Get username from id_rsa.pub file.
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
