### Satellite

![Screenshot](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/Screenshot.PNG)

The challenge gives us two files: a pdf file and a runnable binary that seems to be pretty big for only a runnable file (3.2 mb)
`README.pdf` and `init_sat`. 
In other words, suspicious. 

![README.pdf](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/README.PNG)

This is what the README.pdf file looks like. Upon closer inspection, we can see the word
**osmium** drawn on the picture in the PDF file. 

After running init_sat, we are met with this particular text:
`
Hello Operator. Ready to connect to a satellite?
Enter the name of the satellite to connect to or 'exit' to quit
`
If we enter the wrong name, it will automatically thow this message:
`
Unrecognized satellite: test

Enter the name of the satellite to connect to or 'exit' to quit
`
From our README.pdf file, we found out that we need the word **osmium** for something.

![init_sat](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/init_sat.PNG)
It worked! 
There is a Google documents link where rest of the config data lies, and that should be our next clue. 

![Base64](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/base64.PNG)
This is what shows up on the Google doc, and it seems to be a base64 encoded string (*the two '=' equal signs at the end gave it away*).

After decoding the message, an interesting piece of text came up, which led to my next clue. 

`
Username: wireshark-rocks
Password: start-sniffing!
`

Wireshark is a network packet analyser. Which led to my next question: How was Wireshark related to this problem?
I thought back to the unusually big file size of 'init_sat'. Maybe it was doing something in the background in which
I can find out what, by running Wireshark while executing 'init.sat'. 







#### Unintended Solution:

The `strings` command works with this challenge as well, and I'm pretty sure this is an unintended solution. 
I solved the problem through this method first, then tried the method with Wireshark afterwards. 
Once we run the command `strings init_sat | grep satellite`, we get a large block of results. 

![netcat](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/netcat.PNG)

However, there is something that catches my eye. I've underlined the important part in red. 
This... looks like a netcat address! Lets try connecting.
`nc satellite.ctfcompetition.com 1337`

![flag](https://github.com/Eunseo-Lee/Computer-Journey/blob/master/CTF%20Writeup/2019/Google%20CTF%20Beginners/Satellite/Screenshots/flag.PNG)

The flag takes the place of what was obscured with asterisks when we first connected. At first, I tried the 
`string` command first to test my luck if I'd get the flag on my first try. After trying various words with the `grep` command
I went with 'satellite', and it worked. Imagine my excitement when I came by the netcat address. 

This was a shortcut to the solution, but I was unsatisfied with the way I solved it, and went back to do it the proper way. 

##### Flag: CTF{4efcc72090af28fd33a2118985541f92e793477f} 


