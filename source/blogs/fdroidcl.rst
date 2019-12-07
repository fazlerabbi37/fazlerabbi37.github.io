fdroidcl
========
`< Blog <../blog.html>`_

Playing around with fdroidcl; a `F-Droid <https://f-droid.org/>`_ desktop client.

Created on: 2019-01-20

F-Droid is an awesome App store that focuses on open source Android application. fdroidcl as it says in its `GitHub repo <https://github.com/mvdan/fdroidcl>`_; is a F-Droid desktop client.

fdroidcl can be used to perform much of the regular actions like update, search, install, uninstall, download and more. The major actions are documented at the GitHub repo. With fdroidcl we can perform some more advance actions like combination of two commands and not all of the are documented. While using fdroidcl I found a few and I will list them here.

List of search options
----------------------
This are the search options::

    fdroidcl search [option]
    
    -q      Print package names only
    -i      Filter installed apps
    -u      Filter apps with updates
    -d      Select apps last updated in the last <n> days; a negative value drops them instead
    -c      Filter apps by category
    -o      Sort order (added, updated)

List all installed apps
-----------------------
To list all installed apps on a device we can use the following command::

    fdroidcl search -i -q

Source
------
 - `fdroidcl <https://github.com/mvdan/fdroidcl>`_
