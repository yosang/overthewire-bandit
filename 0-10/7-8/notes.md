- In this one we got one big file with key value pairs, of a key being a random word and the value being the password we want
- We are instructed to extract the value next to the key `millionth`. Thats our password.
- Here we use cat, pipe and grep
- `cat data.txt | grep millionth`
```bash
bandit7@bandit:~$ ls -l
total 4088
-rw-r----- 1 bandit8 bandit7 4184396 Apr 10 14:23 data.txt
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
- We found our password
    - dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc