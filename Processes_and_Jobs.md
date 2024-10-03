# Processes and Jobs

Module about viewing and interacting with processes

## Listing Processes

`/challenge/run` is renamed to something random and `ls` cannot be used in `/challenge`

The new `/challenge/run` process is already running so using `ps -ef` would show the new name of the process.

On running `ps -ef` the output is:
```
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 17:33 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 17:33 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 17:33 ?        00:00:00 /challenge/6957-run-14246
root          72      68  0 17:33 ?        00:00:00 sleep 6h
hacker        73       0  0 17:34 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        92      73  0 17:34 pts/0    00:00:00 ps -ef
```

The flag retrieved when running `/challenge/6957-run-14246` is:
`pwn.college{QXncIa_nO3y-K-fL0ZWBhEJSfrF.dhzM4QDL4kjN0czW}`

## Killing Processes

`/challenge/dont_run` must be killed before `/challenge/run` is executed so you get the flag.

The `PID` of `/challenge/dont_run` is found by using the `ps` command by:
`ps -ef | grep /challenge/dont_run`

This gives the output:
```
hacker        73      71  0 17:41 ?        00:00:00 /challenge/dont_run
hacker        93      75  0 17:41 pts/0    00:00:00 grep --color=auto /challenge/dont_run
```

The process is killed using `kill` by `kill 73`

Now running `/challenge/run` gives the flag `pwn.college{odlREhs_-4Ut_dwbzAprzgCEINQ.dJDN4QDL4kjN0czW}`

## Interrupting Processes

`/challenge/run` is run first and it gives the output:
```
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
```
After using the hotkey `Ctrl-C` it gives the flag `pwn.college{kTJJ8bBXflN_vHBZbT6RKUxidwu.dNDN4QDL4kjN0czW}`

## Suspending Processes

The first instance of `/challenge/run` is run.

It is suspended using the hotkey `Ctrl-Z`.

Then after running the next instance of `/challenge/run`, the flag outputted is `pwn.college{MBR6UAvFa-bj0ZgUtKiwbzo72MM.dVDN4QDL4kjN0czW}`

## Resuming Processes

Just like the previous challenge `/challenge/run` is run and then suspended using `Ctrl-Z`

Then it is resumed using `fg`

This gives the flag `pwn.college{ErDopYpOkB5-y8ZjwFrVW8TTNVu.dZDN4QDL4kjN0czW}`

## Backgrounding Processes

Just like the previous challenge `/challenge/run` is run and then suspended using `Ctrl-Z`

Then it is resumed in the background using `bg`.

Another instance of `/challenge/run` is run which gives the flag `pwn.college{8EjhWZaYd8vAkkGjPGvZ94-ugb-.ddDN4QDL4kjN0czW}`

## Foregrounding Processes

In this challenge, `/challenge/run` must be first run, then suspended then resumed in the background and then directly foreground the process.

This can be done using the following commands,
```
/challenge/run
Ctrl-Z
bg
fg
```

This gives the flag `pwn.college{0DFFvH26TnxeHYVm1zuNcZ8AhSy.dhDN4QDL4kjN0czW}`

## Starting Backgrounded Processes

`/challenge/run` needs to be backgrounded without suspending it first. This can be done by appending a `&` to the command:

`/challenge/run &`
This gives the flag: `pwn.college{8PVscUyOeJet6XdkKdSCyPTBkov.dlDN4QDL4kjN0czW}`

## Process Exit Codes

The exit-code of `/challenge/get-code` must be accessed and used as an argument for `/challenge/submit-code`.

After running `/challenge/get-code` the exit code is stored in the shell variable `?`

Therefore `echo $?` prints the exit code which is `208`

`/challenge/submit-code` gives the flag `pwn.college{EOOPr8poD66btSzR1wS2p8Kje4T.dljN4UDL4kjN0czW}`
