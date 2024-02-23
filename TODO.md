
- Copy all shells from https://www.revshells.com/.
- Copy all privesc info from https://gtfobins.github.io/.
- Copy all LOLBAS info from https://lolbas-project.github.io/.

- Learn about how this works:
- `http://ipaddress/?page=php://filter/convert.base64-encode/resource=config`

- Learn about `rlwrap` and other methods for automating shell stabilization (`powercat`?).
	- Note that `rlwrap` doesn't protect against control characters (by default?).

- Explore PowerCat (remnant from my memory):
	- https://github.com/secabstraction/PowerCat
- Also, PowerSploit:
	- https://github.com/PowerShellMafia/PowerSploit
- Finish figuring out how to render special characters from winPEAS output in text file copied to Kali.

On HTB "Active" Box, could not specify -U ' '%' '  for smbclient. This resulted in logon failure. Had to leave out that param to connect... Figure out why!

Notes from other hackers:
- C:\\Windows\\Tasks possible good writable location.
- Invoke-Command Good to know.
- Migrate to Conhost for stable shell.
