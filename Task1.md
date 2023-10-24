# Level 0

Just use ssh command ```ssh bandit0@bandit.labs.overthewire.org -p 2220``` to login, use the given password

# Level 0

Password is in the readme file, ```cat readme``` and then use given password to login to bandit1

# Level 1

Simple ```cat -``` does not work, I was surprised ```cat $(ls)``` or ```cat *``` does not work either.
I just did ```cat ./-```

# Level 2

Just cat ```cat *```, I know the intended solution is using `a\ b` but I didn't want to type that much over a slow ssh connection.

# Level 3

```
cd inhere
ls -a
cat .hidden
```

Again, my first attempt ```cat inhere/*``` did not work.

# Level 4

Just ls each file untill something human readable is printed. I am sure there is a better way, maybe using the find command, but this was easier and what I did.

# Level 5

Ok too may files here, have to use find command

```
find -type f -size 1033c
```

# Level 6

Same as level 5, just more files and more flags

# Level 7

Ez just use grep ```cat data.txt  | grep millionth```

# Level 8

```sort data.txt | uniq -u``` and then find the line which starts with 1. I should probably use awk for this, but I have forgotten it T-T

# Level 9

Just grep  again

# Level 10

Just do ```cat data.txt | base64 -d```

# Level 11

Just do rot13, I am not sure if there is a way to do this from terminal, I just went to rot13.com

# Level 12

xxd is installed, but ```cat data.txt | xxd -r /tmp/file.txt``` gave a garbage output.

file command tells us its gzip compressed data, so unzip by zcat, and repeat may times with other compression tools. This was very annoying and I had to look some commands up.

# Level 13 

Just login using ssh
```ssh -i sshkey.private -p 2220 bandit14@localhost```
and then cat the password

# Level 14

I used netcat here ```nc localhost 30000```

# Level 15

This was something I did not know about much. I did some reading on openssl, this is the commend I ended up using:
```openssl s_client -connect localhost:30001```

# Level 16

I used nmap to scan through the posts ```npam -p 31000-32000 localhost```
and tried the previous command all all 5 ports untill i got an output. This *can* be automated, but its easier for such less number of ports.

# Level 17

First to connect with ssh, we have to put output of level 16 in a .key file and login like this:
```ssh -i b17.key bandit17@bandit.labs.overthewire.org -p 2220```
Also ```chmod 400 b17.key``` because we get a warning

Then I used the diff command to find which line is different

# Level 18

This was hard, and took a lot of time. I Thought I had to modify the .bashrc somehow using the previous login, and it did not work. I tried may things to do that, none of which worked.

The commands you might need part is also very unhelpful here

I ended up googling "loginto ssh without bashrc" and came across the -t flag, which I used as follows:
```ssh -t bandit18@bandit.labs.overthewire.org -p 2220 /bin/sh```

the t flag can also just give me the output I want is I do ```cat readme``` ad the end instead of ```/bin/sh```

Also another weird solution is that if you press C-c fast enough after logging in, the .bashrc will not execute, and you are in!

# Level 19

This one was very easy
```./bandit20-do cat /etc/bandit_pass/bandit20```

# Level 20

Using netcat with & in the end so I can run it in the background:
```nc -l localhost 6969 < /etc/bandit_pass/bandit20 &```

And then ```./suconnect 6969```

# Level 21

This on was odd. I catted the bandit22 cronjob file, which had another file's name in it, which had another file's name in it, which has the password. Nothing to do with cronjobs at all

Anyway, this is the final password for level 22: **WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff**

I am putting it here to prove that I have done all previous levels, and so that I can continue q22 if needed for future tasks.
