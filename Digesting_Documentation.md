# Digesting Documentation

Module about reading documentatin of programs

## Learning From Documentation

Running the command `/challenge/challenge` gives the flag but it works only when the argument is `--giveflag`(as mentioned in the problem description).

```
/challenge/challenge --giveflag
```
flag: `pwn.college{AG9urZnIJ5Ep_vGp7VVoYm5RniP.dRjM5QDL4kjN0czW}`

## Learning Complex Usage

The documentation states that `/challenge/challenge` when used with argument `--printfile` prints the contents of the argument of `--printfile`. Therefor to obtain the flag `/flag` must be used as its argument.

```
/challenge/challenge --printfile /flag
```
flag: `pwn.college{8NBy8CdCOGuJc91CRwz-J4cpOuw.dVjM5QDL4kjN0czW}`

## Reading Manuals

On running `man challenge`, the description was:
```
DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --fcwpyw NUM
              print the flag if NUM is 882

```
Therefore to attain the flag, we must run:
```
/challenge/challenge --fcwpyw 882
```
flag: `pwn.college{8Ofc-8wp28ByZI_wlfK4svHHyzY.dRTM4QDL4kjN0czW}`

## Searching Manuals

On running `man challenge` and navigating by searching for `flag` using `/flag` and using `n` to go to the next location, `--frjd This argument will give you the flag!1=` is seen.

Therefore to attain the flag,
```
/challenge/challenge --frjd
```
flag: `pwn.college{sy6aa3i4IENRV12Vtf92RqVKXvk.dVTM4QDL4kjN0czW}`

## Searching For Manuals

On running `man man` and scrolling down, I noticed
```
man -k printf
           Search the short descriptions and manual page names for the keyword  printf  as  regular
           expression.  Print out any matches.  Equivalent to apropos printf.
```

So I used `man -k flag` which gave the output:
```
dpkg-buildflags (1)  - returns build flags to use during package build
Dpkg::BuildFlags (3perl) - query build flags
fegetexceptflag (3)  - floating-point rounding and exception handling
fesetexceptflag (3)  - floating-point rounding and exception handling
i386 (8)             - change reported architecture in new program environment and/or set personali...
ioctl_iflags (2)     - ioctl() operations for inode flags
linux32 (1)          - change reported architecture in new program environment and/or set personali...
linux64 (1)          - change reported architecture in new program environment and/or set personali...
pcap-config (1)      - write libpcap compiler and linker flags to standard output
security_compute_av_flags (3) - query the SELinux policy database in the kernel
security_compute_av_flags_raw (3) - query the SELinux policy database in the kernel
sejoxzuurw (1)       - print the flag!
set_matchpathcon_flags (3) - set flags controlling the operation of matchpathcon or matchpathcon_in...
set_matchpathcon_invalidcon (3) - set flags controlling the operation of matchpathcon or matchpathc...
set_matchpathcon_printf (3) - set flags controlling the operation of matchpathcon or matchpathcon_i...
setarch (1)          - change reported architecture in new program environment and/or set personali...
setarch (8)          - change reported architecture in new program environment and/or set personali...
x86_64 (8)           - change reported architecture in new program environment and/or set personali...
```

Therefore running `man sejoxzuurw` gives the man page of the challenge program.
In the man page, 
```
--sejoxz NUM
        print the flag if NUM is 846
```
is seen. Therefore the required command to get the flag is,
```
/challenge/challenge --sejoxz 846
```
flag: `pwn.college{8UIsejoR-RxAz4uurHwo6ESxSN2.dZTM4QDL4kjN0czW}`

## Helpful Programs

On running `/challenge/challenge --help` the output is,
```
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
```

The output of `/challenge/challenge -p` is,
```
The secret value is: 738
```

Therefore to get the flag, the command that should be run is,
```
/challenge/challenge -g 738
```
flag: `pwn.college{gELpboEu7E38S7onK6BGZKj9Kgk.ddjM4QDL4kjN0czW}`

## Help for Builtins

On running `help challenge`, the output is,
```
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune		display a fortune
      --version		display the version
      --secret VALUE	prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "QauKB4nN".
```

Therefore the command to get the flag is,
```
challenge --secret QauKB4nN
```
flag: `pwn.college{QauKB4nNsNgBxofm5MmsmlYQR5f.dRTM5QDL4kjN0czW}`