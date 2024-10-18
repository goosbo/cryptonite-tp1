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

