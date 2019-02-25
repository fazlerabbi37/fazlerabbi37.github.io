Hacking a Zkteco access control device to take attendance
=========================================================
How we hacked(modified!?) a Zkteco access control device to take automatic attendance.


We had a good old attendance system for our team in my workplace where we used to sign in and sign out the time on a piece of paper. Then those entries were added to an Google Sheet if needed. This system was going well for a starting member of 15 but it became very painful as we grew in number. We decided to automate the system if possible. We could have chosen the most convenient way and brought a time attendance device but if we went that route, I wouldn't be writing this hack-blog, would I be?

.. ::image:: ../source/media/zkteco_f18_back.jpg

We have know for sometime that we have a Zkteco device installed in front of our door but we didn't know anything about it at all so we started digging. On the first glance all we could see the is the Zkteco company logo so we searched with the company name and came up with their official website. The website has an array of different devices ranging from Access Control, Time Attendance, Biometrics Access, Entrance Control etc and most of them looked similar. Closer inspection of the devices was necessary and we unmounted the device from the wall.

On the back we found an reset button. Oh, did I say we didn't have access to the menu of the device as it already had an admin setup? No worries, we would reset it. After the reset, I enrolled myself as an admin user and now we could see the menu and more option popped out. We saw a database management option where all the access logs were saved. We save an option to backup data to USB storage and after a close look, we also find a USB port on the side of the device. We plugged an empty USB device and used that option to dump the data onto that USB drive. To add to our problem it was a ``.dat`` file that couldn't be opened with any online tool we tried.

On the back side of device we found more information about the device. It was a Zkteco `F18 <https://www.zkteco.com/en/product_detail/F18.html>`_ Access Control device. We found manual but Zkteco would not allow us to download the manual if we don't open an account first. We downloaded the manual after opening an account with a `Disposable <https://temp-mail.org/>`_ email account.

After reading the somewhat long manual of 92 page, we found out the our device can only be used for access control, meaning upon presenting a valid credential it would sent signal to a door lock to open. That wouldn't be super helpful if want to take attendance with it.

On the manual we also find that the device can be accessed over a network. Now we got curious and connected the device to our intranet. We tried to ping the device but go no response. After fiddling with the network settings a bit we figured out the subnet mask was wrong and after fixing that we got ping. Yea! But now what???

On the Download Center, from where we downloaded the manual we noticed something call ZKAccess. We decided to install in on a Windows host. After the installing ZKAccess when we opened it it asked for a password but we didn't set any as of yet. Digging through the ZKAccess management we found out that the user name and password both are ``admin``. 

With the help of the might man, ahem manual we were able to connect our device over network to the ZKAccess software. Basically on Ethernet communication mode the device opens up a TCP/IP port, port 4370 to the LAN where ZKAccess connects with correct communication password. With ZKAccess we could pull the data from device and see the access log for each ID aka user. But we were still miles away from have a automatic attendance system. The log would show all the entries for for a user, as in each time a user has provided a valid credential it would log that. This is nowhere useful for use.

On the ZKAccess manual's index we saw a section about reporting, Access Control Reporting and kept reading. We found out that we can create custom report and export them on as ``xls``. So we created a custom report that takes the time, first name, last name and the id and ran a few test export. All go so far. So now we have a semi-automated (semi as someone still need to download data form device, run the custom report and export the xls) way of getting the access log from the device to an easily usable format. What now? 

We need to put this attendance data on a Google Sheet for it to shareable with our Team Leads and HR. We started to tweak around ways to get a final output from the xls. Hmm, what can we do to achieve it? We tied to come up with all sorts of equation for Excel and Google Sheet to process the data until we saw a suggestion on the Stak Overflow to use `Google Apps Script <https://script.google.com>`_. Google Apps Script aka GScript is JS adapted for Google API which is a topic on itself. So now the question is, can Google Apps Script save our day?

On the journey to find our answer, we landed on the `Developer Doc <https://developers.google.com/apps-script/reference/spreadsheet/>`_ page for Spreadsheet Service. And we progressed one step at a tie from there on. I would rather say they were teeny-tiny, baby steps.

The data from the xls was copy-pasted to a Worksheet of a Google Sheet. The first 4 columns are used keeping consistency with exported data; time, first name, last name and the id. The target is to process the data and get a in-time and out-time for each id and the also finding the duration for each id. 

First step was to figure out a way to load the data of the 4 columns from the Worksheet to GScript. When we succeeded on that we noticed that the date time wasn't quite correct. We wasted a good amount of time trying to figure out this problem. 

The basic operation to achieve our goal is as follows:

- get active Sheet's first Worksheet
- format the time column to time format of ``hh:mm:ss A/P"M"``
- format the id column to integer number format 
- format a long row to time format of ``hh:mm:ss A/P"M"`` as this is where the final output will put
- get all the all id from the id column
- define a array where all the id that we need to take attendance is stored in a ascending order.
- get all id's and loop through all the id to check if it exist on our wanted id list if not clear the content for the id
- sort all the cells based on id column
- now we have a time sorted array of all the id we want to take attendance
- declare a dictionary with all the wanted id and a initial value of 0. this will hold the number of time in id has used the device.
- now loop through all the id and increase the value of dictionary to get the frequency
- now start at the top and you have the out time of the first id then look up the frequency of first id and jump that many row. you have the in time. the next row is next id's out time and so on
- make a function to return diff between tow time given as param. 
- now take all 3 and put them on the long row that we defined before.

That gets the job done! I know not the most efficient or elegant way of achieving our goal but it get's the job done. We have been using it for an year now and it working well till now.

I would polish the code a bit and publish it in GitHub and link it here.

A big thanks goes to Kazi Tusher for helping with the hardware specs, Bidhan Bhushan Roy for those crazy Execl equations, `Nafiur Rahman <https://github.com/nr072>`_ and `Rajib Kumar Chanda <https://github.com/RajibChanda>`_ for helping with the algo and tolerating my noob JS queries.



Source
------
- `Zkteco F18 <https://www.zkteco.com/en/product_detail/F18.html>`_
