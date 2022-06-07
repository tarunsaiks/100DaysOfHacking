# Linux Bandit Overthewire
## 7 -> 8:
Password is stored in data.txt, next to word millionth.

```bash
cat data.txt| sort | grep millionth
```

## 8 -> 9:
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once.

```bash
cat data.txt | sort | uniq -u
```

## 9 -> 10:
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

```bash
cat data.txt | strings | grep ====
```

## 10 -> 11:
The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

```bash
cat data.txt | sort | base64 -d
```

## 11 -> 12:
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

ROT13 is the algorithm used here. we can use `tr` to translate the text.

```bash
cat data.txt | tr a-zA-Z n-ma-zN-ZA-M
```

## 12 -> 13:
The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!).

```bash
$ mkdir /tmp/randomDir && cp data.txt /tmp/randomDir

$  cd /tmp/randomDir && file data.txt

$ xxd -r data.txt newdata

$ file newdata

# shows it is a gzip2 bin file

$ mv newdata newdata.gz

$ gzip -d newdata.gz

$ file newdata

# shows it is a bzip2 file but lacks bz2 extension

$ mv newdata newdata.bz2

$ bzip2 -d newdata.bz2

# for tar use `tar -xvf <fileName>`

```

## 13 ->14:
The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on.

```bash
ssh bandit14@localhost -i sshkey.private
```

## 14 -> 15:
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

## 15 -> 16:
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -ign_eof
```

`-ign_eof` is used to ignore the end of file.

## 16 -> 17:
The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

```bash
$ nmap localhost -p31000-32000

$ cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:<portNumber> -ign_eof
```

## 17 -> 18:
There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

```bash
diff password.new password.old
```

## 18 -> 19:
The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

```bash
sshpass -p `cat bandit18` ssh bandit18@bandit.labs.overthewire.org -p 2220 cat .bashrc
```

## 19 -> 20:
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

```bash
$ ./bandit20-do cat /etc/bandit_pass/bandit20
```


