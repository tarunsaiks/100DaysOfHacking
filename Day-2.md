# Linux Bandit Overthewire

[Bandit](https://overthewire.org/wargames/bandit/)

`ssh login: bandit.labs.overthewire.org`
`port : 2220`

```bash 
sshpass -p `cat bandit0` ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Rather than copy pasting password everytime, using sshpass is helpful in reading passwords from a file, however, not a very secure method to work with in wild.

## 0:
+ To connect to ssh, using default password as `bandit0`.
```bash
touch bandit0_password && echo bandit0 > bandit0_password
sshpass -p `cat bandit0_password` ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## 0 -> 1:
+ On successful login, check for files and directories using `ls`.
```bash
cat readme
```
 + copy the password.
 + store it in a different file or directly use ssh command and paste the password from clipboard. 
 + I prefer to use `sshpass` as it comes handy and passwords are stored in a file, so that I use it anytime.

## 1 -> 2:
+ ls gives a simple `-`
+ `-` is dashed filename.
+ and giving any command with `-` as argument, makes the shell refer to **stdin/stdout**, i.e at `/dev/stdin` and `/dev/stdout` .
+ to read the contents of dashed file, give full path of the file. 

```bash
cat ./-
```

+ copy the password.

## 2 -> 3:
+ spaces in the filename needs to be escaped, here use escape character `\` before a space.
+ or simply use `Tab` in keyboard to auto-fill.

## 3 -> 4:
+ inside folder `inhere`, it looks empty on normal `ls`.
+ use `ls -a` to list the hidden files and directories.
+ check for the contents of hidden file using `cat` or `more` or `less`.

## 4 ->5:
Given password is human readable
+ inside `inhere` directory there are 10 dashed files and one of them contains the password.
+ On using file command on all files that begin with `-`
```bash
file ./-*
```
+ you will find the password containing file.

## 5 -> 6:
Given that password has following properties
1. human readable
2. 1033 in bytes
3. non-executable

On checking the man page of `file`, 
+ It has an argument `-readable` to match files that are readable, using `access()` system call.
+ argument `size n[cwbkMG]`, n is the units of space used based on suffix from [cwbkMG]. 

```
`b'    for 512-byte blocks (this is the default if no suffix is used)
`c'    for bytes
`w'    for two-byte words
`k'    for Kilobytes (units of 1024 bytes)
`M'    for Megabytes (units of 1048576 bytes)
`G'    for Gigabytes (units of 1073741824 bytes)
```
+ Final command would be something like 
```bash
find -readable -size 1033c
```

## 6 -> 7:
The password for the next level is stored somewhere on the server and has all of the following properties:

1. owned by user bandit7
2. owned by group bandit6
3. 33 bytes in size

+ `find` has the argument to check `user` 
+ `find` has the argument to check `group`
```bash
find -user bandit7 -group bandit6 -size 33c
```

This gives alot of error messages, which can be removed using `2>/dev/null`

`2> file redirects stderr to file`

