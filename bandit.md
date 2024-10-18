bandit stuff ig

# LEVEL 0

pretty straightforward

While I did know how to use ssh before, my understanding was limitied to it being a tool to connect to servers and other devices remotely. I learnt that it encrypts data to make the connection secure.

It requires a username and a domain name/ip address and also a password or key for authentication


`ssh bandit0@bandit.labs.overthewire.org -p 2220`
password: `bandit0`

# LEVEL 1

password is in a file called readme,
`cat readme` outputs the password `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

password: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

# LEVEL 2

password is in the `-` file, read using `cat ./-` since `-` is a special character
password: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

# LEVEL 3

you need to use `\` before a space to deal with filenames with spaces

`cat spaces\ in\ this\ filename`

password `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

# LEVEL 4

`cd inhere`

`ls -a` shows all files including hidden files and the output is:
```
.  ..  ...Hiding-From-You
```

`cat ./...Hiding-From-You` gives the password

password: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

