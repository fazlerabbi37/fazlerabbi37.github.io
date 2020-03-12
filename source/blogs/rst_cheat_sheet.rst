ReStructuredText Cheat Sheet
============================
`< Blog <../blog.html>`_

A quick reference to ReStructuredText

Created on: 2019-11-19

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

.. warning:: under heavy construction and not well organized

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

    .kbd {
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

Inline Markup
-------------
This are the following inline markups. Source: `Quick reStructuredText:Inline Markup <https://docutils.sourceforge.io/docs/user/rst/quickref.html#inline-markup>`_


italic or emphasis
``````````````````

bold or strong emphasis
```````````````````````
To do bold or strong emphasis::

    **strong emphasis**

The result will be **strong emphasis**.

hyperlink
----------
https://docutils.sourceforge.io/docs/user/rst/quickref.html#hyperlink-targets


Comments
--------
one line comment::

    .. comment 

multi line comments::

   .. This text will not be shown
   (but, for instance, in HTML might be
   rendered as an HTML comment) 

https://docutils.sourceforge.io/docs/user/rst/quickref.html#comments

Add image
---------
to add image::

   .. image:: path/to/image.ext
      :height: 100
      :width: 200
      :scale: 50
      :alt: alternate text 

source: https://docutils.sourceforge.io/docs/user/rst/quickstart.html#images

superscript
-----------
to do superscript::

    x :sup:`y`

The result would be x :sup:`y`.

source: https://docutils.sourceforge.io/docs/ref/rst/roles.html#superscript

subscript
---------
to do subscript::

    x :sub:`y`

The result would be x :sub:`y`.

source: https://docutils.sourceforge.io/docs/ref/rst/roles.html#subscript

Rendering
---------
This part is all about ``docutils`` packages various tools like ``rst2html``, ``rst2html5`` rendering tricks.

add custom JavaScript (JS) with HTML
````````````````````````````````````
First we need to find out what template is being used by the renderer and it's path. For example, the template used by ``rst2html`` is located in ``/usr/share/docutils/writers/html4css1/template.txt`` for ``rst2html5`` the file is at ``/usr/share/docutils/writers/html5_polyglot/template.txt``. For others try the `--help` switch and look for the `--template` switch and read the description on the right to find the file path. Now we need to copy the file to a location we have write access to as we would modify and use it instead of the default one. We can do a lot of cusomization on this template file that but for now let's focuse on JS. Open the file with a text editor and add either a JavaScript code snipite::

	%(head_prefix)s
	%(head)s
	<script>
		alert("JS is added!!!")
	</script>
	%(stylesheet)s
	%(body_prefix)s
	%(body_pre_docinfo)s
	%(docinfo)s
	%(body)s
	%(body_suffix)s
 
Or add a external JS file path::

	%(head_prefix)s
	%(head)s
	<script src="../RELATIVE/PATH/FROM/DOCUMENT/test.js"></script>
	%(stylesheet)s
	%(body_prefix)s
	%(body_pre_docinfo)s
	%(docinfo)s
	%(body)s
	%(body_suffix)s

Now use the custom template with the `--template` like this::

    rst2html5 --template=template.txt document.rst

source: https://stackoverflow.com/a/3922784


add custom CSS with HTML
````````````````````````
to add custom CSS with HTML we can use the `--stylesheet` switch, but the trick is that before using our custom CSS we have to apply the `docutils` provided CSS first. We can find those default CSS if we take a look at the `--stylesheet-dirs` switch's description. Once we find the we will just use the default CSS names (as the renderer already knows the path for those) and then our custom CSS full path and separate all the CSS by comma like this for `rst2html5`::

    rst2html5 --stylesheet=minimal.css,plain.css,$PATH/TO/CSS/main.css document.rst

    

include generation date time at the end of document
```````````````````````````````````````````````````
to add generation date time at the end of document use `-d` and `-t` switches::

    rst2html5 -d -t document.rst


show link to source at the end of document
``````````````````````````````````````````
to show link to source at the end of document we can use the `-s` switch the is also another switch `--source-url` where we can specify the path to the documents, like this::

    rst2html5 -s --source-url=/PATH/TO/$DOCUMENT document.rst



Source
------
