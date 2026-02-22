# Level07 – SnowCrash

## Objective
Retrieve the flag for `level07` by exploiting unsafe use of an environment variable inside a SUID binary.

## Reconnaissance
The home directory contains a SUID binary `level07` owned by `flag07`.
Dynamic analysis using `ltrace` reveals:
```bash
getenv("LOGNAME") = "level07"
asprintf(...)
system("/bin/echo level07")
```
The program:
- Retrieves the `LOGNAME` environment variable.
- Constructs a command string using `asprintf`.
- Executes it via `system()`.
This shows that user-controlled environment data is used to build a shell command.

### Vulnerability
- The binary executes a shell command based on `LOGNAME` via `system()`.
- Because `system()` invokes `/bin/sh -c`, shell metacharacters can be injected.
- As the binary is SUID and owned by `flag07`, injected commands run with `flag07` privileges.

## Exploitation
Override the `LOGNAME` variable with a malicious payload:
```bash
export LOGNAME='"; getflag; #'
```
Executing the binary triggers the payload, running getflag with `flag07` privileges.

## Flag
![Level07 Flag Screenshot](images/level07_flag.png)

