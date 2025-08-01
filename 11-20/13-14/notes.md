- The password is hidden in /etc/bandit_pass/bandit14 only bandit14 has reading rights to this file
- This level does not require us to find a password, instead to log onto the next level, we are going to use a private key
- From inside bandit13's home folder, we have a file named `sshkey.private`
```bash
bandit13@bandit:~$ file sshkey.private
sshkey.private: PEM RSA private key
bandit13@bandit:~$ ssh bandit14@bandit.labs.overthewire.org -p 2220 -i ~/sshkey.private
```
- we manages to establish a connection to bandit14, now its time to find the password, which according to the instructions should be in `/etc/bandit_pass/bandit14`

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```
- And there it is, we found a password, however, this password does not work to login to bandit14, its a password we are going to need to get password to bandit15, bandit14 log in happens through ssh public key from bandit14.