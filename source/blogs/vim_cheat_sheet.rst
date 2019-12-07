Vim Cheat Sheet
===============
`< Blog <../blog.html>`_

A quick reference to Vim.

Created on: 2019-09-08

.. warning:: under heavy construction and not well organized

.. role:: kbd

exit from vim
-------------
to exit from vim press :kbd:`Esc` then type `:q!`


subscript
---------

  :kbd:`ctrl` + :kbd:`k` [digit] :kbd:`s`


(source: https://vi.stackexchange.com/q/7368)

superscript
-----------

  :kbd:`ctrl` + :kbd:`k` [digit] :kbd:`S`

(source: https://vi.stackexchange.com/q/7368)

indent multiple lines
---------------------
to indent multiple lines select lines in VISUAL mode and do

    :kbd:`>`

do one level indentation of next five line

    :kbd:`5 >` 

https://stackoverflow.com/a/235841/5350059

paste mode
----------
to enable paste mode do

   :kbd:`Esc` then type `:set paste`

insert current date
-------------------
to insert current date

     :kbd:`Esc` then type `:pu=strftime('%Y-%m-%d')`

https://vim.fandom.com/wiki/Insert_current_date_or_time

Switching case of characters
----------------------------
to switching case of characters

    Toggle case "HellO" to "hELLo" with :kbd:`g` + :kbd:`~` then a movement.
    
    Uppercase "HellO" to "HELLO" with :kbd:`g` + :kbd:`U` then a movement.
    
    Lowercase "HellO" to "hello" with :kbd:`g` + :kbd:`u` then a movement.

https://vim.fandom.com/wiki/Switching_case_of_characters
https://stackoverflow.com/a/2966034/5350059


Source
------
 - ` <>`_
