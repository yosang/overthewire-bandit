# Solving the problem
- We are told we need to find the password somewhere in the inhere folder
- But this time theres a bunch of folders and a bunch of files
- Going through each would be a pain, so we need a more efficient method
- We are going to try with find
    - The instructions say we the file should be 1033 bytes, readable and not executable
    - we are going to use the -size flag, -readable and ! -executable ( [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html))

```bash
bandit5@bandit:~/inhere$ find ./maybehere* -readable -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ find ./maybehere* -readable -size 1033c ! -executable
./maybehere07/.file2
bandit5@bandit:~/inhere$ find ./maybehere* -readable -size 1033c !-executable
-bash: !-executable: event not found
bandit5@bandit:~/inhere$ find ./maybehere* -readable -size 1033c ! -executable
./maybehere07/.file2
```
- We got the password
    - HWasnPhtq9AVKe0dmk45nxy20cvUa6EG