Bandit Walkthrough
==================
`< Blog <../blog.html>`_

Walkthrough of Bandit, a wargame by OverTheWire

Created on: 2020-01-09

.. role:: kbd

.. warning:: I know in the server banner is says 'DONT POST SPOILERS! This includes writeups of your solution on your blog or website!'. I fully respect that thus this is my duty to warn the reader not to use this to cheat in the game. This is just a personal note in an attempt to getting started with CTF writeup. I choose Bandit because it is easy and CTF/Techinal writeups are tough enough. I have been using Linux for sometime now and I can assure you that copy-pasting commands without understanding to cross a level or fix a problem don't make you a expert, it makes you a unprepared imposter and good mouse user. So DO NOT USE this to play the game! Use it as a getting started guide to write CTF writeup.

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

The game is divided into levels. Current level has the password for the next level. So, if we go to the `Bandit Level 0 → Level 1 <https://overthewire.org/wargames/bandit/bandit1.html>`_ page we will see the goal if Level 0. If we successfully achieve that goal we will be able to go to Level 1.

Level 0
-------
To start we need to type in our terminal::

    root@bandit:~# ssh bandit0@bandit.labs.overthewire.org -p 2220

It will ask our permission to add the host to the list of known hosts. Type `yes`. Then it will ask for the password. The password for this level is given and it is *bandit0*. Typing that will allow us to enter the game which is a Linux machine with rather long `motd <https://en.wikipedia.org/wiki/Motd_(Unix)>`_. 

The `goal set for level 0 <https://overthewire.org/wargames/bandit/bandit1.html>`_ is to find file called **readme** located in the home directory. After login with SSH, generally the user lands on the home directory. So let's see if we can find the file with `ls`_::

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

    root@bandit:~# ssh bandit1@bandit.labs.overthewire.org -p 2220

This will ask for password and use the string from previous level. If we see the `instructions for level 1 <https://overthewire.org/wargames/bandit/bandit2.html>`_, to go to next level we need to get the content of a file called **-** located in the home directory. If we try `cat`_-ing the file as before is hangs::

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

    root@bandit:~# ssh bandit2@bandit.labs.overthewire.org -p 2220

Use the password from previous level as before. The password for the next level is in a file called **spaces in this filename** as it says in the `level 2 web page <https://overthewire.org/wargames/bandit/bandit3.html>`_.

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

    root@bandit:~# ssh bandit3@bandit.labs.overthewire.org -p 2220

Use the password from previous level as before. We get the `instructions from level 3 <https://overthewire.org/wargames/bandit/bandit4.html>`_ that the password for the next level is in a **hidden** file in the **inhere** directory.

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

    root@bandit:~# ssh bandit4@bandit.labs.overthewire.org -p 2220

The password is in is stored in the **only human-readable** file in the **inhere** directory as we can see in `level 4 instructions page <https://overthewire.org/wargames/bandit/bandit5.html>`_.

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

    root@bandit:~# ssh bandit5@bandit.labs.overthewire.org -p 2220

Like before the password in in a directory named **inhere** which is **human-readable**, **1033 bytes in size** and **not executable**. The details of the level is in the `level 5's page <https://overthewire.org/wargames/bandit/bandit6.html>`_ If we see the contents of the file::

    bandit5@bandit:~$ ls inhere/
    maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
    maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
    bandit5@bandit:~$ 

That is a lot of directory! If we want to go through all those directory to find our specific file it would take a lot of time. We can use the `find`_ command to assist us in our task::

    bandit5@bandit:~$ find inhere/ -type f -size 1033c ! -executable
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

   root@bandit:~# ssh bandit6@bandit.labs.overthewire.org -p 2220


The `goal of level 6 <https://overthewire.org/wargames/bandit/bandit7.html>`_ is to get the password which is saved **somewhere on the server** and is **owned by user bandit7**, **owned by group bandit6** and **33 bytes in size**. Lets see if we have any file or directory in the home directory::

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

   root@bandit:~# ssh bandit7@bandit.labs.overthewire.org -p 2220

We can find the password in a file named **data.txt** next to the word **millionth** as per the `level 7 goal instructions <https://overthewire.org/wargames/bandit/bandit8.html>`_ Let's list all home directory file::

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

   root@bandit:~# ssh bandit8@bandit.labs.overthewire.org -p 2220

The password is in the in the file **data.txt** and is **the only line of text that occurs only once**. More details in the `level 8 page <https://overthewire.org/wargames/bandit/bandit9.html>`_ Just like the `Level 8`_ we can see the `data.txt` is in home directory. Now we need to sort all the files and find all the unique values with a count of how many time they have been repeated. Our password will have a count of 1. We need to use `sort`_ and `uniq`_ commands to accomplish our task.::

    bandit8@bandit:~$ cat data.txt | sort | uniq -c

First we will `cat`_ the `data.txt` file and we will `pipe <https://www.tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-4.html>`_ the output to the `sort`_ command which will sort the output then we will pass the sorted output to `uniq`_ command with `-c` flag that will show the count of the entry before the line.

Now exit from the machine to go to the next level.


Level 9
-------
Let's `ssh`_ to Bandit server with password form level 8::

   root@bandit:~# ssh bandit9@bandit.labs.overthewire.org -p 2220

As the `level 9 instructions <https://overthewire.org/wargames/bandit/bandit10.html>`_ says the password is in the file **data.txt** in one of the few **human-readable strings**, **beginning with several ‘=’ characters**. We can see the **data.txt** file in the home directory. Let's `cat`_ file::

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

   root@bandit:~# ssh bandit10@bandit.labs.overthewire.org -p 2220

Let's check out the instructions of `level 10 page <https://overthewire.org/wargames/bandit/bandit11.html>`_. The password as stored in a file **data.txt** as usual, but it contains **base64 encoded data**. The `data.txt` file is in the home directory same as previous levels. We know from the hint that the content of the file is base64 encoded. In Linux we already have a command named `base64`_. So how does it work? Let's use the `--help` flag that is available in almost all the Linux commands. If we use `base64 --help` it would give use all the functions of the `base64`_ command but the notable one is the `-d` flag that is said to be used to **decode data**. So let's decode it.::

    bandit10@bandit:~$ base64 -d data.txt

We can to see the password for Level 11. Now we will exit from the machine go continue.

Level 11
--------
As usual enter Level 11 with password from Level 10::

    root@bandit:~# ssh bandit11@bandit.labs.overthewire.org -p 2220

The key to unlock Level 12 is in **data.txt** and **all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions** as we see in the `level 11 instructions page <https://overthewire.org/wargames/bandit/bandit12.html>`_ This technique is a very common letter substitution cipher called `ROT13 <https://en.wikipedia.org/wiki/ROT13>`_. The `data.txt` file is already in the home directory so all we need to do is rotate letters by 13 positions. The `tr`_ command can help us do that. The man page says it takes a set of characters and changes it into another set. So the lowercase letter **a** will be replaced by the letter that is after 13 positions after **a** that is **n**. Like that **b** would be **o**. But the cool thing about the `tr`_ command is that we can also specify range of characters like `[a-z]` `[n-m]`. Let's try it out::

    bandit11@bandit:~$ cat data.txt | tr '[a-zA-Z]' '[n-mN-M]'
    tr: range-endpoints of 'n-m' are in reverse collating sequence order
    bandit11@bandit:~$ 

This doesn't seem to work! That is because the `tr`_ command goes through the range in ascending order and when it sees `m` after `n` it can't process it. To know more read `link1 <https://stackoverflow.com/a/8425152/5350059>`_ and `link2 <https://aweirdimagination.net/2015/03/01/reverse-sequence-for-tr>`_.

To see the password for Level 12::

   bandit11@bandit:~$ cat data.txt | tr '[a-zA-Z]' '[n-za-mN-ZA-M]

Which works because it breaks the range into `n-z` and the starts from `a-m`. Now that we have our password, exit from the machine.

Level 12
--------
We can began by doing `ssh`_ into Level 12 machine::

   root@bandit:~# ssh bandit12@bandit.labs.overthewire.org -p 2220

Use the password from `Level 11`_ when asked for. The password for next level is in the **data.txt** and **a hexdump of a file that has been repeatedly compressed**. After reading the `level 12 instructions <https://overthewire.org/wargames/bandit/bandit13.html>`_, we get to learn that it would be useful to create a directory but as home directory is write protected we are suggested in the instruction to make it in the `/tmp` directory. Let's navigate to the `/tmp` directory and make a directory::

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

Before we exit, it is considered good practice to clean up the file or directories we created to erase our tress of intrusion. We can do a lot of things to "clean up" our intrusion but for starters let's remove the files and directories we created::

	bandit12@bandit:/tmp/jonedoe12$ cd ..
	bandit12@bandit:/tmp$ rm -rf jonedoe12

Now exit from the machine to continue.

Level 13
--------
Let's enter Level 13 machine and the password is one we obtained in the last level::

    root@bandit:~# ssh bandit13@bandit.labs.overthewire.org -p 2220

