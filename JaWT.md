# Observations

* The challange is called JaWT, might have something to do with JWTs
* Website says it works better in Google Chrome, maybe a chrome only feature is needed to solve this

I do not like chrome, so I changed my useragent here

# Cookie

The responce cookie has a JWT token, which when decoed (I used jwt.io) gives

## Header
```
{
  "typ": "JWT",
  "alg": "HS256"
}
```

## Payload
```
{
  "user": "John"
}
```

## Signature

Signatue is valid. When the username is changed to `admin` or anything else, it becomes invalid.

Looks like I need to find a signature header combination which will be valid.

# HS256

This is the algo mentioned in the header, google tells me its `a symmetric keyed hashing algorithm that uses one secret key`

It would be impossible to crack

# John

The website asks us to login as John, but the name is a link... to JohnTheRipper's github!

So from here its clear that we are supposed to brutrforce this thing. After looking at the man page and some googling, this is the command I used

`john thing.txt --wordlist=/home/hacker097/Desktop/stuff/wordlists/rockyou.txt --format=HMAC-SHA256`

Which after somes time gives me the key: `ilovepico`

Putting this back in jwt.io gives us out token, which we replace in our cookie, and reload to find our flag!!
