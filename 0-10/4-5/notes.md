# Solving the problem
- We are instructed to find the password in one of the files that are inside the `inhere` folder
- We cd into `inhere` and do ls -l to see the files

```bash
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -l
total 40
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file00
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file01
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file02
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file03
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file04
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file05
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file06
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file07
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file08
-rw-r----- 1 bandit5 bandit4 33 Apr 10 14:23 -file09
```

- There is a bunch of files here, the instructions say we need the one that is human-readable, that tells us it has to be of type text of some sort.
- We can identify the files with `file` command
- So we do `file ./-file*` to check all of them and see which one has text type

```bash
bandit4@bandit:~/inhere$ file ./-file*
./-file00: PGP Secret Sub-key -
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
- We see that file07 is the one we want, we can now `cat` it to get the password
```bash
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```
- we got the password
    - 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
- on to the next level **bandit5**