The password for next level is in the file **/etc/bandit_pass/bandit14** and it can **only be read by user bandit14**. The problem is we will get the password for bandit14 in this level so how do we get it? The `clue of level 13 <https://overthewire.org/wargames/bandit/bandit14.html>`_ also says that we have private SSH key. If we list the files in our how directory we can see the private SSH key file::

    bandit13@bandit:~$ ls
    sshkey.private
    bandit13@bandit:~$ 

Let's see the man page of the `ssh`_ command to see how can we use it. The `-i` flag allows it to use private key and we know from the instructions that user is `bandit14` and `localhost` can be used as a host name::

    bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost
    Could not create directory '/home/bandit13/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? 

We type **yes** and we should be logged in as `bandit14`. Now we can see the file in `/etc/bandit_pass/bandit14`::

    bandit14@bandit:~$ cat /etc/bandit_pass/bandit14

Now exit from the machine.


Level 14
--------
We can get into this level by 3 ways:

- We can continue our previous session where we `ssh`_-ed to become `bandit14` because it is in the same machine as Level 13.

- Use the password we got from the previous level and use it::

   root@bandit:~# ssh bandit14@bandit.labs.overthewire.org -p 2220

- Or pulling the SSH private key to our local machine with `sftp`_ and using it to `ssh`_::

    root@bandit:~# sftp -P 2220 bandit13@bandit.labs.overthewire.org
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit13@bandit.labs.overthewire.org's password: 

If we put the password for `bandit13` here and we should see::

    root@bandit:~# bandit13@bandit.labs.overthewire.org's password: 
    Connected to bandit.labs.overthewire.org.
    sftp> 

`sftp`_ has a command `get` to that can be used to get a file from remote machine to local machine. So let's get the SSH private key with `get` and exit from `sftp`_::

    sftp> get sshkey.private 
    Fetching /home/bandit13/sshkey.private to sshkey.private
    /home/bandit13/sshkey.private                                                                                                         100% 1679     4.8KB/s   00:00    
    sftp> exit
    root@bandit:~#

The last step is to use the SSH private key to log in to Level 14::

    root@bandit:~# ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    Permissions 0640 for 'sshkey.private' are too open.
    It is required that your private key files are NOT accessible by others.
    This private key will be ignored.
    Load key "sshkey.private": bad permissions
    bandit14@bandit.labs.overthewire.org's password: 

As we can see we get an permission error that is because it needs to be read-writable by the current user aka 600 permission::

    root@bandit:~# chmod 600 sshkey.private

Now we can ssh::

    root@bandit:~# ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

The password for next level can be obtained if we submit the **password of this level** to port **30000 on localhost** as we see in the `level 14 goal page <https://overthewire.org/wargames/bandit/bandit15.html>`_. We can use the `nc`_ tool to connect to a port. After reading the man page we see that we can connect to a specific port like `30000` of a specific host like `localhost` like this::

    bandit14@bandit:~$ nc localhost 30000

Our courser should be seen stuck in the left most side which is actually waiting for our input. If we type or paste the password of this level we should get a **Correct!** message followed by a password string. Now exit from the machine to continue.

.. note:: try to do it with `curl` or maybe `wget`?


Level 15
--------
As always we will start by entering the machine by using the password from previous level::

    root@bandit:~# ssh bandit15@bandit.labs.overthewire.org -p 2220

The password for the next level will be `echo`_-ed back to us just like before if we submit the **password of this level** to port **30001 on localhost** which is using **SSL encryption** as per `level 15 instructions <https://overthewire.org/wargames/bandit/bandit16.html>`_. Can we use `nc`_ to do that? Unfortunately `nc`_ doesn't support ssl but if we check the instructions we see emphasized paragraph named `Helpful note` there is discussed what should we do if we get  “HEARTBEATING” and “Read R BLOCK” and suggests us to use `-ign_eof`. A quick search in the web reveales that it is a flag for `openssl`_. The man page of `openssl`_ gives us the `s_client`_ flag which as you can see has it's own man page. On the man page of `s_client`_ the first option is `-connect` that takes a host and port. Let's try that::

    bandit15@bandit:~$ openssl s_client -connect localhost:30001
    CONNECTED(00000003)
    ... a lot of output about ssl ...
    ---

Here the courser is stuck, waiting for our input. If we give it the password of this level it would return **Correct!** followed by the `password string` then a line space and finally we should see a text **closed**. Now exit from the machine.


Level 16
--------
Let's begin by `ssh`_-ing into the Level 16 machine to search for next levels password::

    root@bandit:~# ssh bandit16@bandit.labs.overthewire.org -p 2220



After reading the `level 16 instructions <https://overthewire.org/wargames/bandit/bandit17.html>`_ we can see that the password for next level if we enter **this levels password** to a **localhost port in between 31000 and 32000** and it **usages SSL** . 31000 to 32000 is 1000 port and scanning it would require a lot of time. Lucky for us we have `nmap`_ to help us. If we load the man page for `nmap`_ we would see it is huge so we can use `grep`_ to help us with this. We need to see what the man page tells us about `range`::

    man grep | grep range

We would see that `-p` flag can help us with that. Let see some examples on how to use `nmap`_, we will use the `-A` flag that prints number of lines after the matching pattern::

    man nmap | grep EXAMPLES -A 3

Now that we have seen some examples we get a general format to run `nmap`_ which is `nmap -p port-range host` and for our case it would be::

    bandit16@bandit:~$ nmap -p 31000-32000 localhost

    Starting Nmap 7.40 ( https://nmap.org ) at 2020-01-16 09:26 CET
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00023s latency).
    Not shown: 999 closed ports
    PORT      STATE SERVICE
    31518/tcp open  unknown
    31790/tcp open  unknown

    Nmap done: 1 IP address (1 host up) scanned in 0.09 seconds

We see two open ports. Last time we used `openssl`_, this time we will use a improved version of `nc`_ which is `ncat`_ which has a `-ssl` flag. Let's try `ncat`_ for first port `31518`::

    bandit16@bandit:~$ ncat --ssl localhost 31518

If we paste the password it `echo`_'s back the same thing which is not what we want. Let's try the next port, `31790`::

    bandit16@bandit:~$ ncat --ssl localhost 31790

If we paste the password this time it `echo`_'s **Correct!** followed by **-----BEGIN RSA PRIVATE KEY-----** and a lot of string and then ends with **-----END RSA PRIVATE KEY-----**. This seems like a private key. It could be the SSH private key for next level. Let's get out of this by pressing Ctrl + c. Now we can copy the key and exit from the machine. Now open a file named `bandit17.key`, paste the key and save that::

    root@bandit:~# vim bandit17.key

We have to change the permission of the file to access the next level::

    root@bandit:~# chmod 600 bandit17.key


Level 17
--------
We will us the SSH private key from the previous level to get into Level 17::

    root@bandit:~# ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220

There is two file in the home directory **passwords.old** and **passwords.new**. The password for next level is in **passwords.new** and it is the only line that is different from **passwords.old** according to the `instructions of level 17 <https://overthewire.org/wargames/bandit/bandit18.html>`_. We have a handy-dandy tool named `diff`_ that `compare files line by line`. Let's use it::

    bandit17@bandit:~$ diff passwords.new passwords.old 

We should see the difference between two file and the first string would be the password for next level.

We can also get the password for this level::

    bandit17@bandit:~$ cat /etc/bandit_pass/bandit17

Now exit from the machine.


Level 18
--------
We will use the password from the previous level to `ssh`_ into this level::

    root@bandit:~# ssh bandit18@bandit.labs.overthewire.org -p 2220

But as soon as we enter the password we see the long banner which says::

    Byebye !
    Connection to bandit.labs.overthewire.org closed.

And get are back to our local machine. If we see the `instructions on level 18 <https://overthewire.org/wargames/bandit/bandit19.html>`_ we would see that the password in a **readme in the home directory** and our **.bashrc to log us out when we log in with SSH**. So we can SSH but can stay in the session. If we look closely in the `ssh`_ man page or the output of the `ssh --help` command we should see at the usage part, after all those flags and options we have a command option. Would it mean it would let us execute commands in the remote machine? Let's try to list the file in the remote machine with `ls`_ with `ssh`_'s command option::

    root@bandit:~# ssh bandit18@bandit.labs.overthewire.org -p 2220 ls
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit18@bandit.labs.overthewire.org's password: 
    readme
    root@bandit:~# 

If we enter the password for this level we see that we can see one `readme` file as output. This could be the file with password! So let's `cat`_ the file just like we listed the file::

    root@bandit:~# ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

This will reviled the password for next level. Time to exit the box or machine to move on to the next one.


Level 19
--------
Get inside the box with with `ssh` with last password form last level::

    root@bandit:~# ssh bandit19@bandit.labs.overthewire.org -p 2220

The `goal of level 19 <https://overthewire.org/wargames/bandit/bandit20.html>`_ is to is to obtain password for next level by using the **setuid binary in the home directory** form the usual place for password in **/etc/bandit_pass** directory. Let's see what we have in our home directory::

    bandit19@bandit:~$ ls
    bandit20-do
    bandit19@bandit:~$ file bandit20-do 
    bandit20-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=8e941f24b8c5cd0af67b22b724c57e1ab92a92a1, not stripped
    bandit19@bandit:~$

