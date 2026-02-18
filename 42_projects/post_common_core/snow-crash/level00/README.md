# Level00 – SnowCrash

## Objective
Obtain the flag for level00 by analyzing files belonging to the user `flag00`.

## Reconnaissance
Identified files owned by `flag00` and located a file containing an encoded string.
```bash
find / -user "flag00" 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
```

## Exploitation
The string in the file `/usr/sbin/john` consisted of only letters shifted in the alphabet,
which is a strong indication of a Caeser cipher. To confirm, we used [dCode – Caesar Cipher](https://www.dcode.fr/chiffre-cesar) to decode it.

## Flag
![Description](images/level00_flag.png)
