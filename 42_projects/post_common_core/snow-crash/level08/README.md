# Level08 – SnowCrash

## Objective
Retrieve the flag for `level08` by bypassing file access restrictions in a SUID binary.

## Reconnaissance
The home directory contains:
- A SUID binary level08 owned by flag08
- A file token readable only by flag08
Running the binary without arguments shows it expects a file to read:
```bash
./level08 [file to read]
```
Dynamic analysis (`ltrace`) reveals the following behavior:
The program checks whether the provided filename contains the string "token" using `strstr()`.
If the filename includes `"token"`, access is denied.
Otherwise, it attempts to open and read the file.
This suggests a naïve protection mechanism based only on the filename string.

### Vulnerability
The binary performs a substring check:
```bash
strstr(user_input, "token")
```
If "token" appears in the filename, access is blocked.
However, this check only applies to the string provided as argument, not to the actual file being accessed.
This creates a symlink bypass vulnerability.
Because the binary is SUID and owned by `flag08`, it executes with `flag08` privileges and can read protected files.

## Exploitation
Create a symbolic link to the protected file using a different name:
```bash
ln -s /home/user/level08/token /tmp/test
```
Since `/tmp/test` does not contain the string `"token"`, the check passes.
The binary follows the symbolic link and reads the real `token` file with `flag08` privileges.

## Flag
![Level08 Flag Screenshot](images/level08_flag.png)

