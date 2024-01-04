We are given a weird vryptic song as input. Digging a bit, we see that it is the rockstar language, which is a meme language. 

I found a line which looks interesting `If the music is a guitar`, which is clearly checking for something, lets see where this guitar variable is defined

`A guitar is a six-string`

Good, now according to rockstar lang doccumentation, each word's length corresponds to a digit, so "a six-string" translates to 136. When we run to code using an online compiler, it prints `Keep on rocking!` and asks for another input, which is checked using this line\

`If the rhythm without Music is nothing`

instead of trying to figure out more rockstar syntax, I just removed the line, hoping it would just continue working as if the line was evaluated to true. Running the code with the missing line, and giving 136 as the first input, we get a nre output.

![image](https://github.com/HACKER097/Criptonite-tasks/assets/38581702/f0d4ac83-5ee3-4d96-ba32-d9ac062a9706)

Converting these numbers to their corrosponding ASCII chars gives us `BONJOVI` whis becomes a flag when enclosed in `picoCTF{}`
