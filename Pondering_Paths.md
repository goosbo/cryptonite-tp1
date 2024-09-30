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