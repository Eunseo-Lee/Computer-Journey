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
I thought back to the unusually big file size of 'init_sat'. Maybe, it was doing something in the background where I 
