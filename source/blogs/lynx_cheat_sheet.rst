Lynx Cheat Sheet
=====================================
`< Blog <../blog.html>`_

A quick reference to `Lynx <https://invisible-island.net/lynx>`_, a text-based web browser.

Created on: 2020-06-02

Tag: `cheat_sheet <tag_cheat_sheet.html>`_, `living_in_the_shell <tag_living_in_the_shell.html>`_

.. role:: kbd

The bottom of the Lynx show all the useful keyboard keys to help navigation easier but here are few that I found most used and worth taking note.

Install
-------
To install Lynx in Ubuntu::

    sudo apt install lynx

Go to a website
---------------
To go to a website::

    lynx protocol://domain.tld

    OR

    lynx domain.tld

From inside the browser, press: :kbd:`g` and then ``protocol://domain.tld`` OR ``domain.tld``

Or we can edit the existing URL by typing :kbd:`Shift` + :kbd:`g`.

source: `Lynx Users Guide: Starting Lynx with a Remote File <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#Remote>`_

Exit from Lynx
--------------
To exit from Lynx, press: :kbd:`q`.

This will invoke a yes/no prompt. Type ``y`` to exit. To exit without prompt press :kbd:`Shift` + :kbd:`q`.  

source: `Lynx Users Guide: Leaving Lynx <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#Leaving>`_

Go back
-------
To go back, press: :kbd:`←`.

source: `Lynx Users Guide: Navigating hypertext documents with Lynx <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#IntraDocNav>`_

Working with link
-----------------
We can use :kbd:`↑` and :kbd:`↓` to select a link and use :kbd:`→` or :kbd:`⏎`

source: `Lynx Users Guide: Navigating hypertext documents with Lynx <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#IntraDocNav>`_

Save rendered file to disk
--------------------------
To save file to disk, press: :kbd:`p`.

Now we are presented with options to save file, mail. print to screen or print to a connected printer. Using the arrow key select the 'Save to a local file'. Now we need to enter a file name with that the file will be saved.

source: `Lynx Users Guide: Printing, Mailing, and Saving rendered files to disk <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#Disposing>`_

See source
----------
To see source, press: :kbd:`\\`.

source: `Lynx Users Guide: Viewing the HTML document source and editing documents <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#LocalSource>`_

Download source file
--------------------
To download source file, press: :kbd:`d` or :kbd:`D`.

source: `Lynx Users Guide: Downloading and Saving source files <https://lynx.invisible-island.net/lynx_help/Lynx_users_guide.html#RemoteSource>`_

Options
-------
There are lot of options available in Lynx. We can access the by pressing :kbd:`o`.

Bookmarks
---------
To save a bookmark, press:

    :kbd:`a`

Now press :kbd:`s` to bookmark the page, :kbd:`l` to bookmark selected link or :kbd:`c` to cancel.

Press :kbd:`v` to see all bookmark file and :kbd:`v` to remove a bookmark. Press kbd:`e` to edit if you have external editor configured, which can be done with `Options`_




Source
------
- `Resources <https://lynx.invisible-island.net/lynx-resources.html>`_
- `Lynx help files <https://lynx.invisible-island.net/lynx_help/lynx_help_main.html>`_
- `Wikipedia: Text-based web browser <https://en.wikipedia.org/wiki/Text-based_web_browser>`_
