Screen Cheat Sheet
==================
`< Blog <../blog.html>`_

A quick reference to Screen aka GNU Screen

Created on: 2020-03-17

Tag: `cheat_sheet <tag_cheat_sheet.html>`_, `living_in_the_shell <tag_living_in_the_shell.html>`_

.. role:: kbd

install in Ubuntu
-----------------
to install in Ubuntu 18.04::

    sudo apt install screen -y

start a session
---------------
to start a new session::

    screen

We will be greeted with the welcome screen with information related to screen. We can turn it off by default by editing the ``~/.screenrc`` and adding the following::

    startup_message off

start a named session
---------------------
If we type ``screen`` then ``screen`` will autmaticalley designate a name for the session that follows this scheme::

        11547.pts-5.gun_screen
          ^       ^    ^
          |       |    |
        PID of    |  hostname
     the session  |
                    
            psudo terminal
               number


Session name is used while reattaching to a session, for example we will reattach to the session in the example with ``screen -r pts-5.gun_screen``. Though in ``bash`` tab completion for session name is supported but this long complex naming structure can be problematic when frequently detaching and reattaching. So we can assign name to a session like this with the `-S` flag::

    screen -S screen_test

create a new window
-------------------
By default each session is created with one window numbered as `0`. To create a new window:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`c`

The :kbd:`Ctrl` + :kbd:`a` is called the escape command and used to invoke ``screen``. The :kbd:`c` is the command which screen gets after invocation.

.. note:: The escape command can be changed, which we will see later.

.. note:: The commands after the escape command is case sensitive.


switch between window
---------------------
to switch between window, we can go to next window:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`n`

or go to previous window:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`p`

another quick way to switch between window is to use the window numbers like `0` or `1` but remember that this only works for window `0` to `9` like this:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`5`

to use two digit numbered window do the following:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`'`

There should be a prompt at the left bottom saying ``Switch to window:``. Now type the window number:

    :kbd:`12`

This obviously works with single digit numbered window. 


list all the window
-------------------
to list all the window:

   :kbd:`Ctrl` + :kbd:`a` then press :kbd:`"`. [:kbd:`"` is :kbd:`Shift` + :kbd:`'`]
 
This shows a list of windows with 3 column: Num, Name and Flags. We can use the :kbd:`↑` and :kbd:`↓` to select a window and press :kbd:`Enter` to switch to that window.

show all windows
----------------
to see all the windows of a session:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`w`

This will show the number and name of all the windows at the bottom of the screen like this::

    0-$ bash  1*$ bash  2$ bash

The ``*`` after the 1 means that we are currently on window 1.

rename a window
---------------
we have already seen that we can list and see window with window name but by default all of the are name are ``bash`` as that is the programming running in them. To change the name of a window:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`A`

We will see a prompt at the left bottom saying ``Set window's title to: bash``. We need to press :kbd:`Backspace` until it reaches **:** now we can type the window title and press :kbd:`Enter` to rename it.

kill a window
-------------
to kill a window:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`K`

We should get a prompt at the usual left bottom corner saying ``Really kill this window [y/n]`` type `y` and press :kbd:`Enter` to kill the window.

detach from a session
---------------------
to detach from a session:

    :kbd:`Ctrl` + :kbd:`a` then press :kbd:`d`

In the terminal we should see something similar to ``[detached from 23537.screen_test]``.

list all session
----------------
to list all session::

    screen -ls

If we have multiple session we would see something like this::

	There are screens on:
		23537.screen_test	(03/18/2020 05:10:48 PM)	(Detached)
		23547.screen_test	(03/18/2020 05:10:48 PM)	(Attached)
		23557.screen_test1	(03/18/2020 05:10:48 PM)	(Detached)
	3 Sockets in /run/screen/S-$USER.

Yes, we can assign same name for two different session but that is not that useful.

to attach to a detached session
-------------------------------- 
From our previous output, we can see that we have 3 session and 2 with same name. To attach to a detached session we normal use the `-r` flag like this::

	screen -r screen_test1

As we can see for unique name we can use the session name but for sessions with same name we have to specify the PID as well, like this::

	screen -r 23537.screen_test
    
We can also use tab completion to get our window without typing.

