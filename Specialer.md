After connecting throught ssh, its clear that most common commands such as `cat` or `ls` do not work. The challenge mentions that it does has autocompelete functionality, so lets see what happens when he press tab 2 times.

![image](https://github.com/HACKER097/Criptonite-tasks/assets/38581702/fd5a574a-30cd-4c77-9110-6c695ef6f1e1)

Nice, now we can see all the commands avalable to us.

Typing `cd` and then tab shows us all the files, we no longer need the ls command.

![image](https://github.com/HACKER097/Criptonite-tasks/assets/38581702/8cc520d2-68a8-4198-a721-4a752d5cc22c)

![image](https://github.com/HACKER097/Criptonite-tasks/assets/38581702/1998e56f-cbc4-4a9c-ad95-b606cfe98de8)

None of the files seem to be labled as a flag, so I guess we will just have to cat each one to see whats in them, Without usiong the cat command somehow. 

This can be done using `<` which is used to redirect input from a file, similar or pipes. After doing this for each file one by one, we find our flag!

![image](https://github.com/HACKER097/Criptonite-tasks/assets/38581702/77cb8edd-e4e5-40cf-8550-413db19458c3)
