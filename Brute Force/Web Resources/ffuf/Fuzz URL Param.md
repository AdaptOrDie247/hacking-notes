Fuzz uniform parameter (e.g., notice ?user=, ?movie=, etc. in URL)
-b sets cookie value, in this case our logged in session ID
`ffuf -u 'https://streamio.htb/admin/?FUZZ=' -b 'PHPSESSID=bdoga8oui5bvm3q3aum7v0j35s' -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -fs 1678`
