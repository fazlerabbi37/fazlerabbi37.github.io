Inside a docx file
==================
`< Blog <../blog.html>`_

Let's take a peek inside a docx file.

Created on: 2019-01-22

While converting ``.docx`` file to ``.md`` using ``pandoc`` I faced a unique problem. Each time I converted the ``.docx`` file to ``.md``, the images in the ``.md`` file where getting jumbled. While investigating I came across this `GitHub issue <https://github.com/jgm/pandoc/issues/1979>`_ and a fascinating `comment <https://github.com/jgm/pandoc/issues/1979#issuecomment-76958416>`_ about ``.docx`` files which says it is just a fancy ``zip`` file with ``xml`` mapping.

Let's dive in. Let's take a ``.docx`` file and start probing.

First let's download a ``.docx`` file::

    wget https://calibre-ebook.com/downloads/demos/demo.docx

Then, we will need to change the file extention::

    mv demo.docx demo.zip

Unzipping::

    unzip demo.zip -d demo

Looking at the file tree::

    ls -R demo

Gives us the following output::

    demo:
    '[Content_Types].xml'   customXml   docProps   _rels   word

    demo/customXml:
    item1.xml  item2.xml  itemProps1.xml  itemProps2.xml  _rels

    demo/customXml/_rels:
    item1.xml.rels  item2.xml.rels

    demo/docProps:
    app.xml  core.xml

    demo/_rels:

    demo/word:
    document.xml  endnotes.xml  fonts  fontTable.xml  footnotes.xml  media  numbering.xml  _rels  settings.xml  styles.xml  theme  webSettings.xml

    demo/word/fonts:
    font1.odttf  font2.odttf  font3.odttf  font4.odttf  font5.odttf  font6.odttf

    demo/word/media:
    image1.gif  image2.png  image3.png  image4.png

    demo/word/_rels:
    document.xml.rels  fontTable.xml.rels  numbering.xml.rels

    demo/word/theme:
    theme1.xml


We will look more closely in all of this file in future!

Source
------
- `--extract-media for docx reader not working <https://github.com/jgm/pandoc/issues/1979>`_
- `'docx is a fancy zip' comment <https://github.com/jgm/pandoc/issues/1979#issuecomment-76958416>`_
