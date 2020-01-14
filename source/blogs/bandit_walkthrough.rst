Bandit Walkthrough
==================
`< Blog <../blog.html>`_

Walkthrough of Bandit, a wargame by OverTheWire

Created on: 2020-01-09

.. role:: kbd

.. warning:: I know in the server banner is says 'again, DONT POST SPOILERS! This includes writeups of your solution on your blog or website!'. I fully respect that thus this is my duty to warn the reader not to use this to cheat in the game. This is just a personal note in an attempt to getting started with CTF writeup. I choose Bandit because it is easy and CTF/Techinal writeups are tough enough. I have been using Linux for sometime now and I can assure you that copy-pasting commands without understanding to cross a level or fix a problem don't make you a expert, it makes you a unprepared imposter and good mouse user. So DO NOT USE this to play the game! Use it as a getting started guide to write CTF writeup.

From the Bandit webpage::

    The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.

Presequisite
------------
To play Bandit we will need a `Terminal emulator <https://en.wikipedia.org/wiki/Terminal_emulator>`_ and a `SSH client <https://www.ssh.com/ssh/client>`_. If we are in Linux Or macOS then we should already have both of this available in our machine. If we are in Windows then `Cmder <https://cmder.net/>`_ is the way to go!  We will also need a working internet connection.

Starting the game
-----------------
To start playing the Bandit wargame:

- Open `Bandit <https://overthewire.org/wargames/bandit>`_ wargame webpage in a browser.
- Open a terminal emulator
- Start reading the instructions in the webpage and follow them to get started.

The game is deviled into levels. Current level has the password for the next level. So, if we go to the `Bandit Level 0 → Level 1 <https://overthewire.org/wargames/bandit/bandit1.html>`_ page we will see the goal if Level 0. If we successfully achieve that goal we will be able to go to Level 1.

Level 0
-------
To start we need to type in our terminal::

    ssh bandit0@bandit.labs.overthewire.org -p 2220

It will ask our permission to add the host to the list of known hosts. Type `yes`. Then it will ask for the password. The password for this level is given and it is *bandit0*. Typing that will allow us to enter the game which is a Linux machine with rather long `motd <https://en.wikipedia.org/wiki/Motd_(Unix)>`_. 

The goal set for Level 0 is to find file called **readme** located in the home directory. After login with SSH, generally the user lands on the home directory. So let's see if we can find the file with `ls`_::

    bandit0@bandit:~$ ls
    readme
    bandit0@bandit:~$ 

There we have our file. Now let's see the content of the file with `cat`_::

    bandit0@bandit:~$ cat readme 

We should be able to see a 33 character long string. This is our password for Level 1.

Now we need exit from the machine::

    bandit0@bandit:~$ exit
    logout
    Connection to bandit.labs.overthewire.org closed.


Level 1
-------
First let's go to Level 1::

    ssh bandit1@bandit.labs.overthewire.org -p 2220

This will ask for password and use the string from previous level. To go to next level we need to get the content of a file called **-** located in the home directory. If we try `cat`_-ing the file as before is hangs::

    bandit1@bandit:~$ cat -


Pressing :kbd:`Ctrl` + :kbd:`c` will give us back our terminal. The `cat`_ command doesn't work on the **-** file because it indicates stdin or stdout.


.. read the links bellow to explane more:
    https://www.tldp.org/LDP/abs/html/special-chars.html#DASHREF2
    https://stackoverflow.com/questions/8045479/whats-the-magic-of-a-dash-in-command-line-parameters
    https://unix.stackexchange.com/questions/16357/usage-of-dash-in-place-of-a-filename

To see the content of the file::

    bandit1@bandit:~$ cat ./-

We should be able to see a 33 character long string aka the flag. This is our password for Level 2. Now exit from the machine as before with the `exit`_ command.


Level 2
-------
First let's go to Level 2::

    ssh bandit2@bandit.labs.overthewire.org -p 2220

Use the password from previous level as before. The password for the next level is in a file called **spaces in this filename**.

Let's try to see the file with `ls`_::

    bandit2@bandit:~$ ls
    spaces in this filename
    bandit2@bandit:~$ 

If we try to see the file by typing `cat spaces in this filename`, we get::

    bandit2@bandit:~$ cat spaces in this filename
    cat: spaces: No such file or directory
    cat: in: No such file or directory
    cat: this: No such file or directory
    cat: filename: No such file or directory
    bandit2@bandit:~$ 

