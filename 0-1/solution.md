# Solving the problem
- We know that the password for lvl 1 is stored in a file called readme in the home directory
    - We go ahead and `ls -l` in the current directory to see if there is a readme file.
    - There is a readme file
- We need to extract the password
    - we use `cat < readme` to read the file
- we found the password
    - ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
- we proceed to ssh to **bandit1** with the found password

