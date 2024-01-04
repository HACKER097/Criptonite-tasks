# Web Exploitation

## Logon

I tried logging in with username `Joe` and password `Joe123`, this did not work, and it told me that the password is very secure

Next I tried logging in with `admin` `admin`, which surprisingly worked. I soon realized that it works for any other username than `Joe`

I looked at the source code, which had nothing. Thr request we sent also didn't seem to have anything of importance.

I tried xss, and sql injection in the login feilds, both with no results. I don't know much about xss or sql injection, but it didn't seem to work with the guides I was looking at.

Finally I looked at the response cookie, which contained an `admin` variable, set to false. I changed it to true, and reloaded the page to find the flag

`picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}`

## Picobroswer

This one was very easy. I just had to put Picobroswer in my useragent. I have used this trick to get acces to bing chat without having to install Edge.

`picoCTF{p1c0_s3cr3t_ag3nt_84f9c865}`

## caas

Line 8 in the given code looks exploitable

`  exec(`/usr/games/cowsay ${req.params.message}`, {timeout: 5000}, (error, stdout) => {`

it is executing whatever you put at the end of the message, so you can do send a message like `hello;ls` and you will get the output of 'ls'.

```
< hello >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
Dockerfile
falg.txt
index.js
node_modules
package.json
public
yarn.lock
```

So `falg.txt` is right here. I wasted 25 mins here trying to cat out `flag.txt` instead of `falg.txt`. But finally I saw it. This is the final query I used. Using `%20` instead of space.

`curl "https://caas.mars.picoctf.net/cowsay/hello;cat%20falg.txt"`

## Forbidden Paths

This one was very easy. Paths that start with `/` are blocked, but you can just do `../` a bunch of times, and you will eventually reach the root directly, so i resuested the file `../../../../../../flag.txt` and got the flag.

## Local Authority

In the `login.php` found in the the html, we see these interesting lines

```php
          document.getElementById('msg').innerHTML = "Log In Successful";
          document.getElementById('adminFormHash').value = "2196812e91c29df34f5e217cfd639881";
          document.getElementById('hiddenAdminForm').submit();
```

So it is submitting a hiddn form using this. Lets see what happens when we run this in the console after an uncessful login.

We are redirected to admin.php, and the flag is found!!

# Reverse

## Shop

We must buy the flag, which costs 100, but we only have 40 coins.

So, I assume when I buy n amount of something which costs m, m x n is removed from my coins. So I entered the number of items I want to buy as a negetive number, which would remove a negetive number from my balance, which means coins are added to my balance. After buying the flag, i got this:

`Flag is:  [112 105 99 111 67 84 70 123 98 52 100 95 98 114 111 103 114 97 109 109 101 114 95 51 100 97 51 52 97 56 102 125]`

Which when unicode decoded gives 

`picoCTF{b4d_brogrammer_3da34a8f}`

## keygenme-py

This is the code I used, it is finding these indices [4,5,3,6,2,7,1,8] of `(hashlib.sha256(username_trial).hexdigest()` . Its the reverse of what they use to find the key.

```python
import hashlib

username_trial = b"FRASER"
key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_static2_trial = "}"

key =[]
index = [4,5,3,6,2,7,1,8]
for i in index:
    key.append(hashlib.sha256(username_trial).hexdigest()[i])

key_part_dynamic1_trial = "".join(key)

key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial
print(key_full_template_trial)
```

# Forensics

## tunn3l v1s10n

The file doesnt have a extention, so i tried `xxd tunn3l_v1s10n | less` to see the first 2 chars of the hexdump which are `BM` which means it is a bitmap (.bmp) file.

