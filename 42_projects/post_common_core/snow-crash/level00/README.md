# Level00 – SnowCrash

## Objective
Obtain the flag for level00 by analyzing files owned by the user `flag00`.
## Reconnaissance
Identify files belonging to `flag00`:
```bash
find / -user "flag00" 2>/dev/null
```
Located the file `/usr/sbin/john` containing an encoded string.

## Exploitation
The file `/usr/sbin/john` contained only alphabetic characters, indicating a Caesar cipher.
- Determined the shift and decoded the string using a Caesar cipher decoding method.
- Recovered the flag from the decoded string.

## Flag
![Description](images/level00_flag.png)
