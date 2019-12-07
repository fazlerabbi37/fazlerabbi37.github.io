ReStructuredText Cheat Sheet
============================
`< Blog <../blog.html>`_

A quick reference to ReStructuredText

Created on: 2019-11-19

.. warning:: under heavy construction and not well organized

<kbd>

render html code
----------------
to render html code::

	.. raw:: html

		<a href="testurl">testurl</a>

https://stackoverflow.com/a/50566700/5350059


add custom role to render with css
----------------------------------
first add the css style to css file and give it a name.::

    .red {
        color:red;
        }

then use that name as role in rst::

    .. role:: red

    An example of using :red:`interpreted text`


https://stackoverflow.com/a/4669850/5350059

add keyboard key rendering
--------------------------
by default rst doesn't support keyboard key rendering role `:kdb:` but we can add custom css to do that. edit the css file and put::

    .kbd
    {
        -moz-border-radius:3px;
        -moz-box-shadow:0 1px 0 rgba(0,0,0,0.2),0 0 0 2px #fff inset;
        -webkit-border-radius:3px;
        -webkit-box-shadow:0 1px 0 rgba(0,0,0,0.2),0 0 0 2px #fff inset;
        background-color:#f7f7f7;
        border:1px solid #ccc;
        border-radius:3px;
        box-shadow:0 1px 0 rgba(0,0,0,0.2),0 0 0 2px #fff inset;
        color:#333;
        display:inline-block;
        font-family:Arial,Helvetica,sans-serif;
        font-size:11px;
        line-height:1.4;
        margin:0 .1em;
        padding:.1em .6em;
        text-shadow:0 1px 0 #fff;
    }


now to use it in a file do::

    .. role:: kbd

    :kbd:`keyboard_key`

https://meta.superuser.com/q/4788/655587

and custom role source


Multiline Admonitions (ie. note, warning, hint)
-----------------------------------------------
to add multiline admonitions like note, warning or hint, just indent the paragraph bellow the directives like this::

    .. note::

        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, 
        when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into
        electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages
        and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.

https://sublime-and-sphinx-guide.readthedocs.io/en/latest/notes_warnings.html

Hyperlink a section in the same document
----------------------------------------
to hyperline a section in the same document do::

    `section name`_


Source
------
