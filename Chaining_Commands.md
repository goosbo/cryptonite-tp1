# Chaining Commands

Module about chaining several commands together

## Chaining with Semicolons

`/challenge/pwn` and `/challenge/college` need to be chained together using `;`. This can be done using `/challenge/pwn; /challenge/college`, This gives the flag `pwn.college{snJ7_xt11Z2Z1H0aJHA_npTMJCD.dVTN4QDL4kjN0czW}`

## Your First Shell Script

The file `x.sh` is created using `touch x.sh`

I edited it using `nano` with `nano x.sh` and put the commands
```
/challenge/pwn
/challenge/college
```

Now this shell script is run using `bash x.sh`, this gives the flag `pwn.college{gu8LObEZsKdkOFHh0fHVl5ssZx6.dFzN4QDL4kjN0czW}`

## Redirecting Script Output

The output from `x.sh` in the previous challenge must be piped to `/challenge/solve`. this can be done by `bash x.sh | /challenge/solve`, this gives the flag `pwn.college{kCB6aaAdR-d5rxY_venSSkO4OM8.dhTM5QDL4kjN0czW}`

## Executable Shell Scripts

A script `y.sh` that contains `/challenge/solve` is made.
I make it executable using `chmod +x y.sh`
Running it using `./y.sh` gives the flag `pwn.college{01UdHqDrIDhlMB-33lu7Xu2gYlz.dRzNyUDL4kjN0czW}`