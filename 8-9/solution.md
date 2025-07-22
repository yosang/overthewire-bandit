- In this one we got a file `data.txt` with a bunch of passwords and a bunch of duplicates.
- For us to remove the duplicates and only retrieve the password that is unique we need to do some piping
- We start with cat, to get the data from the file
    - then we pipe into a sort, because uniq only works on adjacent matching lines.
    - Then we do uniq with -u flag to only print out the unique line, which is our password
```bash
bandit8@bandit:~$ cat data.txt | sort | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
- We got our password
    - 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM