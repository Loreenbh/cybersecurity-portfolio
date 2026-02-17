# Level00 – SnowCrash

## Objective
Obtain the flag for level00 by analyzing files belonging to the user `flag00`.

---

## Reconnaissance
Search for files owned by `flag00`:

```bash
find / -user "flag00" 2>/dev/null
```

## Output
```
/usr/sbin/john
/rofs/usr/sbin/john
```

The file `/usr/sbin/john` contained a password encoded with a Caesar cipher.
Tool used for decoding:
[dCode – Caesar Cipher](https://www.dcode.fr/chiffre-cesar)

## Flag
![Description](images/level00_flag.png)
