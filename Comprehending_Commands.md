# Comprehending Commands

module about some useful Linux commands

## cat: not the pet, but the command!

The `flag` file is in the home directory and contains the required flag.

The text in the `flag` file can be read by using it's relative path as an argument with the `cat` command.

`cat flag` gives the flag `pwn.college{8f3pgfeT52ciZkd-cTMJU3Z5b_w.dFzN1QDL4kjN0czW}`.

## catting absolute paths

The `flag` file is now in the root directory.

The file can be read using `cat` just like the previous challenge but it's absolute path is used as an argument instead.

`cat /flag`
flag: `pwn.college{ULJdZLLR469NJbwgpwPcKxQUJ8B.dlTM5QDL4kjN0czW}`

## more catting practice

The `flag` file is in the `/lib/python3.8/config-3.8-x86_64-linux-gnu/` directory and it's absolute path must be used again.

`cat /lib/python3.8/config-3.8-x86_64-linux-gnu/flag`
flag: `pwn.college{A5CDyaYpRRUAQr9O3kpFctGu9aI.dBjM5QDL4kjN0czW}`


## grepping for a needle in a haystack

The flag is in the `/challenge/data.txt` which contains a hundred thousand lines.

The `grep` command must be used to print out the specific line that contains the flag.

The flag always starts with `pwn.college` therefore `grep pwn.college /challenge/data.txt` will retrieve the flag.
flag: `pwn.college{gshFWqfFG89n0lxMUG7Agd6UCCs.ddTM4QDL4kjN0czW}`

## listing files

`run` in `/challenge` has been renamed to something else.

After changing directory to `/challenge`, `ls` lists out all the files.

The new name for run is, `21978-renamed-run-7345`

```
    cd /challenge
    ls
    ./21978-renamed-run-7345
```
flag: `pwn.college{M1KRKhxG8MEZkYeMVrBae7rH5gE.dhjM4QDL4kjN0czW}`

## touching files

Two files `/tmp/pwn` and `/tmp/college` must be created for `/challenge/run` to output the flag.

They can be created by using the path of the required file as an argument for the `touch` command.

```
touch /tmp/pwn
touch /tmp/college
/challenge/run
```
flag: `pwn.college{oBy9ghXIPMexf_LM__pZrU-iXxx.dBzM4QDL4kjN0czW}`

## removing files

`delete_me` in the home directory must be removed for `/challenge/check` to output the flag.

This can be done using the relative path of `delete_me` as an argument for the `rm` command.

```
rm delete_me
/challenge/check
```
flag: `pwn.college{UNYZMd-lvAISpYqyV720RaHsmA6.dZTOwUDL4kjN0czW}`

## hidden files

The flag is in a hidden file in the root directory.

`ls -a` lists out all the files including hidden ones.

Using this command in the root directory shows `.flag-23971766530490` which contains the flag and it can be read using the `cat` command.

```
cd /
ls -a
cat .flag-23971766530490
```
flag: `pwn.college{suMYID-J8ZdM0XEAsGlhijvQ_Vn.dBTN4QDL4kjN0czW}`


## An Epic Filesystem Quest

The quest starts in the root directory : `cd /`

On using `ls`, a file `REVELATION` is seen.

`cat REVELATION` reads:
```
Tubular find!
The next clue is in: /opt/aflplusplus/nyx_mode/QEMU-Nyx/linux-user/host/s390x
```

So I cd into `/opt/aflplusplus/nyx_mode/QEMU-Nyx/linux-user/host/s390x` and run ls.
It shows a file `BLUEPRINT` that seems to have the next hint.
`cat BLUEPRINT` reads:
```
Tubular find!
The next clue is in: /etc/vulkan/icd.d
```

I cd into `/etc/vulkan/icd.d` and run ls.
It shows a file `SNIPPET` that seems to have the next hint.
`cat SNIPPET` reads:
```
The next clue is in: /usr/local/lib/python3.8/dist-packages/scapy/tools/automotive

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```

I cd into `/usr/local/lib/python3.8/dist-packages/scapy/tools/automotive` and run `ls -a` since the file is hidden.
The file `.TRACE` looks like the next hint.
`cat .TRACE` reads:
```
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/drivers/media/common/saa7146

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```

I use `ls /opt/linux/linux-5.4/drivers/media/common/saa7146` to find the file name without cding into the directory. The file seems to be called `README-TRAPPED`
`cat /opt/linux/linux-5.4/drivers/media/common/saa7146/README-TRAPPED` reads:
```
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/drivers/tty/serdev

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```

I cd into `/opt/linux/linux-5.4/drivers/tty/serdev` and run `ls` which shows `GIST` as the hint file.

`cat GIST` reads:
```
The next clue is in: /usr/share/qemu/keymaps

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```

Just like the last trapped file, I used `ls /usr/share/qemu/keymaps` which shows a file `TIP-TRAPPED`.
`cat /usr/share/qemu/keymaps/TIP-TRAPPED` reads:
```
Great sleuthing!
The next clue is in: /usr/lib/debug/.build-id/61
```

I cd into `/usr/lib/debug/.build-id/61` and run `ls` which shows a file `DISPATCH`.
`cat DISPATCH` reads:
```
Congratulations, you found the clue!
The next clue is in: /usr/local/share/radare2/5.9.5/syscall

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```

I run `ls /usr/local/share/radare2/5.9.5/syscall` which shows a file `ALERT-TRAPPED`
`cat /usr/local/share/radare2/5.9.5/syscall` reads:
```
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{EK-5G_iNeVRrSWX0t0OAfc-Cmvf.dljM4QDL4kjN0czW}
```