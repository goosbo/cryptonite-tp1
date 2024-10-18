# Pondering PATH

module abouth the PATH variable

## The PATH Variable

`/challenge/run` deletes the flag using `rm`. This can be avoided by just remvoing access to `rm`.
`PATH=""` empties the PATH variable and now `rm` can no longer be accessed

Running `/challenge/run` now gives the output
```
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{M8yddlzCNmPVI8dqaj5dlHFfTDg.dZzNwUDL4kjN0czW}
```

## Setting PATH

`/challenge/run` invokes `win` with it's bare name. Since `win` is in the `/challenge/more_commands/` directory, we need to add that to PATH.

`PATH="/challenge/more_commands/"`

Now running `/challenge/run`, gives the flag `pwn.college{QzDDYmKO7vM4vMnhI_YJQXtsO-e.dVzNyUDL4kjN0czW}`

## Adding Commands

So this challenge involves the following processes: create a shell script called `win` which gets the flag, set the PATH variable properly to access both `win` and whatever command required to retrieve flag(in this case `cat`) and then finally run `/challenge/run`

I created a folder called `windir` to have the `win` script in the home directory using `mkdir windir`
Then I used `cd windir` and then `touch win` to create the script
Edited the script using `nano` and added `cat /flag` to the file

Now I needed to figure out which folder `cat` was saved in so I could make sure to let it remain in the PATH variable

`echo $PATH` gives the output 
```
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

After analysing each of these locations I found out that `cat` is in `/usr/bin`
Therefore I set PATH using `PATH="/usr/bin:/home/hacker/windir"`

Now I ran `/challenge/run` but I got the output
```
Invoking 'win'....
/challenge/run: line 4: /home/hacker/windir/win: Permission denied
```

I had forgotten to make `win` executable, which I then did using `chmod +x win`

Now on running `/challenge/run` I got the flag `pwn.college{Qb8pa9EY8hjrgTIh-EqZyQnQYU9.dZzNyUDL4kjN0czW}`

## Hijacking Commands

In this module you need stop `/challenge/run` from deleting the flag by using `rm` and also print the flag.

My first idea was to create a script called `rm` that is basically a copy of `win` from the previous challenge and put the locations of only the new `rm` and `cat` in PATH.
The thing I didn't consider is that `rm` is in the same directory as `cat`.

Therefore I decided to use `read` instead of `cat`
I created the file `rm` in the directory `windir` from the previous challenge and added the following lines:
```
read VAR < /flag
echo $VAR
```

Then I set `PATH` to `"/home/hacker/windir"`

Now on running `/challenge/run` I get the output:
```
Trying to remove /flag...
pwn.college{8AithLf2pUQOihjZI0ah5Wuw1qK.ddzNyUDL4kjN0czW}
```