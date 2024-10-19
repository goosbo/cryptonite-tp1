bandit stuff ig

# LEVEL 0

pretty straightforward

While I did know how to use ssh before, my understanding was limitied to it being a tool to connect to servers and other devices remotely. I learnt that it encrypts data to make the connection secure.

It requires a username and a domain name/ip address and also a password or key for authentication


`ssh bandit0@bandit.labs.overthewire.org -p 2220`
>password: bandit0

# LEVEL 1

password is in a file called readme,
`cat readme` outputs the password `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

>password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

# LEVEL 2

password is in the `-` file, read using `cat ./-` since `-` is a special character
>password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

# LEVEL 3

you need to use `\` before a space to deal with filenames with spaces

`cat spaces\ in\ this\ filename`

>password MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

# LEVEL 4

`cd inhere`

`ls -a` shows all files including hidden files and the output is:
```
.  ..  ...Hiding-From-You
```

`cat ./...Hiding-From-You` gives the password

>password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ


# LEVEL 5

Using `ls` in the `~/inhere` directory shows:
```
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
```

Now i used `file ./*` to print the file type of each directory(normally `file *` should work but the file names start with special characters)
this gives the output:
```
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

Since ASCII text is readable by humans I use `cat ./-file07`
which gives the password

>password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

# LEVEL 6

There are three requirements for the file with the password in `~/inhere`
human-readable, 1003 bytes in size and not executable

Looking at the `man` page for `find`, I found that `size` can be used to search for a file with a specific size
and if the number ends with a `c` it represents number of bytes
`find . -size 1033c` gives the output:
`./maybehere07/.file2`

Since there is only one file, the other factors don't have to be checked

`cat ./maybehere07/.file2` gives the password

>password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

# LEVEL 7

I thought of using `find` with all the requirements throughout the `/` directory to find the required file

The requirements are: owned by user bandit7,owned by group bandit6 and 33 bytes in size

`-user` and `-group` can be used with `find` to get the files with the required user and group

`find / -user bandit7 -group bandit6 -size 33c` would give the file with the password but it also shows a lot of errors.

I was thinking of making a temporary text file to pass the error stream to but bandit does not allow creating files, therefore I decided to pipe the output to `/dev/null` after a google search

`find / -user bandit7 -group bandit6 -size 33c 2> /dev/null`
this gives the output: `/var/lib/dpkg/info/bandit7.password`
`cat /var/lib/dpkg/info/bandit7.password` will give the password

>password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

# LEVEL 8

The password is in `data.txt` but in a specific line next to the word `millionth`

Therefore I decided to pipe the output of `cat data.txt` to `grep millionth` to output the specific line

`cat data.txt | grep milionth` gives the password

>password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

# LEVEL 9

The password is in the only unique line in `data.txt`

After looking at the `man` page for `uniq`, I found `-u` that only outputs the unique lines
Even though `data.txt` has lines occuring multiple times, they are scattered non-uniformly so I can use `sort` to output sorted lines and then pipe it to `uniq -u`

`sort data.txt | uniq -u`
This outputs the password

>password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

# LEVEL 10

The password is in a human readable string in `data.txt` and is preceded by `=`

the `strings` command seems to output readable lines in `data.txt`

If I pipe it with `grep =` it should output the possible options

`strings data.txt | grep =` outputs:
```
}========== the
p\l=
;c<Q=.dEXU!
3JprD========== passwordi
qC(=	
~fDV3========== is
7=oc
zP=	
~de=
3k=fQ
~o=0
69}=
%"=Y
=tZ~07
D9========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
N=~[!N
zA=?0j
```

Analysing the above output, the password is retrieved
>password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

# LEVEL 11

The password is in `data.txt` which is base64 encoded

According to it's man page `base64 -d` will decode a base64 encoded file

`base64 -d data.txt` gives the output:
`The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

>password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr 

# LEVEL 12

The password in `data.txt` is rot13 encrypted

the `tr` translates text to the condition given in the argument

`a` should become `n` and `n` should become `z` with each of the other letters following the required order
The same is done with upper case letters

`cat data.txt | tr a-zA-Z | n-ma-zN-ZA-M`
This gives the output: `The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

>password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

# LEVEL 13

I make a temporary directory using `mktemp -d` and copy `data.txt` to it

When I use `xxd data.txt` I see that the magic number is `1f8b` which is of a gzip file.
So I rename it to have a .gz extension and decompress it.
```
mv data.txt data.gz
gzip -d data.gz
```
This makes a decompressed file `data`

Now `xxd data` shows a magic number of `425a` which is that of a `bzip` file
```
mv data data.bz
bzip2 -d data.bz
```

`xxd data` again shows that it is a gzip file so the process to decompress it is done again just like done previously.

Now `cat data` shows that it contains a file `data5.bin` which means that it is a tar file
```mv data data.tar
tar -x -f data.tar
```
This decompresses it to show `data5.bin`

Similarly `data5.bin` seems to be a tar file since it contains `data6.bin`
The process is repeated and `data6.bin` is retrieved.

`xxd data6.bin` shows the magic number `425a` which means it is a bzip file
```
mv data6.bin data6.bz
bzip2 -d data6.bz
```
It decompresses it to give the file `data6`

`data6` is a tar file containing `data8.bin` and is decompressed like one of the previous cases

`data8.bin` has the magic number of a `gzip` file and is decompressed to `data8`

`cat data8` gives the password

>password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

# LEVEL 14

This time instead of a password a key is given that resides in the home folder.

To retrieve the key to my own pc, I used `scp` which can securely transfer files through a connection.

`scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`

This retrieves the key and now you can access level 14 with `ssh -i ./sshkey.private bandit14@bandit.labs.overthewire.org`

>password: given key
>in the next level we find that the password is MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

# LEVEL 15

The current password must be sent to local host at port 30000.

Since all passwords are stored in `/etc/bandit_pass`, level 14's password can be retrieved with `cat /etc/bandit_pass/bandit14`

`nc` can be used to transfer files by connection to a host

`nc 127.0.0.1 30000` connects to local host at port 30000 and now if I enter the current password, I get the password for level 15.

>password: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

# LEVEL 16

Just like the previous level, the current password should be sent to local host but at port 30001. This time it must be done with ssl/tls encryption.

`ncat` also can be used to tranfer files and it has a flag called `--ssl` that does so with ssl/tls encryption.

`ncat --ssl 127.0.0.1 30001` and now when I enter the current password I get the password for level 16.

>password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

# LEVEL 17

Similar to the previous challenges but the port is not given.

The port is said to be between 31000 and 32000 and has ssl/tls encryption

I used the port scanner `nmap` to find the right port

`nmap -sV -p31000-32000 127.0.0.1`

Here `-sV` does a service scan and prints the results which can be used to find the port with ssl/tls encryption and `-p31000-32000` scans within the required range of ports

the output is:
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-19 17:30 UTC
Stats: 0:00:42 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 0.00% done
Stats: 0:01:47 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 80.00% done; ETC: 17:32 (0:00:26 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0055s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```
the port `31518` seems to print out whatever is inputed

`ncat --ssl 127.0.0.1 31790` is the right connection and gives the key for the next level

```
rsa key: 
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

# LEVEL 18

`diff` prints the differences between 2 files

Since the password is stored in the only line that if different between `passwords.new` and `passwords.old`

`diff passwords.new passwords.old` will print out the difference and the output is:
```
42c42
< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
---
> ktfgBvpMzWKR5ENj26IbLGSblgUG9CzB
```

Therefore,
>password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

