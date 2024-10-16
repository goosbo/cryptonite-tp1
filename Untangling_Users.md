# Untangling Users

This module is all about users on a Linux system.

## Becoming the root with su

In this challenge, we need to use `su` to switch our user to `root`. `su` asks for the root password which in this case is `hack-the-planet`. After becoming `root` user, the flag can be read using `cat /flag` and it is `pwn.college{cYYnFxQ6GrPTJE6iRKSB8j0cQ4l.dVTN0UDL4kjN0czW}`

## Other users with su

In this challenge, we need to switch to the user `zardus` instead. This can be done with `su zardus` and the password is `dont-hack-me`. Now `/challenge/run` gives the flag `pwn.college{IIDH6w1TE7GucuIZYR-bzvG8Kxi.dZTN0UDL4kjN0czW}`

## Cracking passwords

A leak of `/etc/shadow` exists in `/challenge/shadow-leak`. It can be cracked using `john /challenge/shadow-leak` which gives the following output:
```
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:18 100% 2/3 0.05387g/s 313.7p/s 313.7c/s 313.7C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

Now you can used the password `aardvark` with `su zardus`
`/challenge/run` gives the flag `pwn.college{ID77UceD-vCMj2zO-BJbD4z9nEx.ddTN0UDL4kjN0czW}`

## Using sudo

We cannot run `cat /flag` since we do not have superuser permission.

Since we have `sudo` permission, `sudo cat /flag` works and gives the flag `pwn.college{U6fqA3Ui1dLY9nCFvYMBQA7l0Na.dhTN0UDL4kjN0czW}`