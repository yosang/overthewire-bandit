# Solving the problem
- Instructions say there is a folder called `inhere`, thats where we would find the password, we go ahead an ls -l inhere to see whats there
    - and we didnt find any files in here
    - instructions say files are hidden so we got to use the -a flag on ls
```bash
bandit3@bandit:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Apr 10 14:23 inhere
bandit3@bandit:~$ ls -l inhere/
total 0
bandit3@bandit:~$ ls -la inhere/
total 12
drwxr-xr-x 2 root    root    4096 Apr 10 14:23 .
drwxr-xr-x 3 root    root    4096 Apr 10 14:23 ..
-rw-r----- 1 bandit4 bandit3   33 Apr 10 14:23 ...Hiding-From-You
```

- We got a file, with name `...Hiding-From-You`, I guess thats the file we want
    - we go ahead and cd to the folder and cat the file to get the password

```bash
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Apr 10 14:23 .
drwxr-xr-x 3 root    root    4096 Apr 10 14:23 ..
-rw-r----- 1 bandit4 bandit3   33 Apr 10 14:23 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You 
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
bandit3@bandit:~/inhere$ 

```
- We got the password:
    - 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