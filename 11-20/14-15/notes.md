- To get to level 15, we need to use the password we got in bandit14
- The instructions stay that we need to submit the password to localhost on port 30000
- We watched the first video in recommended resources [How the internet works in 5 mins](https://www.youtube.com/watch?v=7_LPdttKXPc) to get an idea of what is expected of us in this level.
- By the looks of it we just need to connect over IP, send over some text (in this case the bandit14 password) and we should receive bandit15 password back, looking at `telnet`, it looks like what we need.

```bash
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

- We got the the password
    - 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo