# Project
Solutions for the bandit game from overthewire

site: https://overthewire.org/wargames/bandit/

# Pup
Im using pup to generate the `instructions.md` files, with `curl` and `pup` to parse the html level descriptions.

```bash
curl https://overthewire.org/wargames/bandit/bandit13.html | pup '#content' > instructions.md
```

You can install `pup` from the main repo here: https://github.com/ericchiang/pup