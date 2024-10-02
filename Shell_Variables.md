# Shell Variables

module about variables in shell scripting

## Printing Variables

You need to print the flag stored in variable `FLAG` using `echo`. The value in the variable can be accessed using `$` prepended to it.

Therefore,
`echo $FLAG` outputs the flag,
flag: `pwn.college{IaOKZWSn_669lH6L0nhJbn_ERIN.ddTN1QDL4kjN0czW}`

## Setting Variables

`PWN` needs to be set to `COLLEGE` to get the flag

This can be done by entering `PWN=COLLEGE` to the shell

The output is
```
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Qb7VAX0KOHPeu1C9OSfvC_xWFdG.dlTN1QDL4kjN0czW}
```

## Multi-word Variables

Similar to the previous challenge, but `PWN` must be set to `COLLEGE YEAH` which is two words. This can be achieved using `""` around `COLLEGE YEAH`

Therefore, `PWN="COLLEGE YEAH` which outputs the flag `pwn.college{MmFzM1efYfoq74fK5DkWayBmWP4.dBjN1QDL4kjN0czW}`

## Exporting Variables

First `PWN` is set to `COLLEGE` and exported using `export PWN=COLLEGE`

Then `COLLEGE` is set to `PWN` but not exported using `COLLEGE=PWN`

Then a child shell is invoked using `sh`

`/challenge/run` is run using arguments `PWN` and `COLLEGE`
```
/challenge/run PWN COLLEGE
```

This gives the flag `pwn.college{kyWa3MlUemrgy1bKjdkovv5CznP.dJjN1QDL4kjN0czW}`

## Printing Exported Variables

Running `env` gives the following output

```
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
DOJO_MODE=standard
PWD=/home/hacker
DOJO_AUTH_TOKEN=8a3094561693c0f7fbd2b4a31ac79e117b0511ca9f9f18e51a48397c5b2268ba
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
FLAG=pwn.college{gU8V_C_shluU1qutCBzJFUhI8nJ.dhTN1QDL4kjN0czW}
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm
LESSOPEN=| /usr/bin/lesspipe %s
SHLVL=1
LC_CTYPE=C.UTF-8
PATH=/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
_=/run/workspace/bin/env
```

From here it can be seen that `FLAG=pwn.college{gU8V_C_shluU1qutCBzJFUhI8nJ.dhTN1QDL4kjN0czW}`

## Storing Command Output

The output of `/challenge/run` can be stored in `PWN` using `PWN=$(/challenge/run)`

The flag is retreived by `echo PWN` which gives the output `pwn.college{wiJdq4UMJOUL2EmSQPSw1HU5LiQ.dVzN0UDL4kjN0czW}`

## READING INPUT

`COLLEGE` has to be read from the input by the user and put in variable `PWN`

Input is read to `PWN` by `read PWN`

Now I type `COLLEGE` and enter, this outputs the flag `pwn.college{A58XCitIA82Tak6MyaJRadEP18m.dhzN1QDL4kjN0czW}`

## READING FILES

`/challenge/read_me` must be read to variable `PWN` to get the flag

This can be done by using `<` from the previous module

`read PWN < /challenge/read_me`

This gives the flag `pwn.college{E0m6XH4lbf_cuZXn6Rl34WI-QSF.dBjM4QDL4kjN0czW}`