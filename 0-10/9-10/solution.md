- The password is hidden in data.txt, somewhere between a bunch of gibberish text.
- We use `strings` to fetch it out, also limit the number of character to 10 so we dont get any gibberish on the screen.

```bash
bandit9@bandit:~$ strings -n 10 data.txt 
========== the
========== password{k
=========== is
_$DM[q2	RO-;
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```
- We got the password
    - FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey