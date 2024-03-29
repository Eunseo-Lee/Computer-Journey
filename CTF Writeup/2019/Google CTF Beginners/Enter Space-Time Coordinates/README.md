### Enter Space-Time Coordinates

![Screenshot](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Enter%20Space-Time%20Coordinates/Screenshot.PNG)

The challenge gives us an attachment with 2 files.
 `log.txt` and  `rand2`

The file `log.txt` contains what seems to be 5 different coordinates. 

```
0: AC+79 3888{6652492084280_198129318435598}
1: Pliamas Sos{276116074108949_243544040631356}
2: Ophiuchus{11230026071572_273089684340955}
3: Pax Memor -ne4456 Hi Pro{21455190336714_219250247519817}
4: Camion Gyrin{235962764372832_269519420054142}
```

The 64-bit ELF file `rand2` generates coordinates similar to log.txt, but different values each time the program is run.
`rand2` asks for user input, but I don't think that has anything to do with getting the flag. 

'strings' is a Linux command-line tool to find printable letters in files. 
In my Linux terminal, I ran the command:

`strings rand2 | grep CTF`

This gave me an immediate answer:
"Arrived at the flag. Congrats, your flag is: CTF{welcome_to_googlectf}"

At first I thought the coordinate values were something I'd have to decode using XOR, 
but thought the first challenge of beginners' CTF wouldn't be so hard. 
So I went with running the `strings` command first to find anything that would be useful. 
I didn't realize I'd get the flag on the first try, but it was a fun problem to get my mind
going to solve the next few problems. 

##### Flag: CTF{welcome_to_googlectf}
