Publish Sphinx doc with GitHub Pages
====================================
The whole process of publishing Sphinx generated doc with GitHub Pages.

GitHub Pages is a very interesting and useful way to host project or code documentations. There are three ways we can use GitHub Pages in our project:

1. A ``master`` branch with ``index.html`` in the root directory
2. A ``docs`` directory in the ``master`` branch with ``index.html`` in the root directory
3. A ``gh-pages`` branch with ``index.html`` in the root directory

This site usages the first method. I use reStructuredText(rST) to write the content. Then I use a ``shell`` script that usages ``rst2html.py`` from ``docutils`` to generate ``html`` files. The ``index.html`` is kept in the root directory of ``master`` branch and all other ``html`` files relative to the ``index.html`` which is a bit complex if done manually and is not really clean if we are doing code documentation.

I am using Sphinx for code and project documentation for sometime now. I like Sphinx as it usages rST which I am familiar with and it has tons of extension and a nice interface. Generating ``html`` from Sphinx is as easy as typing ``make html`` which generates ``html`` files in a pre-defined build directory. The build directory is defined in the ``Makefile``.

Now here is the problem, Sphinx generates docs to a pre-defined directory within a ``html`` directory and GitHub Pages can only build pages if ``index.html`` is found in the root directory of ``master`` branch or ``docs`` directory in ``master`` branch or root directory of ``gh-pages`` branch. If we are using separate directory for ``source`` and ``build`` the generated ``html`` files will be in ``build\html`` directory. From the project root directory the path is ``docs\build\html`` which GitHub Pages can't find and throws a ``404`` error. Even if we don't use separate directory for ``source`` and ``build`` the ``html`` file path will be ``docs\html`` which is not acceptable for GitHub Pages.

Now we will use a trick to fool both Sphinx and GitHub Pages.

1. At first modify the ``Makefile`` in the docs directory that was generated with Sphinx. Modify the ``BUILDDIR`` variable to be ``..`` from ``build``.::

    BUILDDIR      = ..
    #BUILDDIR      = build

What it means that Sphinx will make a ``html`` directory in the root directory of ``master`` branch when we will make html with ``make html`` command. We can modify the ``make.bat`` to reflect the change if we wish make html in Windows as well::

    set BUILDDIR=..
    REM set BUILDDIR=build


2. Rename the ``docs`` folder to ``html``.

3. Build the documentation: ``make html``. It finds a ``html`` directory at it's build path which is root  directory of ``master`` branch and builds all the ``html`` file there.

4. Create a ``.nojekyll`` file with ``touch .nojekyll`` command which will say GitHub Pages to ignore Jekyll theme which fixes the broken ``css`` problem.

5. Undo ``step 2`` by renaming the ``html`` folder to ``docs`` where the GitHub Pages will look for when build pages.

I wrote a small shell script, `make_github_pages_from_sphinx.sh <https://github.com/fazlerabbi37/Code.random/blob/c7ae5ec32a8b6eb703a37cd6085a557f503a856c/shell/make_github_pages_from_sphinx.sh>`_ to do all this steps at one go. The script assumes you have a docs directory at the project root directory and you are using separate ``source`` and ``build`` directory.

Now the last thing we need to do is head over to GitHub and go to the project ``Settings`` and select 'master branch /docs folder' as Source in GitHub Pages section. Give GitHub Pages a minute to build the pages and visit the link given at 'Your site is ready to be published at...' and you should see the Sphinx generated docs.

This blog is inspired by the blog `Sphinx + GitHub pages <https://jefflirion.github.io/sphinx-github-pages.html>`_ by `Jeff Irion <https://jefflirion.github.io/>`_ and tries to fix the broken ``css`` problem by adding ``.nojekyll`` in ``docs`` directory.

