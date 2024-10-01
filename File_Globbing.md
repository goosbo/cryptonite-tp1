# File Globbing

module about globbing

## Matching with *

To get the flag, `/challenge/run` must be run with current working directory as `/challenge` but the cd command must be at most four characters.

The command I used to change directory into `/challenge` is `cd /ch*`
Then `./run` is executed
flag: `pwn.college{EXglw5AjRzfKlDF4-hvUroQKyF5.dFjM4QDL4kjN0czW}`

## Matching with ?

Exactly like the previous challenge but `?` must be used for the wildcard and there is no length limit.

Therefore sequence of commands are:
```
cd /?ha??enge
./run
```
flag: `pwn.college{EaXVQxqKCrqtQcU1m3BG1HgBkYy.dJjM4QDL4kjN0czW}`

## Matching with []

`cd` into `/challenge/files` with `cd /challenge/files`

`/challenge/run` needs to have one argument and we need to use a `[]` glob so that it contains `file_b`, `file_a`, `file_s` and `file_h`.

Command: `/challenge/run file_[absh]`
flag: `pwn.college{sdu2LQ_6q6f4Rr9WKM4tjxQl3Aw.dNjM4QDL4kjN0czW}`

## Matching paths with []

Same as the previous challenge but commands must be run from home directory.

```
/challenge/run /challenge/files/flag_[absh]
```
flag: `pwn.college{c-8sr3ab6_tqDhZYn08ocX-1qxp.dRjM4QDL4kjN0czW}`

## Mixing globs

run `cd /challenge/files` to go to the required directory

On running `ls`, it is seen that there are 26 files starting with a unique alphabet starting from a to z.

So to attain the flag, which requires "challenging", "educational" and "pwning" to be the arguments of `/challenge/run` with less than or equal to 6 characters, it is sufficient to use `[]` with c, e and p and then wildcarding every other character.

```
/challenge/run [cep]*
```
flag: `pwn.college{onjhCh1qG2OWrXP-WO0MHJTg3CL.dVjM4QDL4kjN0czW}`

## Exclusionary globbing

`cd` into `/challenge/files` just like previous challenges

Every file that does not start with p, w and n need to be used as an argument.
Therefore `[]` needs to be used with `!` right after the bracket opens and the characters pwn. Since the rest of the characters don't matter they are wildcarded with `*`.

```
/challenge/run [!pwn]*
```
flag: `pwn.college{0ES_n6EKtgjoaaxyJz7GdeJdcKa.dZjM4QDL4kjN0czW}`