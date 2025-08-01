# Project
This repo holds my olutions for the bandit game from overthewire

site: https://overthewire.org/wargames/bandit

# SSH Connection
Every bandit level requires a `SSH` connection. 

The host is `bandit.labs.overthewire.org`, the port is `2220` and the username is the current level we are connection to. Every level connection will ask for a password, which we should have found in the previous level. For the first level, the password is provided for us as `bandit0`. Im on Linux, so the `SSH` syntax looks like `ssh USERNAME@HOST -p PORT` 

```bash
yosang@localhost:~$ ssh bandit0@bandit.labs.overthewire.org -p 2220
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit0@bandit.labs.overthewire.org's password:
```
The password will not be visible as we type.

Once we are in, we should receive a welcome text, and we are ready to play.

# Playing the game
Every level requires us to find a password, that we need in order to move on to the next level. The instructions state how the password is hidden, and what tools can help us find it.

Read the instructions, to figure out how to extract the password for the next level.

# Pup
Im using pup to generate the `instructions.md` files, with `curl` and `pup` to parse the html level descriptions.

```bash
curl https://overthewire.org/wargames/bandit/bandit13.html | pup '#content' > instructions.md
```

You can install `pup` from the main repo here: https://github.com/ericchiang/pup