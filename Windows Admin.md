Create Domain User
`net user username password /add /domain`

Add User to Domain Group
`net group "groupname" username /add`

Add User to Local Group
`net localgroup "groupname" username /add`

Create PowerShell Credential
```
$pass = convertto-securestring 'password' -asplain -force
$cred = new-object system.management.automation.pscredential('domain\user', $pass)
```