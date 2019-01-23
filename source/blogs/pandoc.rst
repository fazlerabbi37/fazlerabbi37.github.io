Pandoc
======
Using Pandoc to convert documents.

I have recently discovered ``pandoc``, a command line tool for converting documents. It is a very useful tool and as it says in their site it is turning out to be a universal document convert for me. I am mainly using ``pandoc`` to convert Microsoft Word Documents (``.docx``) documents to Markdown (``.md``).

Installation 
------------
I am using Ubuntu 18.04 LTS so installing ``pandoc`` is as easy as typing::

    sudo apt install pandoc -y

Usages
------
So lets see some usage.

We can use the following command to converting ``.docx`` to ``.md``::

    pandoc --extract-media=$media_dir -f docx example.docx -t markdown -o example.md

See more usages at `Pandoc Demo Example page <https://pandoc.org/demos.html>`_. Try online at `Try pandoc! <http://pandoc.org/try/>`_.

Source
------
- `Pandoc officail site <https://pandoc.org/>`_
- `Pandoc Demo Example page <https://pandoc.org/demos.html>`_
- `Try pandoc! <http://pandoc.org/try/>`_
- `Pandoc convert docx to markdown with embedded images <https://stackoverflow.com/a/39961440>`_
