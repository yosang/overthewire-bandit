# Solving the problem
We need to establish a connection to the game using SSH

The command format is `ssh user@remote-server -p PORT`

- The user represents the level we are connecting to, which in this case is **bandit0**
- The remote server is the server we are connecting to, which in this case is **bandit.labs.overthewire.org**
- We also need to provide a port, we do that with `-p` and the port here is **2220**
- On the next screen we are asked for a password, which is given in the instructions as **bandit0**