We see a we have one file named `bandit20-do` and our `file`_ command shows that it is a `setuid ELF 32-bit LSB executable` and ss the instruction also suggests let execute it without any argument::

    bandit19@bandit:~$ ./bandit20-do 
    Run a command as another user.
      Example: ./bandit20-do id
    bandit19@bandit:~$ 

Cool! So we can use this to run any command as another user for this case as `bandit20` user I guess. This would definitely be useful.

Now if we check out the `/etc/bandit_pass` directory we will see a lot's of file::

    bandit19@bandit:~$ ls /etc/bandit_pass/
    bandit0  bandit10  bandit12  bandit14  bandit16  bandit18  bandit2   bandit21  bandit23  bandit25  bandit27  bandit29  bandit30  bandit32  bandit4  bandit6  bandit8
    bandit1  bandit11  bandit13  bandit15  bandit17  bandit19  bandit20  bandit22  bandit24  bandit26  bandit28  bandit3   bandit31  bandit33  bandit5  bandit7  bandit9
    bandit19@bandit:~$ 

So the password for next level should be one file `bandit20`. Let's check out it's contents::

    bandit19@bandit:~$ cat /etc/bandit_pass/bandit20
    cat: /etc/bandit_pass/bandit20: Permission denied
    bandit19@bandit:~$ 

Alas! We, the user `bandit19` doesn't have access to this file but we have a tool that can solve this problem. Yes, it is the `bandit20-do` setuid **binary executable**. Let's use it to achieve our goal::

    bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20

Now that we have the password string, we should exit from the box.


Level 20
--------
Entering the Level 20 machine using the password from previous level::

   root@bandit:~# ssh bandit20@bandit.labs.overthewire.org -p 2220


If we go through the `instructions of level 20 <https://overthewire.org/wargames/bandit/bandit21.html>`_, we will see that here we have a **setuid binary in the home directory** that **connects to localhost** on a **port that we will specify**, in the next line it will **read the password of this level** and **if matches it will return the password for next level**. If we list home directory we should see a `suconnect` file which is `setuid ELF 32-bit LSB executable`::

    bandit20@bandit:~$ ls
    suconnect
    bandit20@bandit:~$ file suconnect 
    suconnect: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=74c0f6dc184e0412b6dc52e542782f43807268e1, not stripped
    bandit20@bandit:~$ 

If we execute it with out any argument like the previous level we see::

    bandit20@bandit:~$ ./suconnect 
    Usage: ./suconnect <portnumber>
    This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
    bandit20@bandit:~$ 

We have no port list or port range so we will use the `-p` flag of `nmap`_ to scan all port::

    bandit20@bandit:~$ nmap -p- localhost

    Starting Nmap 7.40 ( https://nmap.org ) at 2020-01-16 12:11 CET
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00017s latency).
    Not shown: 65525 closed ports
    PORT      STATE SERVICE
    22/tcp    open  ssh
    113/tcp   open  ident
    6013/tcp  open  x11
    30000/tcp open  ndmps
    30001/tcp open  pago-services1
    30002/tcp open  pago-services2
    30003/tcp open  amicon-fpsu-ra
    31518/tcp open  unknown
    31790/tcp open  unknown
    39063/tcp open  unknown

    Nmap done: 1 IP address (1 host up) scanned in 2.69 seconds
    bandit20@bandit:~$ 

We have a lots of open port but I would like to start from the bottom of the list because top of list has port like `22` `113` which runs well recognized services like `SSH` and `Identification Protocol`. So let's try with the last port `39063`::

    bandit20@bandit:~$ ./suconnect 39063
    Could not connect
    bandit20@bandit:~$ 

No luck! If we try port `31790` we get a place to give input but after taking input it just stays stuck. We see the same for `31518`. In port `30003` we see a ourput::

    bandit20@bandit:~$ ./suconnect 30003
    Read: I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secr
    ERROR: This doesn't match the current password!
    bandit20@bandit:~$ 

So maybe we have many ports in the machine that takes something like a password of current level and a secret and returns the password for next level. Let's keep digging. Port `30002` gives us something similar port `30003` and port `30001`, `30000` same as port `31790` and `31518`. I went on and tried all the ports even SSH at `22`. It all failed in some way or other. So I decided to read the instructions again which I did for couple of times but could not get anything. It was getting frustrating. Finally, I got my break when I read the **Note** that said "Try connecting to your **own** network daemon". Can we do that? So for this to work we need one more `ssh`_ connection. We can use the `-l` flag of `nc`_ to start a listener with `-p` flag to specify source port and `-v` flag for verbose mode in the first terminal::

    bandit20@bandit:~$ nc -lv -p 10101

From the second terminal we will connect to this port::

    bandit20@bandit:~$ ./suconnect 10101


We can see that the courser is waiting for input. Let's press Ctrl + c to exit. If we check our first terminal we should see that we have or shall we say had a connection::

    bandit20@bandit:~$ nc -lv -p 10101
    listening on [any] 10101 ...
    connect to [127.0.0.1] from localhost [127.0.0.1] 53372
    bandit20@bandit:~$ 

Now we can see the password of next level by sending the password of `bandit20` to a port from terminal 1::

    bandit20@bandit:~$ cat /etc/bandit_pass/bandit20 | nc -lv 127.0.0.1 -p 10101
    listening on [any] 10101 ...


It is waiting and waiting for us to connect. Now if we go to terminal 2 and connect to port `10101` with our setuid binary::

    bandit20@bandit:~$ ./suconnect 10101
    Read: password_strings_of_bandit20
    Password matches, sending next password
    bandit20@bandit:~$ 

In terminal 1 we should be able to see the password for next level.


Level 21
--------
Into the Level 21 machine we go, obviously with `ssh`_ and password from Level 20::

   root@bandit:~# ssh bandit21@bandit.labs.overthewire.org -p 2220

As the `web page of level 21 <https://overthewire.org/wargames/bandit/bandit22.html>`_ says, a program is running automatically at **regular intervals from cron** and we should take a **look in /etc/cron.d/**. To know more about cron we can take a look at the `cron - Wikipedia <https://en.wikipedia.org/wiki/Cron>`_ page. There we see that it comes from `crontab`. Now we have a command in Linux named `crontab`_ and the man page says the `-l` flag should show us the current `crontab`::

    bandit21@bandit:~$ crontab -l
    crontabs/bandit21/: fopen: Permission denied
    bandit21@bandit:~$ 

Well we don't have permission. So let's see what we find in the `/etc/cron.d/` directory::

    bandit21@bandit:/etc/cron.d$ ls
    atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
    bandit21@bandit:/etc/cron.d$ 

We are in Level 21 machine so maybe the `cronjob_bandit22` could have something of value. Let's see the contains of file with `cat`_::

    bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
    @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    bandit21@bandit:/etc/cron.d$ 

So we have two lines in `crontab`_. Basically it has two part, the first one is a event or time and the second one is a command. For the first line the event is **After rebooting** and the command is running the **bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null** and for second line the event is **At every minute.** run the **bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null**  command. The explanation and details can be found in the `crontab(5) <https://linux.die.net/man/5/crontab>`_ man page or we can cheat a bit by using `crontab guru`_ site. 

Now that we know that the `/usr/bin/cronjob_bandit22.sh` script is running `every minute`, time to take a closer look at it. First we will see the file permission and then the contents of the script::

    bandit21@bandit:/etc/cron.d$ ls -la /usr/bin/cronjob_bandit22.sh
    -rwxr-x--- 1 bandit22 bandit21 130 Oct 16  2018 /usr/bin/cronjob_bandit22.sh
    bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
    #!/bin/bash
    chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    bandit21@bandit:/etc/cron.d$ 


So from the permission we can see that we `bandit21` user can only read and execute the script but can't write to it. From the content of the script we can see that it changes the permission of a file in the `/tmp` directory with `chmod`_ to give read-write permission to the user and read permission to the group and everyone. Then `cat`_-s the password of `bandit22` user's password to the file. So we don't have access to the password file of `bandit22` user saved on `/etc/bandit_pass/bandit22` nor we can modify the script to give it to us but we sure do have read access to the file in `/tmp` directory. We can to see the password for Level 22 by::

   bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

Now exit from the machine.


Level 22
--------
Entering the Level 22 machine using the password from previous level::

   root@bandit:~# ssh bandit22@bandit.labs.overthewire.org -p 2220

The flag of this level is as same as the previous level where a program is running automatically at **regular intervals from cron** and we should take a **look in /etc/cron.d/** as per the `instructions of level 22 <https://overthewire.org/wargames/bandit/bandit23.html>`_. Just like before if we run `crontab -l` we get permission denied. We let's take a look at the ``/etc/cron.d/`` directory::

    bandit22@bandit:~$ ls /etc/cron.d/
    atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
    bandit22@bandit:~$ 

Just like before we will see the content of the `cronjob_bandit23` file::

    bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
    @reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    * * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    bandit22@bandit:/etc/cron.d$ 

It's same like `Level 22`_. Checking the file permission and contains of the script `/usr/bin/cronjob_bandit23.sh`::

    bandit22@bandit:/etc/cron.d$ ls -la /usr/bin/cronjob_bandit23.sh
    -rwxr-x--- 1 bandit23 bandit22 211 Oct 16  2018 /usr/bin/cronjob_bandit23.sh
    bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
    #!/bin/bash

    myname=$(whoami)
    mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

    echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

    cat /etc/bandit_pass/$myname > /tmp/$mytarget
    bandit22@bandit:/etc/cron.d$ 

This one has the same permission as previous level except for one little change people of group `bandit22` can execute it which can be very helpful to debug the script. The contents of the script may seem a bit hard at the first look but let's read it line by line:

- The 1st line is the `Shebang`_ that indicates that it is a `bash script`_ file.

- The 3rd line executes the `whoami` command and saves it value to the `myname` variable.

- The 4th line concats the string **"I am user "** and the variable **myname** then `echo`_-s the string to `md5sum`_ command via pipe. The `md5sum`_ calculates the `MD5 sum <https://en.wikipedia.org/wiki/Md5sum>`_ of the `echo`_-ed string and pass to `cut`_ command. The man page of `cut`_ says that the `-d` flag helps `cut`_ to divide a string by a given delimiter and `-f` flag selects a specified number. Finally the value is saved in the `mytarget` variable. 

- The 6th line just echos a string saying that "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget" which if the variables are replace with values of our current user, `bandit22`; would say: "Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3". 

- The 8th line `cat`_-s the contents of the `/etc/bandit_pass/$myname` aka the password of a user to the file in `/tmp` directory with the file name saved in `mytarget` variable. 

We can see all this in action if we execute the script in debug mode of `bash`_ with the `-x` flag. 

Now we can't write or modify the script. But if we can figure out the file name that will be saved in the `/tmp` directory we can get the password. We know the script will be executed as `bandit23` user so the `myname` variable will be `bandit23`. The easy way to do it is to take the existing script, copy to a place we have write access, change the permission bit with `chmod`_ and modify it to change to fit our need::

    bandit22@bandit:~$ mkdir -p /tmp/jonedoe22
    bandit22@bandit:~$ cd /tmp/jonedoe22
    bandit22@bandit:/tmp/jonedoe22$ cp /usr/bin/cronjob_bandit23.sh bandit23.sh
    bandit22@bandit:/tmp/jonedoe22$ chmod 777 bandit23.sh
    bandit22@bandit:/tmp/jonedoe22$ ls -la
    total 305928
    drwxr-sr-x 2 bandit22 root      4096 Jan 18 10:31 .
    drwxrws-wt 1 root     root 313204736 Jan 18 10:33 ..
    -rwxrwxrwx 1 bandit22 root       210 Jan 18 10:31 bandit23.sh
    bandit22@bandit:/tmp/jonedoe22$ 


For the sake of simplicity we have given read-write-execute permission to user-group-everyone. Now let's modify the `myname` variable to set the value to be `bandit23` and execute it::

	bandit22@bandit:/tmp/jonedoe22$ ./bandit23.sh

We should see the output of the `echo`_ command on line 6 and an additional error saying that the access to file in `/tmp` directory is denied. Now if we take the file path and `cat`_ it we should see the password for `Level 23`_. Let's do the clean up::

	bandit22@bandit:/tmp/jonedoe22$ cd ..
	bandit22@bandit:/tmp$ rm -r jonedoe22
	bandit22@bandit:/tmp$ 

Now let's exit from the machine.


Level 23
--------
Using the password from previous level, let's entering the Level 23 machine::

   root@bandit:~# ssh bandit23@bandit.labs.overthewire.org -p 2220

Just like `Level 22`_ the flag can obtained by exploiting a program running at **regular intervals from cron** via `cron` and we can check the files under **/etc/
cron.d/** directory to see how it is running.::

    bandit23@bandit:/etc$ cd /etc/cron.d/
    bandit23@bandit:/etc/cron.d$ ls 
    atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
    bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
    @reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
    * * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
    bandit23@bandit:/etc/cron.d$ 

We see the same things as before. Let's move on to check the file permission and contents of the script::

	bandit23@bandit:/etc/cron.d$ ls -la /usr/bin/cronjob_bandit24.sh
	-rwxr-x--- 1 bandit24 bandit23 253 Oct 16  2018 /usr/bin/cronjob_bandit24.sh
	bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
	#!/bin/bash

	myname=$(whoami)

	cd /var/spool/$myname
	echo "Executing and deleting all scripts in /var/spool/$myname:"
	for i in * .*;
	do
		if [ "$i" != "." -a "$i" != ".." ];
		then
		echo "Handling $i"
		timeout -s 9 60 ./$i
		rm -f ./$i
		fi
	done


	bandit23@bandit:/etc/cron.d$ 

So we have as we are in `bandit23` group we can read-execute the script. Let's read the file line-by-line to understand what is happening:

- The 1st line is the `Shebang`_ that indicates that it is a `bash script`_ file.

- The 3rd line executes the `whoami` command and saves it value to the `myname` variable.

- The 5th line changes directory with `cd`_ to `/var/spool/$myname`.

- The 6th line `echo`_-s the line "Executing and deleting all scripts in /var/spool/$myname:". That means we have some file in `/var/spool/$myname` which this scripts and the deletes them. If we resolve the `myname` variable to the user `bandit24` it would say "Executing and deleting all scripts in /var/spool/bandit24".

- The 7th line starts a `for`_ loop that goes through all the files and directories in the `/var/spool/$myname` directory.

- The 9th line has an `if`_ condition that check if the file is not **.** and **..** then let's the program proceed.

- The 11th line `echo`_-s the line "Handling $i"  which should "Handling some-script.sh" if we resolve the variable `i` with a valid script name.

- The 12th line usages a command `timeout`_ with `-s` flag. If we load the man page for `timeout`_ command we would see in the description that it would start a command and kill it if the command is running after a mentioned time. The `-s` flag is used for specifying a signal on timeout. If we compare that to our command we would see that we are running a script from the directory and after 60 seconds we are sending signal 9 with the `-s` flag to kill the script.

- The 13th line removes the script with `rm`_ command with `-f` flag that forces the process.

Now as we can see the script itself is very simple that just executes all the scripts in the `/var/spool/$myname` directory in the case of `bandit24` it would be `/var/spool/bandit24`. We don't have any command that can help use to get use the password for user `bandit24`. If we see first **Note** in the instructions page we would see that it say's we need to **create our own first shell-script** and may be we can drop the script in the directory? Let's check the file permission of the `/var/spool/bandit24` directory::

	bandit23@bandit:~$ ls -la /var/spool/bandit24
	ls: cannot open directory '/var/spool/bandit24': Permission denied
	bandit23@bandit:~$ 

So we don't have permission inside the `/var/spool/bandit24` directory but what permission does it have::

    bandit23@bandit:~$ ls -la /var/spool/
    total 1348
    drwxr-xr-x  5 root root        4096 Oct 16  2018 .
    drwxr-xr-x 11 root root        4096 Oct 16  2018 ..
    drwxrwx-wx  7 root bandit24 1359872 Jan 18 13:06 bandit24
    drwxr-xr-x  3 root root        4096 Oct 16  2018 cron
    lrwxrwxrwx  1 root root           7 Oct 16  2018 mail -> ../mail
    drwx------  2 root root        4096 Jan 14  2018 rsyslog
    bandit23@bandit:~$

We can see that `root` and `bandit24` user have read-write-execute permission but everyone has write-execute permission but just not the read permission. That's why we get permission denied when we tried to list all the file in `/var/spool/bandit24` directory. Now that we know that we have write access to the directory we can write our own script and put in on `/var/spool/bandit24` what will be execute by `bandit24` user via the script. This will also delete that script from the `/var/spool/bandit24` directory so we must keep a copy of the original shell. We can write a shell that will `cat`_ the password of `bandit24` user in our read-writable directory. First let's create a directory in `/tmp` directory::

	bandit23@bandit:/var/spool$ mkdir -p /tmp/jonedoe23
	bandit23@bandit:/var/spool$ cd /tmp/jonedoe23

Now we will write the script. We will reuse the script from `Level 21`_. The content is as follows::

	bandit23@bandit:/tmp/jonedoe23$ cat get-pass.sh 
	#!/bin/bash
	touch /tmp/jonedoe23/bandit24_pass 
	chmod 777 /tmp/jonedoe23/bandit24_pass
	cat /etc/bandit_pass/bandit24 > /tmp/jonedoe23/bandit24_pass
	bandit23@bandit:/tmp/jonedoe23$

We have a script name `get-pass.sh`. It creates a file named `bandit24_pass` in our read-writable directory `/tmp/jonedoe23/` changes the permission bit to `777` so that everyone has read-write-execute permission and `cat`_-s the password of `/bandit24` to the previously created file `bandit24_pass`. Now let's change the scripts file permission to be executable and copy it to `/var/spool/bandit24/`::

	bandit23@bandit:/tmp/jonedoe23$ chmod +x get-pass.sh 
	bandit23@bandit:/tmp/jonedoe23$ cp get-pass.sh /var/spool/bandit24/
	bandit23@bandit:/tmp/jonedoe23$

We can check current time with the `date`_ command. Once a new minute has started the script will be executed and we will have able to see the password with::

   bandit23@bandit:/tmp/jonedoe23$ cat bandit24_pass

Little bit of clean up to remove the files and directories created::

	bandit23@bandit:/tmp/jonedoe23$ cd ..
	bandit23@bandit:/tmp$ rm -r jonedoe23
	bandit23@bandit:/tmp$ 

Now exit from the machine.


Level 24
--------
The Level 24 machine is accessible with password from previous level::

   root@bandit:~# ssh bandit24@bandit.labs.overthewire.org -p 2220

The `goal of level 24 <https://overthewire.org/wargames/bandit/bandit25.html>`_ it to get the password for `Level 25`_ which can be will be provided to us if we connect to a daemon **listening on port 30002** which takes the **password for bandit24** and a **secret numeric 4-digit pincode**. Now as the instructions says there is no way to get the password **except by trying all of the 10000 combinations aka brute-forcing**. Doing this 10000 combination by hand would be a tiresome task. So we will write a script for this. But first check if we can connect to the daemon at port 30002 with `nc`_::

    bandit24@bandit:~$ nc localhost 30002
    I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
    Timeout. Exiting.

It was waiting for a input but it exited with a timeout. Now let's create a directory in `/tmp` and create our script named `bandit25-brute-force.sh` with the following contents::

    bandit24@bandit:/tmp/jonedoe24$ cat bandit25-brute-force.sh 
    #!/bin/bash

    BANDIT24_PASS=""

    for PIN in {0..9}{0..9}{0..9}{0..9}
    do
        echo "$BANDIT24_PASS $PIN"  
    done | nc localhost 30002

	
Now the script is very very simple. As usual the first line contains `Shebang`_ to indicate that is is a `bash script`_ . The password for `bandit24` user will be saved in the `BANDIT24_PASS` variable in 3rd line. I have intentionally left it blank so make sure to put the password. The 5th line starts a for loop that will iterate first digit from 0 to 9 and so for the second, third and forth digit and save it in a variable named `PIN`. Next we are `echo`_-ing the value of `BANDIT24_PASS` variable followed by a space, then followed by the value of `PIN` variable. The loop ends with the `done` syntax and everything gets piped it to the `nc`_ command.

The important thing to notice here is that this script it very rudimentary because it has no way of knowing that if we are successful thus it would keep trying after the goal is complete. So we need to keep a close eye when it is trying the different pin. Let's make it executable first and then execute it::

    bandit24@bandit:/tmp/jonedoe24$ chmod +x bandit25-brute-force.sh
    bandit24@bandit:/tmp/jonedoe24$ ./bandit25-brute-force.sh
    I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
    Wrong! Please enter the correct pincode. Try again.
    Wrong! Please enter the correct pincode. Try again.
    Wrong! Please enter the correct pincode. Try again.
    ... same error ...
    Wrong! Please enter the correct pincode. Try again.
    Wrong! Please enter the correct pincode. Try again.
    Correct!
    
The next line will give use the password to go to next level. We will do the basic clean up and will exit the machine::

    bandit24@bandit:/tmp/jonedoe24$ cd ..
    bandit24@bandit:/tmp$ rm -r jonedoe24
    bandit24@bandit:/tmp$ exit


Level 25
--------
Entering the Level 25 machine using the password from previous level::

   root@bandit:~# ssh bandit25@bandit.labs.overthewire.org -p 2220

The `level 25 instructions <https://overthewire.org/wargames/bandit/bandit26.html>`_ says that going to next level should be **fairly easy** but the **default shell for bandit26 is not /bin/bash**. We need to **find out what it is, how it works and how to break out of it.**

Alright then, let's see what we have in the home directory of `bandit25` user with `ls`_::

    bandit25@bandit:~$ ls
    bandit26.sshkey
    bandit25@bandit:~$ 

We have a SSH key for `bandit26`. Maybe that it what the `fairly easy` part was about. If we check the file type we will see it is a SSH private key::

    bandit25@bandit:~$ file bandit26.sshkey 
    bandit26.sshkey: PEM RSA private key
    bandit25@bandit:~$ 

Let's use it to `ssh`_ into `Level 26`_::

    bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost
    Could not create directory '/home/bandit25/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? yes
    Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    Linux bandit 4.18.12 x86_64 GNU/Linux
    
    --- rest of the motd ---

    Connection to localhost closed.

So we can `ssh`_ into the machine but get kicked out because the `default shell for bandit26 is not /bin/bash`. The default shell for all users are saved in the `/etc/passwd` file. Let's `grep`_ for `bandit26` user in the `/etc/passwd` file see it's shell::

    bandit25@bandit:~$ grep bandit26 /etc/passwd
    bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
    bandit25@bandit:~$ 

The last part with `/usr/bin/showtext` is the default shell for user `bandit26`. Generally, a shell is a binary executable file like `bash`. Let's check the file type of the shell::

    bandit25@bandit:~$ file /usr/bin/showtext
    /usr/bin/showtext: POSIX shell script, ASCII text executable
    bandit25@bandit:~$ 

We can see that for `showtext` shell is a `POSIX shell script, ASCII text executable`. That means we can see the contains of the file with `cat`_::

    bandit25@bandit:~$ cat /usr/bin/showtext
    #!/bin/sh

    export TERM=linux

    more ~/text.txt
    exit 0
    bandit25@bandit:~$ 

If we check the script it is obvious form the `Shebang`_ that it is a `sh script`_. The script `export` or `set`-'s the `TERM` environment variable to `linux` the shows us a text from the file saved in the home directory of user and named `text.txt`. Then it `exit`_-s with code 0. I don't see any way to move forward. How about we try to give it a different shell? ::

    bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost /bin/sh
    Could not create directory '/home/bandit25/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? yes
    Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    ls
    ^Cbandit25@bandit:~$ 


It just hangs there until `Ctrl` + `c` is pressed to exit. If we try the `-T` flag of `ssh`_ which `Disable pseudo-terminal allocation` gives the same result. For `-t` flag of the `ssh`_ command, which `Force pseudo-terminal allocation` we don't see the long `motd`_, just the `bandit` ascii art::

	bandit25@bandit:~$ ssh -t -i bandit26.sshkey bandit26@localhost /bin/sh
	Could not create directory '/home/bandit25/.ssh'.
	The authenticity of host 'localhost (127.0.0.1)' can't be established.
	ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
	Are you sure you want to continue connecting (yes/no)? yes
	Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
	This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

	  _                     _ _ _   ___   __  
	 | |                   | (_) | |__ \ / /  
	 | |__   __ _ _ __   __| |_| |_   ) / /_  
	 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
	 | |_) | (_| | | | | (_| | | |_ / /| (_) |
	 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
	Connection to localhost closed.
	bandit25@bandit:~$ 

So we are going back to analyzing our shell `showtext`. Let's see the contains of the script again::

	bandit25@bandit:~$ cat /usr/bin/showtext
	#!/bin/sh

	export TERM=linux

	more ~/text.txt
	exit 0
	bandit25@bandit:~$ 

We have 3 things here: `export`, `more`_ and `exit`_. We see that `export` has no man page::

	bandit25@bandit:~$ man export
	No manual entry for export
	bandit25@bandit:~$

But help is here to rescue::

	bandit25@bandit:~$ export --help
	export: export [-fn] [name[=value] ...] or export -p
	Set export attribute for shell variables.

	Marks each NAME for automatic export to the environment of subsequently
	executed commands.  If VALUE is supplied, assign VALUE before exporting.

	Options:
	  -f	refer to shell functions
	  -n	remove the export property from each NAME
	  -p	display a list of all exported variables and functions

	An argument of `--' disables further option processing.

	Exit Status:
	Returns success unless an invalid option is given or NAME is invalid.
	bandit25@bandit:~$ 

We see the `-f` flag that can refer to shell functions but I am not knowledgeable enough. Moving into `more`_. If we run `grep`_ on the man page of `more`_ for "command", we would see::

	bandit25@bandit:~$ man more | grep command
		Options are also taken from the environment variable MORE (make sure to precede them with a dash (-)) but command-line options will override those.
		Interactive commands for more are based on vi(1).  Some commands may be preceded by a decimal number, called k in the descriptions below.  In the  following
			  h or ?    Help; display a summary of these commands.  If you forget all other commands, remember this one.
			  !command or :!command
						Execute command in a subshell.
			  .         Repeat previous command.
		The more command respects the following environment variables, if they exist:
		VISUAL The editor the user prefers.  Invoked when command key v is pressed.
		The more command appeared in 3.0BSD.  This man page documents more version 5.19 (Berkeley 6/29/88), which is currently in use in the Linux community.  Docu‐
		The more command is part of the util-linux package and is available from Linux Kernel Archive ⟨ftp://ftp.kernel.org/pub/linux/utils/util-linux/⟩.
	bandit25@bandit:~$ 

We see that we have an option to give interactive commands based on `vi`_ and pressing `v` invokes the `vi`_. We let's try that. But wait how do we get into `more`_-'s interactive mode? The only time `more`_ enters an interactive mode when it has more text then the screen size. So first we need to re-size our screen to make it very small so that no more then 5 lines are seen at a time. Then `ssh`_ into the `bandit26` account::

	bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost

When we type `yes` after a bit of `motd` we should see something like `--More--(83%)`. It would mean we are in interactive mode. Now let's active the `vi`_ mode by pressing `v`. At least some success! Now how do we get the password for `bandit26` user? If we run `grep`_ for command in the man page of `vi`_ we see a lot of flag but they are `flag` that we can't use there. Let's check up on the web with `see the content of a file while in vim <https://duckduckgo.com/?q=see+the+content+of+a+file+while+in+vim>`_ and our trusty `instant answer panel` says that we can do that by pressing `:` and then typing **r** and the **filename**. We know that the password for user `bandit26` is in **/etc/bandit_pass/bandit26**. If we do `:` then type: `r /etc/bandit_pass/bandit26` we will see a warning with **Warning: Changing a readonly file** and lot of info about the file like owned by, file name, date etc. If we press `q` to exit we will see the password in the screen. Now exit from the machine.


Level 26
--------
It was very tough for me to get the password for previous level. Let's use it to entering the Level 26 machine::

   root@bandit:~# ssh bandit26@bandit.labs.overthewire.org -p 2220

Oh no! We are still getting the same error that we got when we first tried to login into `Level 25`_. Though we have the password for this user, the default shell is same `showtext` which only works in re-sized screen via `vi`_. If we run `grep`_ with **shell** in the man page of `vi`_ we see there is a option to **start shell commands** but we can't see any more details. Maybe we can change the default shell of our `bandit26` user? If we search in the web with `set shell variable inside vi <https://duckduckgo.com/?q=set+shell+variable+inside+vi>`_ we land in a Stack Overflow thread were we see that it is possible to set the shell variable value by pressing `:` and typing `set shell=/bin/bash` and then we would press `:` and type `shell` to go to the `bash`_ shell of user `bandit26`::

	:shell
	bandit26@bandit:~$ 

The `instructions for level 26 <https://overthewire.org/wargames/bandit/bandit27.html>`_ just says that "Good job getting a shell! Now hurry and grab the password for bandit27!" No clues! Let's see the files in the home directory with `ls`_::

	bandit26@bandit:~$ ls
	bandit27-do  text.txt
	bandit26@bandit:~$ 

So we have 2 files `bandit27-do` and `text.txt` file. The `bandit27-do` file seems interesting. If we check the file permission of the file with the `-la` flag of `ls`_ command::

	bandit26@bandit:~$ ls -la bandit27-do
	-rwsr-x--- 1 bandit27 bandit26 7296 Oct 16  2018 bandit27-do
	bandit26@bandit:~$ 

We can see that we are in the files group and group users have execution permission. Let's try to see the password of `bandit27` user from it's usual location `/etc/bandit_pass/bandit27`::

	bandit26@bandit:~$ ./bandit27-do cat  /etc/bandit_pass/bandit27

Well that was easy! We should be able to see the 33 character log string which is the flag for this level. Now we can exit from the machine.

	
Level 27
--------
Use the password from `Level 26`_ to `ssh`_ into the machine::

   root@bandit:~# ssh bandit27@bandit.labs.overthewire.org -p 2220

We can see in the `level 27 web page <https://overthewire.org/wargames/bandit/bandit28.html>`_ that we have a **git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo** the password for **bandit27-git is the same as bandit27**. We have to **Clone the repository to find the password**. So let's start by cloning the repository with `git`_-s `git-clone`_ command using the password of `bandit27` user. But to do that we need to create a directory in `/tmp` where we have read-write-execute access::

	bandit27@bandit:~$ mkdir -p /tmp/jonedoe27
	bandit27@bandit:~$ cd /tmp/jonedoe27
	bandit27@bandit:/tmp/jonedoe27$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
	Cloning into 'repo'...
	Could not create directory '/home/bandit27/.ssh'.
	The authenticity of host 'localhost (127.0.0.1)' can't be established.
	ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
	Are you sure you want to continue connecting (yes/no)? yes
	Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
	This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

	bandit27-git@localhost's password: 
	remote: Counting objects: 3, done.
	remote: Compressing objects: 100% (2/2), done.
	remote: Total 3 (delta 0), reused 0 (delta 0)
	Receiving objects: 100% (3/3), done.
	bandit27@bandit:/tmp/jonedoe27$ 

Now that we have the `repo` repository, let's take a look inside the directory to see what it has::

	bandit27@bandit:/tmp/jonedoe27$ ls repo/
	README
	bandit27@bandit:/tmp/jonedoe27$

One `README` is all we got. Checking the file contains of the `README` file gives us the password for next level::

	bandit27@bandit:/tmp/jonedoe27$ cat repo/README
	

Now clean up the file for make it hard to detect our intrusion and exit the machine::

	bandit27@bandit:/tmp/jonedoe27$ cd ..
	bandit27@bandit:/tmp$ rm -rf jonedoe27
	bandit27@bandit:/tmp$ exit
	logout


Level 28
--------
Entering the Level 28 machine using the password from previous level::

   root@bandit:~# ssh bandit28@bandit.labs.overthewire.org -p 2220

The `goal for level 28 <https://overthewire.org/wargames/bandit/bandit29.html>`_ is same as before. Get the password for next level from a **git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo** and use **bandit28's password when asked for bandit28-git's password as the are same**. So we will follow the same path to create a directory in `/tmp` directory and clone the `repo` repository and list it's files and directories::

	bandit28@bandit:~$ mkdir -p /tmp/jonedoe28
	bandit28@bandit:~$ cd /tmp/jonedoe28
	bandit28@bandit:/tmp/jonedoe28$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
	Cloning into 'repo'...
	Could not create directory '/home/bandit28/.ssh'.
	The authenticity of host 'localhost (127.0.0.1)' can't be established.
	ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
	Are you sure you want to continue connecting (yes/no)? yes
	Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
	This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

	bandit28-git@localhost's password: 
	remote: Counting objects: 9, done.
	remote: Compressing objects: 100% (6/6), done.
	remote: Total 9 (delta 2), reused 0 (delta 0)
	Receiving objects: 100% (9/9), done.
	Resolving deltas: 100% (2/2), done.
	bandit28@bandit:/tmp/jonedoe28$ ls repo/
	README.md
	bandit28@bandit:/tmp/jonedoe28$ 

Same as before we see a `README.md` file. If we see the contents of the file with `cat`_::

	bandit28@bandit:/tmp/jonedoe28$ cat repo/README.md 
	# Bandit Notes
	Some notes for level29 of bandit.

	## credentials

	- username: bandit29
	- password: xxxxxxxxxx

	bandit28@bandit:/tmp/jonedoe28$ 

That doesn't see to be a valid password. We know that `git`_ is version control system so maybe the password was there at some previous version but later changed? Let's change directory to enter the `repo` directory and run the `git-log`_ command to see the commited changes::

    bandit28@bandit:/tmp/jonedoe28$ cd repo/
    bandit28@bandit:/tmp/jonedoe28/repo$ git log
    commit 073c27c130e6ee407e12faad1dd3848a110c4f95
    Author: Morla Porla <morla@overthewire.org>
    Date:   Tue Oct 16 14:00:39 2018 +0200

        fix info leak

    commit 186a1038cc54d1358d42d468cdc8e3cc28a93fcb
    Author: Morla Porla <morla@overthewire.org>
    Date:   Tue Oct 16 14:00:39 2018 +0200

        add missing data

    commit b67405defc6ef44210c53345fc953e6a21338cc7
    Author: Ben Dover <noone@overthewire.org>
    Date:   Tue Oct 16 14:00:39 2018 +0200

        initial commit of README.md
    bandit28@bandit:/tmp/jonedoe28/repo$ 


So there we can see all the commits made in this repository and our initial guess was right. The password was there but it was removed with the last commit as it **leaks info**. Now we can go back to the version with password by using `git-checkout` command with the hash of the commit. The first 8 character of the hash is enough to identify it::

    bandit28@bandit:/tmp/jonedoe28/repo$ git checkout 186a1038
    Note: checking out '186a1038'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b <new-branch-name>

    HEAD is now at 186a103... add missing data
    bandit28@bandit:/tmp/jonedoe28/repo$ 


We see a bunch of message where basically `git`_ is complaining about going back to a version without creating a branch. At the last line it also says we are at **186a103... add missing data** commit. Now if we check the contents of the `README.md` file we should get the password for `Level 29`_::

    bandit28@bandit:/tmp/jonedoe28/repo$ cat README.md

Before we exit, we must remove work::

    bandit28@bandit:/tmp/jonedoe28/repo$ cd ../..
    bandit28@bandit:/tmp$ rm -rf jonedoe28
    bandit28@bandit:/tmp$ exit
    logout

.. note:: Git is a bit complex and has a very stiff learning curve but once mastared it can be a very helpful tool. It is out of scope for us to discuss the tricks of git here. A good place to get started with git would be at the `Official Website of Git <https://git-scm.com/>`_. I am also working on a `Git Cheat Sheet <git_cheat_sheet.html>`_.
    

Level 29
--------
Entering the Level 29 machine using the password from previous level::

   root@bandit:~# ssh bandit29@bandit.labs.overthewire.org -p 2220