exit form session
-----------------
to exit from a session, first we need to attach to that session::

	screen -r 23547.screen_test

Now we will :kbd:`Ctrl` + :kbd:`a` to invoke ``screen`` then type `:quit` and press :kbd:`Enter`. Back in the terminal we should see::

	[screen is terminating]
 

share a screen session with other user
--------------------------------------
we can share session with other user. The user must have an valid account in the server. To share a screen session, fist we need to make sure that ``screen`` has `setuid root` which will enable multiuser support. To `setuid root`::

	chmod +s /usr/bin/screen

Now if we can use the `-x` flag followed by `$USER/$SCREEN_SESSION_NAME`, like following, we see::

	screen -x screen_user/screen_test1

	There is a screen on:
		23537.screen_test       (03/18/2020 05:10:48 PM)        (Private)
	There is no screen to be attached matching reg.

The ``screen_user`` hasn't allowed multiuser so other can't see the session. if ``screen_user`` wants to enable multiuser:

	:kbd:`Ctrl` + :kbd:`a`. next press :kbd:`:` and type `multiuser on`.

Next we will allow our user:

	:kbd:`Ctrl` + :kbd:`a`. next press :kbd:`:` and type `acladd $USER_NAME`

Now if the other user ran the ``screen -x screen_user/screen_test1`` he would be able to see the session and perform all the operations.

To remove a user from the ACL: :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`:` and type `acldel $USER_NAME` To turn off multiuser: :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`:` and type `multiuser off`.
	
source: https://serverfault.com/a/336613
	

scrolling in screen
-------------------
This is one of few odd things that a new user face while using ``screen``. While inside the ``screen`` the default scroll don't work but we still can scroll through the history. Moreover, we can copy, paste and log that history. To start scrolling back:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`[`

This will activate the `Copy mode` [just like vim 😉]. Now we can use the :kbd:`↑`, :kbd:`↓`, or :kbd:`Page up`, :kbd:`Page down`, :kbd:`Home`, :kbd:`End` or vim's :kbd:`j` :kbd:`k` buttons to navigate through the history. We can also copy the history. To copy history, we have to move our courser to the position where we want to start copying and press :kbd:`Enter` then move the courser to the place where we want the copy to end and :kbd:`Enter` again. To paste the copied text do:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`[`


log output to a file
--------------------
to log output of a screen window we need to press:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`H`

This will save the output to a file name ``screenlog.$NUM``. The `NUM` variable starts from `0`. If we do :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`w` to see the windows title we will see something like this::

    0*$(L) bash  1-$(L) bash  2$ bash

The ``*`` means we are currently in that window and the ``(L)`` means we are logging those windows.

Splitting the screen
--------------------
We can split the screen in horizontal and vertical half. To split the screen in horizontal half:

   :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`S`

to split the screen in vertical half:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`|`

By default the screen neither switch to the splitted half nor starts a new window. We need to do both manually. First, to switch between the half use:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`Tab`

Now we can either create a new window with :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`c` or place a previously created window with :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`$WINDOW_NUMBER`.


Exiting from splitted screen
----------------------------
to exit from splitted screen, go to the window you want to use and do:

    :kbd:`Ctrl` + :kbd:`a`. next press :kbd:`Q`


.. note:: till this most of the things are from `Softpedia News: GNU Screen Tutorial: How to use the screen's most important features. <https://news.softpedia.com/news/GNU-Screen-Tutorial-44274.shtml>`_ article because this was one of the article I got that was very easy for me to understand the besics and start using it.


Accidental freezing
-------------------
Sometimes while invocing screen with :kbd:`Ctrl` + :kbd:`a` we misplace our finger and press :kbd:`Ctrl` + :kbd:`s`. This will freeze our screen session. To unfreeze:

    :kbd:`Ctrl` + :kbd:`Q`

source: https://unix.stackexchange.com/a/12108

kill a screen session
---------------------
to kill a screen session::

    screen -X -S $SESSION_YOU_WANT_TO_KILL quit

source: https://stackoverflow.com/a/1509764


Source
------
- https://linux.die.net/man/1/screen
- https://www.gnu.org/software/screen/manual/html_node/index.html
- https://www.gnu.org/software/screen/
- https://news.softpedia.com/news/GNU-Screen-Tutorial-44274.shtml

