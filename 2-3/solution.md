# Solving the problem
- We start by ls -l, and found one file
```bash
bandit2@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit3 bandit2 33 Apr 10 14:23 spaces in this filename
bandit2@bandit:~$ file spaces\ in\ this\ filename 
spaces in this filename: ASCII text
```
- There is two ways we can cat this file, either by escaping each space with a `\` or by writing the name of the file within single or double quotes
- We decide to go with single quotes
```bash
bandit2@bandit:~$ cat 'spaces in this filename' 
```
- We got the password:
    - MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx