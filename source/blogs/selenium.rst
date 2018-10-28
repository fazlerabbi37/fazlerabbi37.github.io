Selenium
========
Notes for Selenium with Python3.

Setup
-----
1. Install Selenium
```````````````````
we can install selenium with pip::


    sudo pip3 install selenium


2. Install ``geckodriver``
``````````````````````````
To run Firefox browser we need to install ``geckodriver``. Let's head over to `geckodriver releases page <https://github.com/mozilla/geckodriver/releases>`_ and get the latest version of ``geckodriver`` for Linux 64 bit. Downloaded file will look like this ``geckodriver-vx.y.z-linux64.tar.gz``. Now we will extract the ``.tar`` file::

    tar -xvzf geckodriver*

Make it executable::

    chmod +x geckodriver

Move to ``/usr/local/bin/``::

    sudo mv geckodriver /usr/local/bin/

Remove the ``.tar`` file::

    rm geckodriver*

3. Install ``chromedriver`` 
```````````````````````````
To run Chrome and Chromium we need to install ``chromedriver`` which we can get from `chromedriver download page <https://sites.google.com/a/chromium.org/chromedriver/downloads>`_. Get the latest version of ``chromedriver`` for  Linux 64 bit. Downloaded file will look like this ``chromedriver_linux64.zip``. Now we need to unzip the ``.zip`` file::

    unzip chromedriver*

.. note:: if you don't have unzip install with ``sudo apt install unzip``

Make it executable::

    chmod +x chromedriver

Move to ``/usr/local/bin/``::

    sudo mv chromedriver /usr/local/bin/

Remove the ``.zip`` file::

    rm chromedriver*

Getting Started
---------------
Import webdriver
````````````````
To get started we need to import webdriver from selenium::

    from selenium import webdriver

Choose browser
``````````````
We can choose Firefox, Chrome or Chromium as our client browser::

    browser = webdriver.$client_browser()

Where ``$client_browser= 'Firefox', 'Chrome' or 'Chromium'``.  

Open a URL
``````````
After the selecting the ``browser`` we can use the ``get()`` method to open a URL.::

    browser.get('url.tld')

For exapmle::

    browser.get('https://duckduckgo.com')

Source
------
 - `Where to find geckodriver needed by Selenium Python package? <https://askubuntu.com/a/863211>`_
 - `Setting Up ChromeDriver and the Selenium-WebDriver Python bindings on Ubuntu 14.04 <http://blog.likewise.org/2015/01/setting-up-chromedriver-and-the-selenium-webdriver-python-bindings-on-ubuntu-14-dot-04/>`_
