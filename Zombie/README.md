# Zombie [Miscellaneous]

NahamCon CTF 2023

*Oh, shoot, I could have sworn there was a flag here. Maybe it's still alive out there?*

```
Connect with:
# Password is "userpass"
ssh -p 32673 user@challenge.nahamcon.com
```

## Writeup

```bash
user@zombie:~$ ls -la

total 24
drwxr-sr-x    1 user     user          4096 Jun 18 12:44 .
drwxr-xr-x    1 root     root          4096 Jun 14 17:52 ..
-rwxr-xr-x    1 user     user          3846 Jun 14 17:52 .bashrc
-rw-r--r--    1 user     user            17 Jun 14 17:52 .profile
-rwxr-xr-x    1 root     root           131 Jun 14 17:52 .user-entrypoint.sh

```

```bash
user@zombie:~$ cat .user-entrypoint.sh

#!/bin/bash

nohup tail -f /home/user/flag.txt >/dev/null 2>&1 & # 
disown

rm -f /home/user/flag.txt 2>&1 >/dev/null

bash -i
exit
```

It is hinted that the contents of flag.txt, despite being deleted, is still stored somewhere in the memory since it was ran via `nohup`

```bash
user@zombie:~$ ps
PID   USER     TIME   COMMAND
    1 root       0:00 /usr/sbin/sshd -D -e
    7 root       0:00 sshd: user [priv]
    9 user       0:00 sshd: user@pts/0
   10 user       0:00 {.user-entrypoin} /bin/bash /home/user/.user-entrypoint.sh
   11 user       0:00 tail -f /home/user/flag.txt
   13 user       0:00 bash -i
   16 user       0:00 ps

```


```bash
user@zombie:~$ ls -la /proc/11/fd
total 0
dr-x------    2 user     user             0 Jun 18 12:49 .
dr-xr-xr-x    9 user     user             0 Jun 18 12:48 ..
lr-x------    1 user     user            64 Jun 18 12:49 0 -> /dev/null
l-wx------    1 user     user            64 Jun 18 12:49 1 -> /dev/null
l-wx------    1 user     user            64 Jun 18 12:49 2 -> /dev/null
lr-x------    1 user     user            64 Jun 18 12:49 3 -> /home/user/flag.txt (deleted)
```


```bash
user@zombie:~$ cat /proc/11/fd/3
flag{6387e800943b0b468c2622ff858bf744}
```
