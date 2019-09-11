Markdown Cheat Sheet
====================
A quick reference to Markdown.


Styles
------
There are many styles support in Markdown. So of them are as follows:

Italics
```````
To make a phrase italic in Markdown, we can surround words which may span multiple words with an underscore '_' or '*' without quotes. For example::

    _Writing in Markdown is not that hard!_

    *Writing in Markdown is not that hard!*

Both gives the following output:

    *Writing in Markdown is not that hard!*

Bold
````
To make phrases bold in Markdown, we can surround words which may span multiple words with two asterisks '__' or '**' without quotes. For example::

    __Writing in Markdown is not that hard!__

    **Writing in Markdown is not that hard!**

Both gives the following output:

    **Writing in Markdown is not that hard!**


Strikethrough
`````````````
To strikethrough a phrases in Markdown, we can surround words which may span multiple words with two asterisks '~~' without quotes. For example::

    ~~Writing in Markdown is not that hard!~~

Gives the following output:

.. container:: strike

     Writing in Markdown is not that hard!

.. pulled this trick following this Stack Overflow `answer <https://stackoverflow.com/a/14295112>`_


Headers
````````
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
`````
There are two different link types in Markdown:

 - Inline
 - Reference

Inline
''''''
To create an inline link, we need to wrap the link text in brackets '[ ]' without quote, and then we wrap the link in parenthesis '( )' For example::

    [Visit GitHub!](www.github.com)

Gives the following output:

    `Visit GitHub! <www.github.com>`_

Above is the simplest way of Markdown inline link. Here are some more examples::

    [I'm an inline-style link with title](https://www.google.com "Google's Homepage")

    [I'm a relative reference to this repository's index file](../index.html)

Reference
'''''''''
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


Images
``````
If we know how to create links in Markdown, we can create images, too. The syntax is nearly the same.

To create an inline image link to https://octodex.github.com/images/bannekat.png, with an alt text that says, Benjamin Bannekat, we would write this in Markdown::

    ![Benjamin Bannekat](https://octodex.github.com/images/bannekat.png).


Giving us the following output:


.. image:: https://octodex.github.com/images/bannekat.png
   :alt: Benjamin Bannekat
   :align: center


This is called the inline style of image linking. Here are a few alternative ways to do it::

    ![](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
    ![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

They both give us the following output:

.. image:: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png
   :alt: Logo Title Text 1
   :align: center


We can also link an image with reference linking same as the `Reference`_ type of Links with the only difference where we need to put '!' without quote to the reference text. For example::

    ![The first father][First Father]

    ![The second first father][Second Father]


    [First Father]: http://octodex.github.com/images/founding-father.jpg
    [Second Father]: http://octodex.github.com/images/foundingfather_v2.png


Gives us the following output:

The first father |First Father|

The second first father |Second Father|

.. |First Father| image:: http://octodex.github.com/images/founding-father.jpg
                  :alt: First Father
                  :align: middle
.. |Second Father| image:: http://octodex.github.com/images/foundingfather_v2.png
                   :alt: Second Father
                   :align: middle

We can also do it like this::

    ![alt text][logo]

    [logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"

Giving us the following output:

.. image:: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png
   :alt: Logo Title Text 2
   :align: center

Blockquotes
```````````
If we need to call special attention to a quote from another source, or design a pull quote for a magazine article, then Markdown's blockquote syntax will be useful.

To create a block quote, all we have to do is preface a line with the "greater than" caret '>' without quote. For example::

    I read this interesting quote the other day:

    > "Her eyes had called him and his soul had leaped at the call. To live, to err, to fall, to triumph, to recreate life out of life!"

Gives us the following output:

I read this interesting quote the other day:

  "Her eyes had called him and his soul had leaped at the call. To live, to err, to fall, to triumph, to recreate life out of life!"


We can also place a caret character on each line of the quote. This is particularly useful if your quote spans multiple paragraphs. For example::

    > His words seemed to have struck some deep chord in his own nature. Had he spoken
    of himself, of himself as he was or wished to be? Stephen watched his face for some
    moments in silence. A cold sadness was there. He had spoken of himself, of his own
    loneliness which he feared.
    >
    > — Of whom are you speaking? Stephen asked at length.
    >
    > Cranly did not answer.

Gives us the following output:

  His words seemed to have struck some deep chord in his own nature. Had he spoken
  of himself, of himself as he was or wished to be? Stephen watched his face for some
  moments in silence. A cold sadness was there. He had spoken of himself, of his own
  loneliness which he feared.

  \- Of whom are you speaking? Stephen asked at length.

  Cranly did not answer.