This is because with the spaces the `spaces`, `in`, `the` and `filename` are treated as separate file and obviously those doesn't exit. We can solve it by escaping the space with *`\`* ::

    bandit2@bandit:~$ cat spaces\ in\ this\ filename

P.S: we don't need to type those, just hit :kbd:`Tab` to autocomplete. 

We should be able to see the flag with Level 3 login password. Now exit from the machine.


Level 3
-------
Entering the Level 3 machine::

    ssh bandit3@bandit.labs.overthewire.org -p 2220

Use the password from previous level as before. The password for the next level is in a **hidden** file in the **inhere** directory.

Let's see what we have in our current directory with `ls`_::

    bandit3@bandit:~$ ls
    inhere
    bandit3@bandit:~$ 

As expected we see the `inhere` directory. Let's go inside the directory with `cd`_ command::

    bandit3@bandit:~$ cd inhere/
    bandit3@bandit:~/inhere$ 

Now we are inside the `inhere` directory. Now we will use `ls`_ again to list all files and we see this::

    bandit3@bandit:~/inhere$ ls
    bandit3@bandit:~/inhere$ 

Or do we? We can't see any file here. Now if we remember the goal we or file is a **hidden** file and the `ls`_ command list all file except for the hidden one. We will use a additional flag of the `ls`_ command to see the hidden files. The flag is `-a` which is pronounced `dash or tack a`. So let's see the file::

    bandit3@bandit:~/inhere$ ls -a
    .  ..  .hidden
    bandit3@bandit:~/inhere$ 

There we see the `.hidden` file. The `.` and the `..` before the `.hidden` are reference to the current and one directory up from the current directory. Finally, to see the content of the file::

    bandit3@bandit:~/inhere$ cat .hidden 


We should be able to see the password for Level 4. Now exit from the machine.

Level 4
-------
Entering the Level 4 machine using the password from previous level::

    ssh bandit4@bandit.labs.overthewire.org -p 2220

The password is in is stored in the **only human-readable** file in the **inhere** directory

Now if we follow the previous level to enter the `inhere` directory and list file, we see::

    bandit4@bandit:~/inhere$ ls
    -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
    bandit4@bandit:~/inhere$ 

Now if we try to see the content of the first file `-file00`, we use `cat`_ command like we did on `Level 1`_ and see this::

    bandit4@bandit:~/inhere$ cat ./-file00
    ����������~%    C[�걱>��| �bandit4@bandit:~/inhere$ 

What is this gibberish!? Let's see what kind of file it is with `file`_ command::

    bandit4@bandit:~/inhere$ file ./-file00
    ./-file00: data
    bandit4@bandit:~/inhere$ 

So this is a data file and is most definitely not *human-readable* which is what our file is. Now we can use the `file`_ command to check the file type of each 10 files and see which one is human-readable but that is very useful when we have hundreds or thousands of files. We can use the wild character `*` to specify all the files in a directory and as we know our file is in the `inhere` directory we can run `file`_ command on all the files of `inhere` directory::

    bandit4@bandit:~/inhere$ file ./*
    ./-file00: data
    ./-file01: data
    ./-file02: data
    ./-file03: data
    ./-file04: data
    ./-file05: data
    ./-file06: data
    ./-file07: ASCII text
    ./-file08: data
    ./-file09: data
    bandit4@bandit:~/inhere$ 

We can see that the `-file07` file has `ASCII text <https://en.wikipedia.org/wiki/Ascii>`_ which is human-readable. We can see the password for Level 4 by::

    bandit4@bandit:~/inhere$ cat ./-file07

Now exit from the machine.

Alternative solution
````````````````````
We could have used the `-i` flag of `file`_ command to see the mime type strings of the files and find the file as well::

    bandit4@bandit:~/inhere$ file -i ./*
    ./-file00: application/octet-stream; charset=binary
    ./-file01: application/octet-stream; charset=binary
    ./-file02: application/octet-stream; charset=binary
    ./-file03: application/octet-stream; charset=binary
    ./-file04: application/octet-stream; charset=binary
    ./-file05: application/octet-stream; charset=binary
    ./-file06: application/octet-stream; charset=binary
    ./-file07: text/plain; charset=us-ascii
    ./-file08: application/octet-stream; charset=binary
    ./-file09: application/octet-stream; charset=binary


Level 5
-------
Entering the Level 5 machine using the password from previous level::

    ssh bandit5@bandit.labs.overthewire.org -p 2220

Like before the password in in a directory named **inhere** which is **human-readable**, **1033 bytes in size** and **not executable**. If we see the contents of the file::

    bandit5@bandit:~$ ls inhere/
    maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
    maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
    bandit5@bandit:~$ 

That is a lot of directory! If we want to go through all those directory to find our specific file it would take a lot of time. We can use the `find`_ command to assist us in our task::

    bandit5@bandit:~$ find inhere/ -type f -size 1033c ! -executabl
    inhere/maybehere07/.file2
    bandit5@bandit:~$ 

We get one file in return! Before we use our known commands to see the attributes of the file to match our criteria, let's first see what the `find`_ command did. If we check the man page for `find`_ command, we see `-type` flag checks for file type and `f` is used for regular file, the `-size` flag checks the size of a file as for size in byte we use `c` after the numeric value. Finally, the `-executable` flag checks if the file is executable. We used `!` to as NOT operator so it check if the file is NOT executable. To understand complex commands we can use `explainshell.com`_. 

Now let's check if the file the `find`_ command found for us matches the criteria by using known commands.

- Is it **human-readable**?::

    bandit5@bandit:~$ file inhere/maybehere07/.file2
    inhere/maybehere07/.file2: ASCII text, with very long lines
    bandit5@bandit:~$ 

It is ASCII text.

- Is it **1033 bytes in size**?::

    bandit5@bandit:~$ ls -la inhere/maybehere07/.file2
    -rw-r----- 1 root bandit5 1033 Oct 16  2018 inhere/maybehere07/.file2
    bandit5@bandit:~$ 

It is 1033 bytes in size.

- Is it **not executable**?

From the previous output of `ls`_ command we can see that the file `inhere/maybehere07/.file2` is not executable. To see the password for Level 6::

    bandit5@bandit:~/inhere$ cat inhere/maybehere07/.file2

Now exit from the machine.


Level 6 
-------
Use the password from previous level to get into Level 6::

   ssh bandit6@bandit.labs.overthewire.org -p 2220


The password is saved **somewhere on the server** and is **owned by user bandit7**, **owned by group bandit6** and **33 bytes in size**. Lets see if we have any file or directory in the home directory::

    bandit6@bandit:~$ ls
    bandit6@bandit:~$ 

No files. Are there any hidden files in the home directory?:: 

    bandit6@bandit:~$ ls -la
    total 20
    drwxr-xr-x  2 root root 4096 Oct 16  2018 .
    drwxr-xr-x 41 root root 4096 Oct 16  2018 ..
    -rw-r--r--  1 root root  220 May 15  2017 .bash_logout
    -rw-r--r--  1 root root 3526 May 15  2017 .bashrc
    -rw-r--r--  1 root root  675 May 15  2017 .profile
    bandit6@bandit:~$ 

This are the common hidden files in a users home directory. Let's widen our search radius to the whole file system with `find`_ command::

    bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
    find: ‘/run/lvm’: Permission denied
    find: ‘/run/screen/S-bandit33’: Permission denied
    find: ‘/run/screen/S-bandit13’: Permission denied
    ... 
    /var/lib/dpkg/info/bandit7.password
    ...
    find: ‘/proc/1056/fd/5’: No such file or directory
    find: ‘/proc/1056/fdinfo/5’: No such file or directory
    find: ‘/boot/lost+found’: Permission denied

We can see one file named `/var/lib/dpkg/info/bandit7.password` that can be our desire file but first let's see the explanation of the `find`_ command used to find the file. The man page for find or in the `explainshell.com`_ site of `find`_ command can be used for this. We will always prefer the man page but just for a change and more ease of use we can use `explainshell.com`_. Now if we go to the `explainshell.com`_ site and paste the `find / -user bandit7 -group bandit6 -size 33c <https://explainshell.com/explain?cmd=find+%2F+-user+bandit7+-group+bandit6+-size+33c>`_ command we see a nice segmented command with explanation with each segment. The `-user` flag finds file of a specific user name, the `-group` flag finds file of a specific group and the `-size` flag works exactly like we explained before in `Level 5`_.

We can also check if the file matches our criteria by only using `ls`_::

    bandit6@bandit:~$ ls -la /var/lib/dpkg/info/bandit7.password
    -rw-r----- 1 bandit7 bandit6 33 Oct 16  2018 /var/lib/dpkg/info/bandit7.password
    bandit6@bandit:~$ 

As we can see the file is indeed **owned by user bandit7**, **owned by group bandit6** and **33 bytes in size**.

See the password for Level L by::

   bandit L@bandit:~/inhere$ cat /var/lib/dpkg/info/bandit7.password

Now exit from the machine.


Level 7
-------
Entering the Level 7 machine using the password from previous level same as before::

   ssh bandit7@bandit.labs.overthewire.org -p 2220

We can find the password in a file named **data.txt** next to the word **millionth**. Let's list all home directory file::

    bandit7@bandit:~$ ls
    data.txt
    bandit7@bandit:~$ 

We can see the `data.txt` file in the home directory. Now, only if we had a tool that can search all the contents of a file and print the result. Lucky us! We have a tool named `grep`_ that does exactly does as pre `Wikipedia <https://en.wikipedia.org/wiki/Grep>`_. If we see the man page of the grep, in the synopsis we can see that the grep is general used like this::

    grep [OPTIONS] PATTERN [FILE...]

So we need a pattern and one file. The word `millionth` can be our pattern and the file is obviously `data.txt`. Let's try that shall we?::

    bandit7@bandit:~$ grep millionth data.txt

The output of the command would show the `millionth` and the password side by side separated by tab. Let's exit from here so that we can continue to the next level.
    

Level 8
-------
As usual, entering the Level 8 with password previous level::

   ssh bandit8@bandit.labs.overthewire.org -p 2220

The password is in the in the file **data.txt** and is **the only line of text that occurs only once**. Just like the `Level 8`_ we can see the `data.txt` is in home directory. Now we need to sort all the files and find all the unique values with a count of how many time they have been repeated. Our password will have a count of 1. We need to use `sort`_ and `uniq`_ commands to accomplish our task.::

    bandit8@bandit:~$ cat data.txt | sort | uniq -c

First we will `cat`_ the `data.txt` file and we will `pipe <https://www.tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-4.html>`_ the output to the `sort`_ command which will sort the output then we will pass the sorted output to `uniq`_ command with `-c` flag that will show the count of the entry before the line.

Now exit from the machine to go to the next level.


Level 9
-------
Let's ssh Bandit server with password form level 8::

   ssh bandit9@bandit.labs.overthewire.org -p 2220

The password is in the file **data.txt** in one of the few **human-readable strings**, **beginning with several ‘=’ characters**. We can see the **data.txt** file in the home directory. Let's `cat`_ file::

	bandit9@bandit:~$ cat data.txt

Wow that is a lot of unrecognized junk! Let's do a quick check what type of file it is::

	bandit9@bandit:~$ file data.txt 
	data.txt: data
	bandit9@bandit:~$ 

We see the junks because this is a data file. I haven't worked with data file or binary a lot but I know about `xxd`_ command which creates a hex dump of a given file. So let's try that and try to `grep`_ **===** as we know password begins with several `=`::

    bandit9@bandit:~$ xxd data.txt | grep "==="
    00000460: 30b0 323d 3d3d 3d3d 3d3d 3d3d 3d20 7468  0.2========== th
    000014a0: 67a8 fcf3 4d26 54dc fbc0 f7c3 be3d 3d3d  g...M&T......===
    000014b0: 3d3d 3d3d 3d3d 3d20 7061 7373 776f 7264  ======= password
    00001b40: c4cd 3d3d 3d3d 3d3d 3d3d 3d3d 2069 7361  ..========== isa
    00003f40: 3d3d 3d3d 3d3d 3d3d 2074 7275 4b4c 646a  ======== truKLdj
    bandit9@bandit:~$ 

We can see the partial strings but not the complete one. At this point I don't know any tool that can improve the result so I searched for `xxd binary file and grep string <https://duckduckgo.com/?q=xxd+binary+file+and+grep+string>`_ and went to the `Stack Overflow answer <https://stackoverflow.com/a/17168847/5350059>`_ from the `Instant Answer panel <https://duck.co/ia>`_ in the side bar. After going through a few answer after I found this `answer <https://stackoverflow.com/a/6320787/5350059>`_ about a command named `strings`_ and tried that::

    bandit9@bandit:~$ strings -ao data.txt | grep "==="

Yes! We got the password this time. Now that We have the password, let's get to know more about the `strings`_ command. If we go to `explainshell.com`_ and paste the `strings -ao data.txt <https://explainshell.com/explain?cmd=strings+-ao+data.txt>`_ command. We see that the `strings`_ command print the strings of all printable characters in files. The `-a` flag scans the whole file and the `-o` flag works like `-t`. If we check the man page of `strings`_ command we see that the `-t` flag prints the offset within the file before each string. Now that we understand the command and have our password, let's exit from the machine.


Level 10
--------
Level 10 machine can be accessed with the password from previous level::

   ssh bandit10@bandit.labs.overthewire.org -p 2220

The password as stored in a file **data.txt** as usual, but it contains **base64 encoded data**. The `data.txt` file is in the home directory same as previous levels. We know from the hint that the content of the file is base64 encoded. In Linux we already have a command named `base64`_. So how does it work? Let's use the `--help` flag that is available in almost all the Linux commands. If we use `base64 --help` it would give use all the functions of the `base64`_ command but the notable one is the `-d` flag that is said to be used to **decode data**. So let's decode it.::

    bandit10@bandit:~$ base64 -d data.txt

We can to see the password for Level 11. Now we will exit from the machine go continue.

Level 11
--------
As usual enter Level 11 with password from Level 10::

    ssh bandit11@bandit.labs.overthewire.org -p 2220

The key to unlock Level 12 is in **data.txt** and **all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions**. This technique is a very common letter substitution cipher called `ROT13 <https://en.wikipedia.org/wiki/ROT13>`_. The `data.txt` file is already in the home directory so all we need to do is rotate letters by 13 positions. The `tr`_ command can help us do that. The man page says it takes a set of characters and changes it into another set. So the lowercase letter **a** will be replaced by the letter that is after 13 positions after **a** that is **n**. Like that **b** would be **o**. But the cool thing about the `tr`_ command is that we can also specify range of characters like `[a-z]` `[n-m]`. Let's try it out::

    bandit11@bandit:~$ cat data.txt | tr '[a-zA-Z]' '[n-mN-M]'
    tr: range-endpoints of 'n-m' are in reverse collating sequence order
    bandit11@bandit:~$ 

This doesn't seem to work! That is because the `tr`_ command goes through the range in ascending order and when it sees `m` after `n` it can't process it. To know more read `link1 <https://stackoverflow.com/a/8425152/5350059>`_ and `link2 <https://aweirdimagination.net/2015/03/01/reverse-sequence-for-tr>`_.

To see the password for Level 12::

   bandit11@bandit:~$ cat data.txt | tr '[a-zA-Z]' '[n-za-mN-ZA-M]

Which works because it breaks the range into `n-z` and the starts from `a-m`. Now that we have our password, exit from the machine.

Level 12
--------
SSH into Level 12 machine::

   ssh bandit12@bandit.labs.overthewire.org -p 2220

Use the password from Level 11 when asked for. The password for next level is in the **data.txt** and **a hexdump of a file that has been repeatedly compressed**. After reading the instructions, we get to learn that it would be useful to create a directory but as home directory is write protected we are suggested in the instruction to make it in the `/tmp` directory. Let's navigate to the `/tmp` directory and make a directory::

    bandit12@bandit:~$ cd /tmp/
    bandit12@bandit:/tmp$ mkdir jonedoe12
    bandit12@bandit:/tmp$ 

Now let's get into newly created `jonedoe12` directory and copy the `data.txt` file from home directory::

    bandit12@bandit:/tmp$ cd jonedoe12
    bandit12@bandit:/tmp/jonedoe12$ cp ~/data.txt .
    bandit12@bandit:/tmp/jonedoe12$ 

At this point I tried using `xxd`_ command to see the hexdump of the file but get nothing. As the clue say it is a **hexdump** of a **compressed** file so I tried to figure out what type of compression was using in the file using `xxd`_ in the hexdump file. By going through the man page of he `xxd`_ command we see that it has a `-r` or `-revert` flag that reverts the hexdump to binary which would be helpful::

    bandit12@bandit:/tmp/jonedoe12$ xxd -r data.txt

We see a lot of garbage as binary. We need to save the output to a file to process it further.::

    bandit12@bandit:/tmp/jonedoe12$ xxd -r data.txt >> data.bin

The `bin` extension is for binary. Now we can check the file type by using the `file`_ command:: 

    bandit12@bandit:/tmp/jonedoe12$ file data.bin
    data.bin: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix

We can see a lot of information among which the part `gzip compressed data` is important as it suggests that it is gzip compressed file. If we type `man gzip` we can see that `gzip`_ file exists. Let's keep reading! The `-d` flag seems to decompress gzip file, so we can try that::

    bandit12@bandit:/tmp/jonedoe12$ gzip -d data.bin
    gzip: data.bin: unknown suffix -- ignored
    bandit12@bandit:/tmp/jonedoe12$ 

A quick search in the web with the error message `gzip: unknown suffix -- ignored <https://superuser.com/a/544175/655587>`_ reviled that `gzip`_ only works on `.gz` file extension. We can run the same command after copying the file with `cp`_ and renaming it to `data.gz`::

    bandit12@bandit:/tmp/jonedoe12$ cp data.bin data.gz
    bandit12@bandit:/tmp/jonedoe12$ gzip -d data.gz
    bandit12@bandit:/tmp/jonedoe12$ 

Let's list all the files in the current directory::

    bandit12@bandit:/tmp/jonedoe12$ ls
    data  data.bin  data.txt
    bandit12@bandit:/tmp/jonedoe12$ 

So the `data.gz` file is no more and we have a new `data` file. If we check the file type of the `data` file with `file`_ command we see::

    bandit12@bandit:/tmp/jonedoe12$ file data
    data: bzip2 compressed data, block size = 900k
    bandit12@bandit:/tmp/jonedoe12$ 

Again a compressed file but this time a `bzip2 compressed data`. The man page for `bzip2` reviles a `-d` flag that can decompress the file. For safe keeping we will make a copy of the file first just like last step and then run the decompression::

    bandit12@bandit:/tmp/jonedoe12$ cp data data.bzip2
    bandit12@bandit:/tmp/jonedoe12$ bzip2 -d data.bzip2
    bzip2: Can't guess original name for data.bzip2 -- using data.bzip2.out
    bandit12@bandit:/tmp/jonedoe12$ 

We see that `bzip2`_ decompressed the file into `data.bzip2.out`. Now we will check the file type again::

    bandit12@bandit:/tmp/jonedoe12$ file data.bzip2.out
    data.bzip2.out: gzip compressed data, was "data4.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
    bandit12@bandit:/tmp/jonedoe12$ 

This time it is a `gzip compressed data` again. From previous step we know that we can decompress file with the `-d` flag. We will list the existing files, make a copy of the original file, decompress it, the list the files again to find the new decompressed file and finally run the `file`_ command in the new file to see the type of the file.::

    bandit12@bandit:/tmp/jonedoe12$ ls
    data  data.bin  data.bzip2.out  data.txt
    bandit12@bandit:/tmp/jonedoe12$ cp data.bzip2.out data.out.gz
    bandit12@bandit:/tmp/jonedoe12$ gzip -d data.bzip2.out.gz
    bandit12@bandit:/tmp/jonedoe12$ ls
    data  data.bin  data.bzip2.out  data.out  data.txt
    bandit12@bandit:/tmp/jonedoe12$ file data.out
    data.out: POSIX tar archive (GNU)
    bandit12@bandit:/tmp/jonedoe12$ 

This is a `POSIX tar archive (GNU)`. Ugh! This is getting tiresome layered compression. But patients is the key to success. We need to keep going. The man page for `tar`_ say that to decompress a tar file we need to use the `-x` flag. We will follow the same steps as previous, list current files, copy the original file, decompress it, then list the files again and see file type by running `find`_ command in the new file::

    bandit12@bandit:/tmp/jonedoe12$ ls
    data  data.bin  data.bzip2.out  data.out  data.txt
    bandit12@bandit:/tmp/jonedoe12$ cp data.out data.tar
    bandit12@bandit:/tmp/jonedoe12$ tar x data.tar
    tar: Refusing to read archive contents from terminal (missing -f option?)
    tar: Error is not recoverable: exiting now

Let's use the `-f` flag for archive file and the `-v` flag for increased verbosity and continue with our procedure::

    bandit12@bandit:/tmp/jonedoe12$ tar xfv data.tar 
    data5.bin
    bandit12@bandit:/tmp/jonedoe12$ file data5.bin 
    data5.bin: POSIX tar archive (GNU)

We get a `POSIX tar archive (GNU)` (I mean again!?). Same procedure for this one as well::

     bandit12@bandit:/tmp/jonedoe12$ ls
     data  data5.bin  data.bin  data.bzip2.out  data.out  data.tar  data.txt
     bandit12@bandit:/tmp/jonedoe12$ cp data5.bin data5.tar
     bandit12@bandit:/tmp/jonedoe12$ tar xfv data5.tar 
     data6.bin
     bandit12@bandit:/tmp/jonedoe12$ ls
     data  data5.bin  data5.tar  data6.bin  data.bin  data.bzip2.out  data.out  data.tar  data.txt
     bandit12@bandit:/tmp/jonedoe12$ file data6.bin 
     data6.bin: bzip2 compressed data, block size = 900k
     bandit12@bandit:/tmp/jonedoe12$ 

Now we will change the file extension and decompress it again::

    bandit12@bandit:/tmp/jonedoe12$ cp data6.bin data6.bzip2
    bandit12@bandit:/tmp/jonedoe12$ bzip2 -d data6.bzip2
    bzip2: Can't guess original name for data6.bzip2 -- using data6.bzip2.out
    bandit12@bandit:/tmp/jonedoe12$ 
    bandit12@bandit:/tmp/jonedoe12$ file data6.bzip2.out
    data6.bzip2.out: POSIX tar archive (GNU)
    bandit12@bandit:/tmp/jonedoe12$ 
    
Decompressing the tar file::

    bandit12@bandit:/tmp/jonedoe12$ tar xvf data6.bzip2.out.tar
    data8.bin
    bandit12@bandit:/tmp/jonedoe12$ file data8.bin 
    data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
    bandit12@bandit:/tmp/jonedoe12$

Decompressing the gzip file::

    bandit12@bandit:/tmp/jonedoe12$ cp data8.bin data8.gz
    bandit12@bandit:/tmp/jonedoe12$ gzip -d data8.gz 
    bandit12@bandit:/tmp/jonedoe12$ ls
    data  data5.bin  data5.tar  data6.bin  data6.bzip2.out  data6.bzip2.out.tar  data8  data8.bin  data.bin  data.bzip2.out  data.out  data.tar  data.txt
    bandit12@bandit:/tmp/jonedoe12$ file data8
    data8: ASCII text
    bandit12@bandit:/tmp/jonedoe12$

Finally we have an ASCII text!!! I am guessing the password is in this file. Let's see by::

    bandit12@bandit:/tmp/jonedoe12$ cat data8

Now exit from the machine to continue.



.. Level L
.. --------
.. Entering the Level L machine using the password from previous level::

..    ssh bandit L@bandit.labs.overthewire.org -p 2220

.. We can to see the password for Level L by::

..    bandit L@bandit:~/inhere$ cat F

.. Now exit from the machine.

.. macro: d

Source
------
- `Bandit: OverTheWire <https://overthewire.org/wargames/bandit/>`_

.. _ls: https://linux.die.net/man/1/ls
.. _cat: https://linux.die.net/man/1/cat
.. _exit: https://linux.die.net/man/3/exit
.. _cd: https://linux.die.net/man/1/cd
.. _file: https://linux.die.net/man/1/file
.. _find: https://linux.die.net/man/1/find
.. _grep: https://linux.die.net/man/1/grep
.. _sort: https://linux.die.net/man/1/sort
.. _uniq: https://linux.die.net/man/1/uniq
.. _xxd: https://linux.die.net/man/1/xxd
.. _strings: https://linux.die.net/man/1/strings
.. _base64: https://linux.die.net/man/1/base64
.. _tr: https://linux.die.net/man/1/tr
.. _gzip: https://linux.die.net/man/1/gzip
.. _cp: https://linux.die.net/man/1/cp
.. _bzip2: https://linux.die.net/man/1/bzip2
.. _tar: https://linux.die.net/man/1/tar
.. _explainshell.com: https://explainshell.com
