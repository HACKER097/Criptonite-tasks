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


# Reverse

## Shop

We must buy the flag, which costs 100, but we only have 40 coins.

So, I assume when I buy n amount of something which costs m, m x n is removed from my coins. So I entered the number of items I want to buy as a negetive number, which would remove a negetive number from my balance, which means coins are added to my balance. After buying the flag, i got this:

`Flag is:  [112 105 99 111 67 84 70 123 98 52 100 95 98 114 111 103 114 97 109 109 101 114 95 51 100 97 51 52 97 56 102 125]`

Which when unicode decoded gives 

`picoCTF{b4d_brogrammer_3da34a8f}`

## 