We have the same `goal for level 29 <https://overthewire.org/wargames/bandit/bandit30.html>`_ as we had in `Level 28`_. We have to get the password for next level from a **git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo** and use **bandit29 and bandit29-git user has same password**. So we will follow the same path to create a directory in `/tmp` directory and clone the `repo` repository, change directory to `repo` directory and list it's files and directories::

    bandit29@bandit:~$ mkdir -p /tmp/jonedoe29
    bandit29@bandit:~$ cd /tmp/jonedoe29
    bandit29@bandit:/tmp/jonedoe29$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
    Cloning into 'repo'...
    Could not create directory '/home/bandit29/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? yes
    Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit29-git@localhost's password: 
    remote: Counting objects: 16, done.
    remote: Compressing objects: 100% (11/11), done.
    remote: Total 16 (delta 2), reused 0 (delta 0)
    Receiving objects: 100% (16/16), done.
    Resolving deltas: 100% (2/2), done.
    bandit29@bandit:/tmp/jonedoe29$ 
    bandit29@bandit:/tmp/jonedoe29$ cd repo/
    bandit29@bandit:/tmp/jonedoe29/repo$ ls -la
    total 16
    drwxr-sr-x 3 bandit29 root 4096 Jan 21 13:19 .
    drwxr-sr-x 3 bandit29 root 4096 Jan 21 13:19 ..
    drwxr-sr-x 8 bandit29 root 4096 Jan 21 13:19 .git
    -rw-r--r-- 1 bandit29 root  131 Jan 21 13:19 README.md
    bandit29@bandit:/tmp/jonedoe29/repo$ 


If we see the contents of the `README.md` file with `cat`_::

    bandit29@bandit:/tmp/jonedoe29/repo$ cat README.md 
    # Bandit Notes
    Some notes for bandit30 of bandit.

    ## credentials

    - username: bandit30
    - password: <no passwords in production!>

    bandit29@bandit:/tmp/jonedoe29/repo$ 

Again we see that in the place of password we have some sort of variable that say's "no passwords in production!". Let's run `git-log`_ in the repository::

    bandit29@bandit:/tmp/jonedoe29/repo$ git log
    commit 84abedc104bbc0c65cb9eb74eb1d3057753e70f8
    Author: Ben Dover <noone@overthewire.org>
    Date:   Tue Oct 16 14:00:41 2018 +0200

        fix username

    commit 9b19e7d8c1aadf4edcc5b15ba8107329ad6c5650
    Author: Ben Dover <noone@overthewire.org>
    Date:   Tue Oct 16 14:00:41 2018 +0200

        initial commit of README.md
        bandit29@bandit:/tmp/jonedoe29/repo$ 

Hmm, so they fix **username** on the last commit!? I am not sure what that is. Let's check the difference between the `fix username` commit with commit id `84abedc1` and the `initial commit of README.md` with commit id `9b19e7d8`::

    bandit29@bandit:/tmp/jonedoe29/repo$ git diff 84abedc1 9b19e7d8
    diff --git a/README.md b/README.md
    index 1af21d3..2da2f39 100644
    --- a/README.md
    +++ b/README.md
    @@ -3,6 +3,6 @@ Some notes for bandit30 of bandit.
     
      ## credentials
       
    -- username: bandit30
    +- username: bandit29
      - password: <no passwords in production!>
         
    bandit29@bandit:/tmp/jonedoe29/repo$ 

So previously the user name was `bandit29` now it is `bandit30`. Could be that the password for `bandit29` is same as `bandit30`? If we try that it doesn't work. Nor the passwords `<no passwords in production!>` and `no passwords in production!`. I got stuck here for some time. After sometime it came to mind that it also support branches. Maybe there is a branch that is not production and contains the password? Usually when we clone only `master` branch is created but the remote can have more branches. We can we use `git branch --help` command to see how to list remote branches. We find that `-r` flag list the remote tracking branches. Let's see what branches we have::

    bandit29@bandit:/tmp/jonedoe29/repo$ git branch -r
      origin/HEAD -> origin/master
      origin/dev
      origin/master
      origin/sploits-dev
    bandit29@bandit:/tmp/jonedoe29/repo$ 

 So we have 2 more branch `dev` and `sploits-dev` in our remote repository named `origin`. Let's checkout the `dev` with `git-checkout`_::

    bandit29@bandit:/tmp/jonedoe29/repo$ git checkout -b dev origin/dev 
    Branch dev set up to track remote branch dev from origin.
    Switched to a new branch 'dev'
    bandit29@bandit:/tmp/jonedoe29/repo$ 
    
If we list the files and directories with `ls`_::

    bandit29@bandit:/tmp/jonedoe29/repo$ ls
    code  README.md
    bandit29@bandit:/tmp/jonedoe29/repo$ 

We see the `README.md` here. We can to see the password for Level 30 by::

    bandit29@bandit:/tmp/jonedoe29/repo$ cat README.md

We will exit from the machine, after the basic clean up::

    bandit29@bandit:/tmp/jonedoe29/repo$ cd ../..
    bandit29@bandit:/tmp$ rm -rf jonedoe29
    bandit29@bandit:/tmp$ exit
    logout


Level 30
--------
We will enter Level 30 machine using the password from previous level::

   root@bandit:~# ssh bandit30@bandit.labs.overthewire.org -p 2220

The `instructions of level 30 <https://overthewire.org/wargames/bandit/bandit31.html>`_ is just like before. Find the password from **ssh://bandit30-git@localhost/home/bandit30-git/repo git repository** and use **bandit30 and bandit30-git password interchangeable**. We will proceed as before, create a directory in `/tmp`, clone the repository, enter the `repo` directory and list the files and directories::

    bandit30@bandit:/tmp/jonedoe30$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
    Cloning into 'repo'...
    Could not create directory '/home/bandit30/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? yes
    Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit30-git@localhost's password: 
    remote: Counting objects: 4, done.
    remote: Total 4 (delta 0), reused 0 (delta 0)
    Receiving objects: 100% (4/4), done.
    bandit30@bandit:/tmp/jonedoe30$ cd repo/
    bandit30@bandit:/tmp/jonedoe30/repo$ ls
    README.md
    bandit30@bandit:/tmp/jonedoe30$ 

Does the `README.md` contains something for us?::

    bandit30@bandit:/tmp/jonedoe30/repo$ cat README.md 
    just an epmty file... muahaha
    bandit30@bandit:/tmp/jonedoe30/repo$ 

No luck there! Let's get `git`_-ing. First we will check the log::

    bandit30@bandit:/tmp/jonedoe30/repo$ git log
    commit 3aa4c239f729b07deb99a52f125893e162daac9e
    Author: Ben Dover <noone@overthewire.org>
    Date:   Tue Oct 16 14:00:44 2018 +0200

        initial commit of README.md
    bandit30@bandit:/tmp/jonedoe30/repo$ 

Nothing much in the log as well. Listing the remote branches shows us::

    bandit30@bandit:/tmp/jonedoe30/repo$ git branch -r
      origin/HEAD -> origin/master
      origin/master
    bandit30@bandit:/tmp/jonedoe30/repo$ 

No extra branch in the remote repository as well. Git also supports tagging [see more at `git-tag`_]. If we give list all tags with the `-l` flag, we see::

    bandit30@bandit:/tmp/jonedoe30/repo$ git tag -l
    secret
    bandit30@bandit:/tmp/jonedoe30/repo$ 

So we have a tag named `secret`, let's check it out to a branch named `test`::

    bandit30@bandit:/tmp/jonedoe30/repo$ git checkout -b test secret
    fatal: reference is not a tree: secret
    bandit30@bandit:/tmp/jonedoe30/repo$ 

After reading some more man page on `git-tag`, I decided to take help from the `Pro Git book <https://git-scm.com/book/en/v2>`_-'s `Tagging <https://git-scm.com/book/en/v2/Git-Basics-Tagging>`_ section. There I saw the `git-show` command. Using the command on the `secret` tag like this `git show secret` returned a 33 character long string. This seems to be our flag. Let's move on!

We will do some house keeping like good guys before we exit the machine::

    bandit30@bandit:/tmp/jonedoe30/repo$ cd ../..
    bandit30@bandit:/tmp$ rm -rf jonedoe30
    bandit30@bandit:/tmp$ exit
    logout


Level 31
--------
Entering the Level 31 machine using the password from previous level::

   root@bandit:~# ssh bandit31@bandit.labs.overthewire.org -p 2220

The `goal of level 31 <https://overthewire.org/wargames/bandit/bandit32.html>`_ is simple and same as before. Clone the repository at **ssh://bandit31-git@localhost/home/bandit31-git/repo** use **bandit31's password for bandit31-git user**, use your `git`_ skill and find the password.

We will start same as before by clone the repository, going into it and list it's contents::

    bandit31@bandit:~$ mkdir -p /tmp/jonedoe31
    bandit31@bandit:~$ cd /tmp/jonedoe31
    bandit31@bandit:/tmp/jonedoe31$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
    Cloning into 'repo'...
    Could not create directory '/home/bandit31/.ssh'.
    The authenticity of host 'localhost (127.0.0.1)' can't be established.
    ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
    Are you sure you want to continue connecting (yes/no)? yes
    Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit31-git@localhost's password: 
    remote: Counting objects: 4, done.
    remote: Compressing objects: 100% (3/3), done.
    remote: Total 4 (delta 0), reused 0 (delta 0)
    Receiving objects: 100% (4/4), done.
    bandit31@bandit:/tmp/jonedoe31$ cd repo/
    bandit31@bandit:/tmp/jonedoe31/repo$ ls
    README.md
    bandit31@bandit:/tmp/jonedoe31/repo$ 

