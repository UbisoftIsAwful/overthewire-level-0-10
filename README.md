# overthewire-level-0-10
Level 0:

To connect to the bandit0 host the ssh command is used. So first I googled ssh syntax given host, ip address, and port. One of the first commands that came up gave the syntax ssh [host]@[ipaddress] -p [port]. Entering that command connects the system to the bandit0 host. The terminal will then prompt the user for a password and this password is given for level 0 as bandit0. Now that a connection to bandit0 was successful the password to connect to the bandit1 host needs to be found. overthewire.org tells us the password is in a file in the home directory. So next I googled how to open files in the linux terminal. To find the name of the file first the files on the system are listed with the ls command. A file titled readme needs to be opened. This is done with the cat command. After the terminal outputs the password it is copy and pasted for level 1. So the terminal will look something like this to return the password. 

ubisoftisawful@Test:~$ ssh bandit0@bandit.labs.overthewire.org -p 2220
-
-
-
bandit0@bandit.labs.overthewire.org's password: 
-
-
-
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
[password]

Level 1:

Before starting level one the terminal is restarted to return to the original host and ip address on the machine. Then the same connection steps are taken to connect to the new host. Once connected the terminal will prompt for a password and the previous password is pasted into the terminal. overthewire.org tells us that the password is stored in a file titled '-'. However - is a reserved character in the linux terminal so typing 'cat -' the terminal assumes - is a command and nothing happens. The first thing i tried was quotes so the terminal would take the - as a string however this doesnt do anything either. So I googled how to read a file titled - in linux and the first result was to use ./. I have googled why this works and what this command does but all of the answers are vauge. From what I understand this tells the terminal to check the current directory for the file instead of the current path. Once the password is outputted it is again copied. The terminal will look something like this.

ubisoftisawful@Test:~$ ssh bandit1@bandit.labs.overthewire.org -p 2220
-
-
-
bandit1@bandit.labs.overthewire.org's password: 
-
-
-
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
[password]

Level 2:

Same as level one the terminal is restarted and all neccesarry connecitons are made. The terminal will again prompt for a password and the previous copied password is pasted and connection to bandit2 is made. To find the password for level 3 a file titled 'spaces in this filename' needs to be opened. The linux terminal assumes a new command is being typed when spaces are added so typing in 'cat spaces in this filename' will have the terminal search for a file titled 'spaces'. However what I tried on level 1, using quotes, tells the terminal to include spaces in the file string. Again the password is copied. The terminal will look something like this. 

ubisoftisawful@Test:~$ ssh bandit2@bandit.labs.overthewire.org -p 2220
-
-
-
bandit2@bandit.labs.overthewire.org's password: 
-
-
-
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat 'spaces in filename'
[password]

Level 3:

Same as the levels before the same connection and password entering steps are taken. Once connected a hidden file in the 'inhere' directory needs to be opened. So step one is to change directory to inhere which can be done easily by typing 'cd inhere'. Once in the correct directory the hidden files need to be listed. Of course I had no idea how to do that so I looked up how to list hidden files. For this level since the only file is the one hidden file a command listing all files including hidden ones can be used. the syntax is 'ls -a'. Once the name of the hidden file is found to be '.hidden' the same command as before 'cat .hidden' will output the contents of the file. The new password is copied and the terminal restarted for level 4. The terminal will look something like:

ubisoftisawful@Test:~$ ssh bandit3@bandit.labs.overthewire.org -p 2220
-
-
-
bandit3@bandit.labs.overthewire.org's password: 
-
-
-
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -a
            .hidden
bandit3@bandit:~/inhere$ cat .hidden
[password]

Level 4:

Same conncection and password steps are taken. Once connected to bandit4 overthewire.org tells us that the next password is in the only human readable file in the 'inhere' directory. So step one is to change to the inhere directory. Once in the in here directory listing the files returns files titled '-file0x' where x goes from index 0 to 9. Because the files start with '-' the same prefix from level 1 is needed './' before the filename. Going through each file one by one returns unreadable characters until -file07 which returns the password in a readable form. The terminal will look something like this.

ubisoftisawful@Test:~$ ssh bandit4@bandit.labs.overthewire.org -p 2220
-
-
-
bandit4@bandit.labs.overthewire.org's password: 
-
-
-
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
bandit4@bandit:~/inhere$ cat ./-file00
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file01
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file02
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file03
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file04
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file05
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file06
[unreadable characters]
bandit4@bandit:~/inhere$ cat ./-file07
[password]

Level 5:

To find the password for level 6 overthewire.org tells us that the neccesary file has the following properties: human readable, 1033 bytes, non-executable. The file is also found in the inhere directory so changing directory is step one. The find command has a size field that can be used. Finding the correct syntax was troublesome however eventually I found it. The issue I was having was with what the terminal defaulted to. The terminal by default assumes 512 byte blocks. however we just want bytes and the suffix for bytes is not b but c. so the command will look something like 'find -size 1033c' luckily there is only one 1033 byte file. The terminal will look something like:

ubisoftisawful@Test:~$ ssh bandit5@bandit.labs.overthewire.org -p 2220
-
-
-
bandit5@bandit.labs.overthewire.org's password: 
-
-
-
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
maybehere04  maybehere07  maybehere11  maybehere15  maybehere19
bandit5@bandit:~/inhere$ find -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere/.file2
[password]

Level 6:

To find the password for level 7 overthewire.org tells us the needed file has the following properties: owned by user bandit7, owned by group bandit6, 33 bytes. The find command also has syntax for user and group specifications so it can be used here aswell. I struggled with this one aswell typing 'find -user bandit7 -group bandit6 -size 33c' first and returning nothing. I had to google the soulution for this one. I was missing a '/'. So I suppose I had to specify to the machine to look through the root directory instead f the home directory. So the command 'find / -user bandit7 -group bandit6 -size 33c'. will return 100s of files most of which the user has no access to. To get rid of any lines that return an error message we append the command with '2>/dev/null'. This dumps lines returned with an error message to what is essentially a recycle bin. The terminal will look something like:

ubisoftisawful@Test:~$ ssh bandit6@bandit.labs.overthewire.org -p 2220
-
-
-
bandit6@bandit.labs.overthewire.org's password: 
-
-
-
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
[password]

Level 7:

To get the password for level 8 a text file is given and the password we need is next to the word miilionth. Using the cat command prints thousands of lines so finding millionth would be fairly difficult. The grep command can be used to only return the line starting with millionth. The command will look something like 'cat data.txt | grep millionth'. The terminal will look like:

ubisoftisawful@Test:~$ ssh bandit7@bandit.labs.overthewire.org -p 2220
-
-
-
bandit7@bandit.labs.overthewire.org's password: 
-
-
-
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       [password]

Level 8:
