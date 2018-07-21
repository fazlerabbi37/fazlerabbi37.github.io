Markdown Cheat Sheet
====================
A quick reference of Markdown.


Italics
-------
To make a phrase italic in Markdown, we can surround words which may span multiple words with an underscore '_' or '*' without quotes. For example::

    _Writing in Markdown is not that hard!_

    *Writing in Markdown is not that hard!*

Both gives the following output:

    *Writing in Markdown is not that hard!*

Bold
----
To make phrases bold in Markdown, we can surround words which may span multiple words with two asterisks '__' or '**' without quotes. For example::

    __Writing in Markdown is not that hard!__

    **Writing in Markdown is not that hard!**

Both gives the following output:

    **Writing in Markdown is not that hard!**


Strikethrough
-------------
To strikethrough a phrases in Markdown, we can surround words which may span multiple words with two asterisks '~~' without quotes. For example::

    ~~Writing in Markdown is not that hard!~~

Gives the following output:

.. container:: strike

     Writing in Markdown is not that hard!

.. pulled this trick following this Stack Overflow `answer <https://stackoverflow.com/a/14295112>`_


Headers
-------
To make headers in Markdown, we preface the phrase with a hash mark '#' without quotes. There are six types of headers, in decreasing sizes. We need to place the same number of hash marks as the size of the header we want::

    # Header one
    ## Header two
    ### Header three
    #### Header four
    ##### Header five
    ###### Header six

Gives the following output:

Header one
----------

Header two
``````````

Header three
''''''''''''

Header four
...........

Header five
~~~~~~~~~~~

Header six
**********


Alternatively, for Header one and Header two, an underline-ish style can be used::

    Alt-H1
    ======

    Alt-H2
    ------

Giving the same output of Header one and Header two:

Alt-H1
------

Alt-H2
``````


Links
-----
There are two different link types in Markdown:

 - Inline
 - Reference

Inline
``````
To create an inline link, we need to wrap the link text in brackets '[ ]' without quote, and then we wrap the link in parenthesis '( )' For example::

    [Visit GitHub!](www.github.com)

Gives the following output:

    `Visit GitHub! <www.github.com>`_

Above is the simplest way of Markdown inline link. Here are some more examples::

    [I'm an inline-style link with title](https://www.google.com "Google's Homepage")

    [I'm a relative reference to this repository's index file](../index.html)

Reference
`````````
To create a reference link we wrap both the link text and the reference text in brackets '[ ]' without quote and at the bottom we write the reference by wrapping the reference text in '[]' followed by a ':' both without quote and then we put the actual URL. For example:: 

    Here's [a link to something else][another place].
    
    [another place]: www.github.com

Gives us the following output:

    Here's a `link to something else`_.

    .. _link to something else: www.github.com

Above is the simplest way of Markdown reference link. Here are some more examples::


    [You can use numbers for reference-style link definitions][1]

    Or leave it empty and use the [link text itself].

    URLs and URLs in angle brackets will automatically get turned into links.
    http://www.example.com or <http://www.example.com> and sometimes
    example.com (but not on Github, for example).

    [1]: http://slashdot.org
    [link text itself]: http://www.reddit.com














Source
------
 - `Markdown Tutorial <https://www.markdowntutorial.com>`_
 - `markdown-here Markdown Cheatsheet <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>`_

