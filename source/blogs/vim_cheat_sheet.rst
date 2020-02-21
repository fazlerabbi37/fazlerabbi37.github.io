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

https://stackoverflow.com/a/235841

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
https://stackoverflow.com/a/2966034


find and replace
----------------
to find and replace

    :kbd:`Esc` the :kbd:`:` the `%s/$REPLACE_THIS/$WITH_THIS/g`

pecific lines

    :kbd:`Esc` the :kbd:`:` the `$START_LINE,$END_LINEs/$REPLACE_THIS/$WITH_THIS/g`

add `c` after `g` to enter an interactive mode.

source: `Find and replace strings in vim on multiple lines <https://stackoverflow.com/a/19995072>`_

move to the beginning of line
-----------------------------
to move to the beginning or start of line:

    :kbd:`0`

source: https://stackoverflow.com/a/10243634

move to the end of line
-----------------------
to move to the end of line:

    :kbd:`$`

source: https://stackoverflow.com/a/105734

delete all line till end
------------------------
to delete all line till end:

    :kbd:`d` + :kbd:`G`

source: https://stackoverflow.com/a/8124616

open in readonly mode
---------------------
to open in readonly mode inside vim:

   :kbd:`Esc` + :kbd:`:` then type `view /path/to/file`

source: https://stackoverflow.com/a/18395765

display line numbers
--------------------
to display line numbers:

   :kbd:`Esc` + :kbd:`:` then type `set number` or `set nu`

to disable::

    :kbd:`Esc` + :kbd:`:` then type `set nonumber` or `set nonu`

source: https://vim.fandom.com/wiki/Display_line_numbers

see file type
-------------
to see file type:

    :kbd:`Esc` + :kbd:`:` then type `set ft`

source: https://vim.fandom.com/wiki/Filetype.vim

macros
------
record a macros:

    :kbd:`Esc` then :kbd:`q` + :kbd:`any key like d,m,n` for register.

the do you task and press :kbd:`q`. It will save the macro to the register [one of those d,m,n that you pressed]. To use the macro:

    number_of_times_you_want_to_execute + :kbd:`@` + :kbd:`register_key_d_m_or_n`

source: https://vim.fandom.com/wiki/Macros

abbreviations
-------------
set an abbreviation:

    :kbd:`Esc` then :kbd:`:` `ab $ABBREVIATION $FULL_TEXT_FOR_THE_ABBREVIATION`

for example:

    :kbd:`:` `ab rtfm read the fine manual`

source: https://vim.fandom.com/wiki/Using_abbreviations

fix indentation
---------------
to fix indentation on a selected part of the file:

    :kbd:`=`

to fix indentation on a whole file:

    :kbd:`g` + :kbd:`g` + :kbd:`=` + :kbd:`G`

source: https://vim.fandom.com/wiki/Fix_indentation

Source
------
 - ` <>`_
