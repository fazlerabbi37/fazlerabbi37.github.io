HackGame Walkthrough
====================
`< Blog <../blog.html>`_

Walkthrough of `HackGame3 <https://hackgame.chaurocks.com>`_, a browser-based web CTF.

Created on: 2020-02-02

.. role:: kbd

From the HackGame3 homepage::

    HackGame3 is a free, safe, legal, browser-based and timed game for hackers to test and expand their exploration skills.

I can't remember exactly where I did I get the `HackGame3`_ site but I find it somewhere floating in the internet around a year ago and gave it a go. I went till level 6 both because till that it was very easy, just picking up the connections. I stopped at level 7 because it required some JavaScript and at that time I had zero understanding of JavaScript. It not like that now I know JavaScript so I am up for round 2. 😛 It's just that after finishing `Bandit Walkthrough`_, I was going through my old notes and I found that I already wrote bits of how to pass form one level to another till level 7. From there I just picked up the old clues, organized them and tried to solve the next level with the help of my mate `@nr072`_. So let's began!

Presequisite
------------
We need a working internet, any modern browser like Google Chrome or Firefox and time.

Starting the game
-----------------
To start the game, just visit `HackGame3`_. We will see a big **Start** button with basic instructions bellow and a leaderboard on the right. Clicking on the **Start** button starts the game. Each level has a web page designated for it. The structure of the pages are same. Level heading, level hint, two input box for username and password and finally a **Lasson larned** section where it is said what should be done to remedy the problem. Remember that the game is time base, so time required to solve each level is recorded and the quicker the better.


Level 1
-------
The clue for this level is **Do you notice something in the URL? Try to access level 2 directly!**. If we see the URL, we would see:

    https://hackgame.chaurocks.com/level1

This is a screenshot of the URL bar of that level:

.. image:: ../static/media/hackgame_walkthrough_image_01.png
   :align: center
   :alt: Level 1 URL Screenshot


As the clue suggested we can change end of the URL form `level1` to `level2` and go to the next level.

Level 2
-------
The clue for this level is **Was level one too easy? Try again with something different!**. Again, if we see the URL, we would see:

    https://hackgame.chaurocks.com/level2?logged=false

What would happen if we changed the `logged` to **true** from **false**?

As I said the beginning levels are too easy! We are in level 3.

Level 3
-------
The clue for this level is **Very good! Do you know some default username/password combinations?**. I am sure everyone guessed it by now! Yes, it it `admin`, `admin`. Let's move on to `Level 4`_


Level 4 
-------
The clue for this level is **Do you know how to read source code?**. That means we have to get the source of this page. IMO, the clean way to read code would be to view source. Press :kbd:`Ctrl` + :kbd:`u` to open current pages source code in new window.

In the source we could see comments along with the actual source code. One comment says `Start looking here` as we see in the screenshot:

.. image:: ../static/media/hackgame_walkthrough_image_02.png
   :align: center
   :alt: Start looking here Comment

Just under the comment we have a from that takes an username and password. If we skip that we would see one more comment that says `TODO: Remove this comment before publishing`. With that we would have our username and password as we see in the screenshot bellow:


.. image:: ../static/media/hackgame_walkthrough_image_03.png
   :align: center
   :alt: Devlopment username and password


Use this in the actual page to go to the next level.

Level 5 
-------
The clue for this level is **Great job! Try it again!**. So we will do the same as `Level 4`_. We will view the source code with :kbd:`Ctrl` + :kbd:`u` where we would see the same `Start looking here` comment and bellow that comment we should see the login form. If we go a bit bellow we would see a script were a JavaScript function named **checkSubmit**. The function first gets the `username` and `password` from the page and then first check if it is `undefined` then if not it would check our input with a hard-coded username and password and return **true** if it matches or else returns `false`.

.. image:: ../static/media/hackgame_walkthrough_image_04.png
   :align: center
   :alt: Hard-coded username and password

If we use this we would be able to go to the next level, `Level 6`_.

P.S: For me, the novice in JavaScript, I wondered how did after from submission the from knew it had to run the `checkSubmit` function? Well, just after the check finises we see 3 more lines of code that gets the `password-form` `element by ID`_ and if it is not `undefined` then calls itself.

.. image:: ../static/media/hackgame_walkthrough_image_05.png
   :align: center
   :alt: Calling the checkSubmit function.


Level 6 
-------
.. The clue for this level is ****. If we see the , we would see:
.. 
.. .. image::
..    :align: center
..    :alt: alternate text





.. Level 
.. -------
.. The clue for this level is ****. If we see the , we would see:
.. 
.. .. image::
..    :align: center
..    :alt: alternate text

Source
------
.. _HackGame3: https://hackgame.chaurocks.com
.. _Bandit Walkthrough: blogs/bandit_walkthrough.html
.. _@nr072: https://github.com/nr072
.. _element by ID: https://www.w3schools.com/jsref/met_document_getelementbyid.asp
