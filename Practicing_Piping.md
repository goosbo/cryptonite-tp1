# Practicing Piping

This module deals with input and output redirection

## Redirecting output

Challenge description asks to use output redirection to write `PWN` to file `COLLEGE`

This can be done by:
`echo PWN > COLLEGE`
flag: `pwn.college{AaFNWR3HCN81NTvgr-S05tLVmbH.dRjN1QDL4kjN0czW}`

## Redirecting more output

Challenge asks to use output redirectiont to write the output of `/challenge/run` in file `myflag`

This can be done by,
`/challenge/run > myflag`

The flag is read by `cat myflag`, which gives the flag `pwn.college{oIg0DsG-uKka3dxxawdJOlVE_pf.dVjN1QDL4kjN0czW}`

## Appending output

output of `/challenge/run` must be directed to `~/the-flag` in append mode. If it is not in append mode second half of flag will overwrite the first half since first half is automatically written to the file and second half is directed to the file.

The required command is `/challenge/run >> ~/the-flag`

`cat the-flag` reads the flag `pwn.college{AdY1BCdHgUFQub46dVvB_toJyXW.ddDM5QDL4kjN0czW}`

## Redirecting errors

Output redirected to `myflag` like one of the previous challenges. Errors must be directed to `instructions`. This can be done using
```
/challenge/run > myflag 2> instructions
```

`cat myflag` reads the flag `pwn.college{cPRnvwf4Rq9DAlwFqgbfiNI84lg.ddjN1QDL4kjN0czW}`

## Redirecting input

First, output of `echo COLLEGE` is redirected to the file `PWN` using `echo COLLEGE > PWN`

Then, the file `PWN` is redirected as input to `/challenge/run` using `/challenge/run < PWN`

This gives the flag `pwn.college{sTsORxnt1kAEqkFGfNAEOovWhfi.dBzN1QDL4kjN0czW}`

## Grepping stored results

Output of `/challenge/run` is redirected to `/tmp/data.txt` using `/challenge/run > /tmp/data.txt`

The flag is searched using grep by the command `grep pwn.college /tmp/data.txt` since all flags start with `pwn.college`

flag: `pwn.college{EJzlroLaZtvBwDu8nuEP-Wrr5va.dhTM4QDL4kjN0czW}`

## Grepping live output

The output of the `/challenge/run` command needs to be connected to `grep pwn.college` using `|` to find the flag

`/challenge/run | grep pwn.college` gives the output:
```
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{468VQZZF8g2ypXu98vJDM6EMXXT.dlTM4QDL4kjN0czW}
```
Therefore the flag is found

## Grepping errors

Similar to previous challenge but errors must be grepped instead.

Standard error redirected to standard output first using `2>& 1`

Therefore the command is,
```
/challenge/run 2>& 1 | grep pwn.college
```

The flag outputted is: `pwn.college{ALf2Q2tnjiB85B-QTVCqxX6c2zR.dVDM5QDL4kjN0czW}`

## Duplicating piped data with tee

First, `tee` is used to intercept between `/challenge/pwn` and `/challenge/college` so we can find out what is going on. This is done by the command `/challenge/pwn | tee check | /challenge/college` 

`cat check` reads:
```
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "IVCKUKeN"
```

Therefore, the correct command to attain the flag is `/challenge/pwn --secret IVCKUKeN | /challenge/college` which outputs the following,

```
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{IVCKUKeNdF4gbGH4Nuz51vd_HpY.dFjM5QDL4kjN0czW}
```
Therefore the flag is attained.

## Writing to multiple programs

Output from `/challenge/hack` must be piped to the 2 commands `/challenge/the` and `/challenge/planet`.

Since `>(/challenge/the)` will give a temporary file which the command `/challenge/the` will read from, it can be used to make `tee` pipe to 2 commands.

The required command is,
```
/challenge/hack | tee >(/challenge/the) | /challenge/planet
```

flag: `pwn.college{IHsI5VGBRd_FVSp2IeRQG2hwqoe.dBDO0UDL4kjN0czW}`

## Split-piping stderr and stdout

This was a bit challenging to think of but I eventually found the right answer.

I first used `2>` along with `>(/challenge/the)` to pipe stderr to the `/challenge/the` program

Then I used the standard `|` that has been used in the last couple challenges to pipe stdout to `/challenge/planet`

```
/challenge/hack 2> >(/challenge/the) | /challenge/planet
```

This gives the output,
```
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{86m14QLtI9Ahq3Tmj167ald2tS-.dFDNwYDL4kjN0czW}
```