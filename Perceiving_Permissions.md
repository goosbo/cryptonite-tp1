# Perceiving Permissions

This module deals with Linux file permissions

## Changing File Ownership

In this challenge, `/file` must be accessed to get the flag but it is currently owned by `root` which makes `cat /flag` show permission denied.

The owner of the flag file can be changed by `chown hacker /flag` and now `cat /flag` gives the flag `pwn.college{oPH75ON8z4CNBL_NeNJziXEZpRQ.dFTM2QDL4kjN0czW}`

## Groups and Files

This challenge is similar to the previous challenge but the group of the file must be changed instead. This can be done by `chgrp hacker /flag` and invoking `cat /flag` gives the flag `pwn.college{8dIQA9kdEDqvnX3WCiZfCR-eIwJ.dFzNyUDL4kjN0czW}`

## Fun With Group Names

The challenge is like the previous challenge but the group of hacker is randamized.

Running `id` gives the output:
```
uid=1000(hacker) gid=1000(grp1393) groups=1000(grp1393)
```

Therefore, group that can access `/flag` is changed by `chgrp grp1393 /flag`

`cat flag` gives the flag `pwn.college{Yw_sGahw8msMzgG-PImHZs7otcF.dJzNyUDL4kjN0czW}`

## Changing Permissions

In this challenge the `/flag` only permits the `root` user to read it.

To make all other users(including hacker) be able to read it, `chmod o+r /flag` is used.

`cat /flag` now outputs the flag `pwn.college{w27lUzcEVbIiecz-fCR8oruLTaS.dNzNyUDL4kjN0czW}`