Lists
`````
There are two types of lists in the known universe: unordered and ordered. That's a fancy way of saying that there are lists with bullet points, and lists with numbers.

Unordered
'''''''''
To create an unordered list, we'll want to preface each item in the list with an asterisk '*' or '-' or '+' without quote, one item par line. For example, a grocery list in Markdown might look like this::

    * Milk
    * Eggs
    * Salmon
    * Butter

Giving the output:

* Milk
* Eggs
* Salmon
* Butter

Occasionally, you might find the need to make a list with more depth, or, to nest one list within another. For example::

    * Tintin
     * A reporter
     * Has poofy orange hair
     * Friends with the world's most awesome dog
    * Haddock
     * A sea captain
     * Has a fantastic beard
     * Loves whiskey
       * Possibly also scotch?

Gives us the following output:

* Tintin

 * A reporter
 * Has poofy orange hair
 * Friends with the world's most awesome dog

* Haddock

 * A sea captain
 * Has a fantastic beard
 * Loves whiskey

    * Possibly also scotch?

Ordered
'''''''
An ordered list is prefaced with numbers, instead of asterisks. Take a look at this recipe:

1. Crack three eggs over a bowl
2. Pour a gallon of milk into the bowl
3. Rub the salmon vigorously with butter
4. Drop the salmon into the egg-milk bowl

To write that in Markdown, you'd do this::

    1. Crack three eggs over a bowl
    2. Pour a gallon of milk into the bowl
    3. Rub the salmon vigorously with butter
    4. Drop the salmon into the egg-milk bowl

We can also make unordered list under ordered list and vice-versa.


Paragraphs
``````````
Markdown has several ways of formatting paragraphs. If we forcefully insert a new line for each line, we would end up having a paragraph for each line. For example::

    Do I contradict myself?

    Very well then I contradict myself,

    (I am large, I contain multitudes.)

Would result in:

Do I contradict myself?

Very well then I contradict myself,

(I am large, I contain multitudes.)

This is called a  hard break; where we can have soft break but giving two space '  ' without quote at the end of each line. For example::

    Do I contradict myself?
    Very well then I contradict myself,
    (I am large, I contain multitudes.)

Which will be rendered as

Do I contradict myself?

Very well then I contradict myself,

(I am large, I contain multitudes.)

Without the line break or two spaces, Markdown will consider all three line as one.::

    Do I contradict myself?
    Very well then I contradict myself,
    (I am large, I contain multitudes.)

Giving:

Do I contradict myself?
Very well then I contradict myself,
(I am large, I contain multitudes.)



.. note:: markdown-here Markdown Cheatsheet: Code and Syntax Highlighting, Tables, Inline HTML, Horizontal Rule, Line Breaks, YouTube Videos


Markdown on different website
-----------------------------
Many website supports markdown or somewhat modified versions of markdown. I am listing a few bellow.

Facebook
````````
It would seem as of Sept 11, 2019; Markdown is not supported in Facebook Post but it supports in Facebook Messenger. Messenger markdown support:

- `Bold`_ with `*text*`
- `Italics`_ with `_text_`
- `Strikethrough`_ with `~text~`
- `Monospace` with `\`text\``
- `Codeblock` with::

    ```
    text
    ````
- `LaTeX typesetting` with `\\(text\\)`

source: https://www.facebook.com/help/147348452522644


Workplace
`````````
`Workplace by Facebook <https://www.facebook.com/workplace>`_ (sort of Facebook for organization) supports Markdown on both Messenger and Post.

- Bold with `**text**`
- Italics with `*text*`
- List with  `- item`
- Link with `[title](https://facebook.com)`
- Numbered list with `1. first item`
- Quote with `> quote`
- H1 with `# Heading`
- H2 with `## Heading`
- Inline code with `code`

source: https://www.facebook.com/help/work/541260132750354


.. GitHub
.. ``````
.. GitLab
.. ``````


More Resources
--------------
- `Markdown Example Wikipedia <http://en.wikipedia.org/wiki/Markdown#Example>`_
- http://spec.commonmark.org/dingus/
- http://johnmacfarlane.net/babelmark2/faq.html
- http://idratherbewriting.com/2013/06/04/exploring-markdown-in-collaborative-authoring-to-publishing-workflows/
- https://www.markdownguide.org

Source
------
 - `Markdown Tutorial <https://www.markdowntutorial.com>`_
 - `markdown-here Markdown Cheatsheet <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>`_
