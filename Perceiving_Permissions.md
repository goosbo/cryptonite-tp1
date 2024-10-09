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

## Executable Files

`/challenge/run` is not executable by the user `hacker` who is the owner.

This can be changed by using `chmod u+x /challenge/run`

Now on running `/challenge/run`, the flag is `pwn.college{EMb_H0tzKPT3rxNy8c7KHzO0J9V.dJTM2QDL4kjN0czW}`

## Permission Tweaking Practice

Running `/challenge/run` outputs:
```
Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr--r-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```

Therefore to get the required permissions, I ran `chmod u+x,o+x /challenge/pwn ` which gives the output
```
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": rwxr--r-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxr-xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```

To achieve the above, I run `chmod g+x /challenge/pwn ` which outputs,
```
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": rwxr-xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rw-r--r-x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```

To achieve the above, I run `chmod u-x,g-x /challenge/pwn `, which outputs,
```
You set the correct permissions!
Round 3 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r-x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": ------r-x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```

To achieve the above, I run `chmod u-rw,g-r /challenge/pwn ` which gives the output:
```
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": ------r-x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

To achieve the above, I run `chmod o-rx /challenge/pwn ` which gives the output:
```
You set the correct permissions!
Round 5 (of 8)!

Current permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
```

To achieve the above, I run `chmod u+rwx,g+rwx,o+rwx /challenge/pwn` which gives the output
```
You set the correct permissions!
Round 6 (of 8)!

Current permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": ---rwxrwx
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
```

To achieve the above, I run `chmod u-rwx /challenge/pwn` which outputs,
```
You set the correct permissions!
Round 7 (of 8)!

Current permissions of "/challenge/pwn": ---rwxrwx
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": ---rwxr--
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

Finallly, I run `chmod o-wx /challenge/pwn ` which now changes `/flags` owner to `hacker`. I make it readable using `chmod u+r /flag` and then read the flag using `cat /flag` which outputs `pwn.college{gqIbM2V6_JLMFqvJgH8o2aSvbdy.dBTM2QDL4kjN0czW}`

## Permission Setting Practice

Challenge just like the previous one but `=` can be used to set the permissions while overwriting the previous permissions. For convenience, I will not show every output after each round, instead I will show the sequence of commands i used to finish the game after running `/challenge/run`.
```
chmod u=-,g+wx,o+x /challenge/pwn 
chmod u+wx,o+w /challenge/pwn 
chmod g=r,o-x /challenge/pwn 
chmod u=rw,g=-,o=- /challenge/pwn 
chmod g+w,o+wx /challenge/pwn 
chmod u=x,g=x,o=x /challenge/pwn
chmod u+r,g=w,o+w /challenge/pwn 
chmod u=w,g+rx,o+r /challenge/pwn 
```

After this, `/flag`'s owner is set to `hacker` and then I make it readable using `chmod u+r /flag`. On running `cat /flag` i get the flag 
`pwn.college{EI7ARfJO1JQQ-Ii92aVwkxDNkdZ.dNTM5QDL4kjN0czW}`

## The SUID Bit

In this challenge, `/challenge/getroot` opens a root terminal which can be used to access the flag.

To run `/challenge/getroot` the SUID bit must be set using `chmod u+s /challenge/getroot`.

Now on running `/challenge/getroot` the output is,
```
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:~#
```

Now, `cat /flag` gives the flag `pwn.college{M8CASyoebmPwM-6eRIE7qdl5hA7.dNTM2QDL4kjN0czW}`