Just like before we have a handy-dandy `README.md`. What is inside it? Wait no more::

    bandit31@bandit:/tmp/jonedoe31/repo$ cat README.md 
    This time your task is to push a file to the remote repository.

    Details:
        File name: key.txt
        Content: 'May I come in?'
        Branch: master

    bandit31@bandit:/tmp/jonedoe31/repo$ 

This time we have task description in the `README.md`, where we have to push a file named **key.txt** with the content **May I come in?** to the **master** branch of the remote repository. This seemingly easy task can be very problematic for the `git`_ uninitiated. If we just know the basics of `git`_, we would know that this is a simple task of creating the file adding it with `git-add`_, commiting with `git-commit`_ and pushing to remote with `git-push`_. Let's do that step by step::

    bandit31@bandit:/tmp/jonedoe31/repo$ echo May I come in? >> key.txt
    bandit31@bandit:/tmp/jonedoe31/repo$ git add key.txt 
    The following paths are ignored by one of your .gitignore files:
    key.txt
    Use -f if you really want to add them.
    bandit31@bandit:/tmp/jonedoe31/repo$ 

What now? So it seems that the `key.txt` in been added to the `gitignore`_ file. `Git`_, Our dear friend, is suggesting us that we can use the `-f` flag to for `git`_ to add the file. We will do that and continue with the steps::

    bandit31@bandit:/tmp/jonedoe31/repo$ man gitignore
    bandit31@bandit:/tmp/jonedoe31/repo$ git add -f key.txt 
    bandit31@bandit:/tmp/jonedoe31/repo$ git commit -m "added key.txt file"
    [master 8a337d7] added key.txt file
     1 file changed, 1 insertion(+)
      create mode 100644 key.txt
    bandit31@bandit:/tmp/jonedoe31/repo$ git push 

Once we give it the password of `bandit31` it will try to push the changes and will fail. But if we see the log of the `git-push`_ command we can see that we have the password for Level 32 by. We will do some house keeping before exiting::

    bandit31@bandit:/tmp/jonedoe31/repo$ cd ../..
    bandit31@bandit:/tmp$ rm -rf jonedoe31
    bandit31@bandit:/tmp$ exit
    logout


Level 32
--------
Using the password from previous level::

   root@bandit:~# ssh bandit32@bandit.labs.overthewire.org -p 2220

This time we see there is something different, at the end of the `motd`_ we see this::

    WELCOME TO THE UPPERCASE SHELL
    >> 

It is not our default shell. The `hint for level 32 <https://overthewire.org/wargames/bandit/bandit33.html>`_ just say's **its time for another escape**. Let's see what we have in the home directory shall we::

    WELCOME TO THE UPPERCASE SHELL
    >> ls
    sh: 1: LS: not found
    >> 

Oh well, no it becomes more clear. **THE UPPERCASE SHELL** transforms every command to uppercase and we need to **escape** it. What if we give the command in upper case? Would it transform it to lower case?::

    >> LS
    sh: 1: LS: not found
    >> 

That doesn't work! What about numbers?::

    >> 0
    sh: 1: 0: not found
    >> 1
    sh: 1: 1: not found
    >> 

We it seems it is not changes the numbers. From all this errors it is clear to us that it usages the `sh`_ shell. Let's check the man page for it. Now as there is now clue left for us, after searching the man page, scratching head for a very very long time we would come across the `Special Parameters` section where we would see special characters like `@` that expands to positional parameters or `#` that expands to number of positional parameters and then `$` that gives use the PID of invoked shell and `0` expands to the name of the shell or shell script. We have seen numbers before, haven't we? Like in `ls`_ it gives error that **sh: 1: LS: not found** so `ls`_ is taken as argument 1 so let's try to invoke shell with the script name::

    >> $0
    $ 

Hmm, can we try to run `/bin/bash` to get the `bash`_ shell?::

    $ /bin/bash
    bandit33@bandit:~$ 

Yes! At last we are inside a `bash`_ shell. We can to see the password for Level 33 with::

    bandit33@bandit:~$ cat /etc/bandit_pass/bandit33

This will give us a 33 character long string which is the flag of this level. Now exit from the machine.


Level 33
--------
Entering the Level 33 machine using the password from previous level::

   root@bandit:~# ssh bandit33@bandit.labs.overthewire.org -p 2220

If we check the web `page of level 33 <https://overthewire.org/wargames/bandit/bandit34.html>`_ it says that **At this moment, level 34 does not exist yet.**. Let's see what we have in the home directory::

    bandit33@bandit:~$ ls
    README.txt
    bandit33@bandit:~$ 

We see a `README.txt` file. If we `cat`_ the file, we see that::

    bandit33@bandit:~$ cat README.txt 
    Congratulations on solving the last level of this game!

    At this moment, there are no more levels to play in this game. However, we are constantly working
    on new levels and will most likely expand this game with more levels soon.
    Keep an eye out for an announcement on our usual communication channels!
    In the meantime, you could play some of our other wargames.

    If you have an idea for an awesome new level, please let us know!
    bandit33@bandit:~$ 

We see the message of compilation for Bandit game! Hooray! 



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
.. _ssh: https://linux.die.net/man/1/ssh
.. _sftp: https://linux.die.net/man/1/sftp
.. _nc: https://linux.die.net/man/1/nc
.. _openssl: https://linux.die.net/man/1/openssl
.. _s_client: https://linux.die.net/man/1/s_client
.. _nmap: https://linux.die.net/man/1/nmap
.. _echo: https://linux.die.net/man/1/echo
.. _ncat: https://linux.die.net/man/1/ncat
.. _diff: https://linux.die.net/man/1/diff
.. _crontab: https://linux.die.net/man/1/crontab
.. _chmod: https://linux.die.net/man/1/chmod
.. _md5sum: https://linux.die.net/man/1/md5sum
.. _cut: https://linux.die.net/man/1/cut
.. _bash: https://linux.die.net/man/1/bash
.. _for: https://linux.die.net/man/1/for
.. _if: https://linux.die.net/man/3/if
.. _timeout: https://linux.die.net/man/1/timeout
.. _rm: https://linux.die.net/man/1/rm
.. _date: https://linux.die.net/man/1/date
.. _more: https://linux.die.net/man/1/more
.. _vi: https://linux.die.net/man/1/vi
.. _git: https://linux.die.net/man/1/git
.. _git-clone: https://linux.die.net/man/1/git-clone
.. _git-log: https://linux.die.net/man/1/git-log
.. _git-tag: https://linux.die.net/man/1/git-tag
.. _git-add: https://linux.die.net/man/1/git-add
.. _git-commit: https://linux.die.net/man/1/git-commit
.. _git-push: https://linux.die.net/man/1/git-push
.. _gitignore: https://linux.die.net/man/5/gitignore
.. _sh: https://linux.die.net/man/1/sh
.. _explainshell.com: https://explainshell.com
.. _crontab guru: https://crontab.guru/
.. _Shebang: https://en.wikipedia.org/wiki/Shebang_(Unix)
.. _bash script: https://www.gnu.org/software/bash/
.. _sh script: https://en.wikipedia.org/wiki/Bourne_shell


..
    Loots!!
    bandit0:bandit0
    bandit1:boJ9jbbUNNfktd78OOpsqOltutMc3MY1
    bandit2:CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
    bandit3:UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
    bandit4:pIwrPrtPN36QITSp3EQaw936yaFoFgAB
    bandit5:koReBOKuIDDepwhWk7jZC0RTdopnAYKh
    bandit6:DXjZPULLxYr17uwoI01bNLQbtFemEgo7
    bandit7:HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
    bandit8:cvX2JJa4CFALtqS87jk27qwqGhBM9plV
    bandit9:UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
    bandit10:truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
    bandit11:IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
    bandit12:5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
    bandit13:8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
    bandit14:4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
    bandit15:BfMYroe26WYalil77FoDi9qh59eK5xNr
    bandit16:cluFn7wTiGryunymYOu4RcffSxQluehd
    bandit17:xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
    bandit18:kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
    bandit19:IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
    bandit20:GbKksEFF4yrVs6il55v6gwY5aVje5f0j
    bandit21:gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
    bandit22:Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
    bandit23:jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
    bandit24:UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
    bandit25:uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
    bandit26:5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
    bandit27:3ba3118a22e93127a4ed485be72ef5ea
    bandit28:0ef186ac70e04ea33b4c1853d2526fa2
    bandit29:bbc96594b4e001778eee9975372716b2
    bandit30:5b90576bedb2cc04c86a9e924ce42faf
    bandit31:47e603bb428404d265f59c42920d81e5
    bandit32:56a9bf19c63d650ce78e6ec0354ee45e
    bandit33:c9c3199ddf4121b10cf581a98d51caee


