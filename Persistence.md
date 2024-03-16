# Windows

Create account via DC (will prompt for existingaccount password)
`impacket-addcomputer 'domain/existingaccount' -method LDAPS -computer-name 'newaccountname' -computer-pass 'newpassword' -dc-ip dcipaddress`
