Rails Console Cheat Sheet
=========================
`< Blog <../blog.html>`_

A quick reference to Rails Console.

Created on: 2019-01-22

Tag: `cheat_sheet <blogs/tag_cheat_sheet.html>`_

Save rails console output to file
---------------------------------
To save rails console output to a file, do the following [1]_::

    f = File.new("$file_name", 'w')
    f << command
    f.close

Show all user
-------------
Run the following command to see all user [2]_::

    User.all

Show all user with pretty print 
-------------------------------
Run the following command to see all user with pretty print [2]_::

    pp User.all

Delete user
-----------
To delete a user run the following [2]_::
user = User.find_by_display_name("My New User Name")
user.delete

Source
------
.. [1] `rails - Redirecting console output to a file <https://stackoverflow.com/a/13380275/5350059>`_
.. [2] `Deleting Users with Rails Console <https://stackoverflow.com/a/6034846/5350059>`_
