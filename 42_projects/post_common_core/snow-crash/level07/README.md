# Level07 – SnowCrash

## Objective
Retrieve the flag for `level07` by exploiting unsafe use of an environment variable inside a SUID binary.

## Reconnaissance
The home directory contains a SUID binary `level07` owned by `flag07`.
Dynamic analysis using `ltrace` reveals the following behavior:
```bash
getenv("LOGNAME") = "level07"
asprintf(...)
system("/bin/echo level07")
```
The program:
1. Retrieves the LOGNAME environment variable.
2. Constructs a command string using asprintf.
3. Passes the result to `system()`.
This indicates that user-controlled environment data is being used to build a shell command.

### Vulnerability
The binary builds a shell command using the `LOGNAME` environment variable and executes it via system().
Because `system()` invokes `/bin/sh -c`, shell metacharacters can be injected.
This creates a classic command injection via environment variable.
Since the binary is SUID and owned by `flag07`, injected commands execute with `flag07` privileges.

## Exploitation
Override the `LOGNAME` variable with a malicious payload:
```bash
export LOGNAME='"; getflag; #'
```

## Flag
![Level07 Flag Screenshot](images/level07_flag.png)

