# Pondering Paths

challenge about file paths

## The Root

Flag is retreived by invoking the program `pwn`.

The program is in the root level so just entering `pwn` does not work since the shell starts at the home directory.

The absolute path `/pwn` invokes the command. Therefore the required flag is retrieved.

## Program and absolute paths

This challenge involves folders inside folders.

The program that retreives the flag is run which is inside challenge which is at the root level.

`directory structure: root -> challenge -> run`

the absolute path is therefore `/challenge/run`. Similar to the first challenge of the module, invoking the command with the absolute path works. This retrieves the required flag.

## Position thy self

When running the same command as the previous challenge, it is seen that the command is invoked from the wrong folder. 

Since it says that `/sys` is the right folder, the current working directory must be changed.

The problem description states that `cd` with an absolute path as an argument changes the current working directiory to that path.

Therefore the required commands should be:
```
cd /sys
/challenge/run
```

## Position elsewhere

Similar to the previous challenge. When `/challenge/run` is run, it asks us to go to `/var/lib/apt/lists`

```
cd /var/lib/apt/lists
/challenge/run
```

## Position yet elsewhere

Just like the previous two challenges. Required current working directory should be `/proc/67`

```
cd /proc/67
/challenge/run
```

## implicit relative paths, from /

Running `/challenge/run` does retrieve the flag. A relative path is required.

The challenge description states that the relative path of `/challenge/run` must be invoked from the `/` directory.

Therefore,
```
cd /
challenge/run
```
## explicit relative paths, from /

Just like the previous challenge, a relative path from `/` is required.

On running `challenge/run`, it states that the relative path must start with `.`.

The problem description states that `.` refers to the current directory.

Therefore,
```
cd /
./challenge/run
```

## implicit relative path

This time the current working directory must be `/challenge`.

The problem description states that you cannot use `run` to run the command due to a safety measure in Linux which ensures that programs in the current working directory that have the same name as important utilities are not executed.

Therefore explicitly running `./run` should work.

An observation here is the command used to ssh into the challenge uses the same explicit use of relative paths.
`ssh -i ./key hacker@dojo.pwn.college` - here ./key explicitly runs key

## home sweet home

`/challenge/run` must be run with an argument and a copy of the flag will be written in the file whose path is given as the argument. The argument size must be less than or equal to 3 characters and must be in the home directory and it should be absolute.

Since `~` is a shorthand for the absolute path of the home directory, it can be used with a file `a` in the home directory to get the required argument.

`/challenge/run ~/a`