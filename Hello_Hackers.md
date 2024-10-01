# Hello Hackers

This was the first module that had to be attempted on pwn.college and it was on executing commands with arguments in the command line.

## Intro to Commands

The description of the challenge states that invoking the `hello` command would give the required flag.

After you ssh into the challenge instance, the prompt `hacker@hello~intro-to-commands:~$ ` is seen.

In a previous example `whoami` is invoked by being typed into the prompt and pressing enter.

Therefore typing `hello` and pressing the enter key retrieves flag `pwn.college{cFfM4RO8xoeCObkugP-g0XtU6Vp.ddjNyUDL4kjN0czW}`.

## Intro to Arguments

In the given example, arguments seem to follow the command after a space.

Since the description of the problem states that the command `hello` must be invoked with argument `hackers`, therefore `hello hackers` is entered in the prompt. This retrieves the key `pwn.college{8Cue8xogWMbqs51WJYOdZmMDtuO.dhjNyUDL4kjN0czW}`.
