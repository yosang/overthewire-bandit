- We got a data.txt file with base64 encoded content.
- In order for us to find the password we need to decode the content first.
- Using the command `base64` and the `-d` flag, we can get this done.
```bash
bandit10@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit11 bandit10 69 Apr 10 14:22 data.txt
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ man base64
bandit10@bandit:~$ base64 -d data.txt 
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
- We got the password
    - dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr