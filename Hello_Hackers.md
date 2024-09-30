# Hello Hackers

This was the first module that had to be attempted on pwn.college and it was on executing commands with arguments in the command line.

## Intro to Commands

The description of the challenge states that invoking the `hello` command would give the required flag.

After you ssh into the challenge instance, the prompt `hacker@hello~intro-to-commands:~$ ` is seen.

In a previous example `whoami` is invoked by being typed into the prompt and pressing enter.

Therefore typing `hello` and pressing the enter key retrieves the required flag.

## Intro to Arguments

In the given example, arguments seem to follow the command after a space.

Since the description of the problem states that the command `hello` must be invoked with argument `hackers`, therefore `hello hackers` is entered in the prompt. This retrieves the required key.
