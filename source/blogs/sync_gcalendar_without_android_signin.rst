Google Calendar sync on Android without signing in
==================================================
Want to sync your Google Calendar sync on Android but don't want to add your Google account on Android?

Created on: 2019-02-05

.. role::  raw-html(raw)
    :format: html


I have been trying to stay away from `Google products <https://en.wikipedia.org/wiki/List_of_Google_products>`_ as much as possible by using their FOSS counterparts. Naturally, I don't like the idea of adding my Google account on Android. Though I have been trying to `avoid Google products <https://fazlerabbi37.github.io/take_back_my_data/>`_ it is still one of the best and convenient product line for most of the people. For example, both my university and current workplace usages G Suite.

Google Calendar is still a very convenient and popular tool for scheduling. Most of my coworkers usages Google Calendar to schedule meeting and to sent invitation for a event. I miss out the most convening features; auto sync to Android calendar and last minute notifications about events as I don't have my G Suite accounts signed in my Android. Only if there was a way to sync them without signing in!

Well, I was using this awesome tool called `ICSx⁵ <https://f-droid.org/en/packages/at.bitfire.icsdroid/>`_ to sync a Public Google Calendar which takes a ``.ical`` formatted URL and syncs it to Android calendar. I saw a ``Requires Authentication`` toggle button just bellow the URL input fields. Then, the next question was can we sync a Private calendar using the authentication? I jumped to the Google Calendar's settings page to grab the *Public address in iCal format* only to find a warning on the bottom that say's "Warning: The address won't work unless this calendar is public."

I though let's dig a bit on the `ICSx⁵ forum <https://forums.bitfire.at/category/5/icsx>`_. A very obvious search of `google calendar sync` took me to this short `thread <https://forums.bitfire.at/topic/872/google-calender-sync-correct-url>`_ of 5 replies. The summery of the thread is that once upon a time (before Nov 2015) Google supported CalDAV protocol that allowed users to sync calendar using ICSx⁵ but which is deprecated as they implemented a new CalDAV protocol that supports OAuth. ICSx⁵ can't sync with the new protocol. However, one user on the thread confirmed that old ways work if you replace your calendar id with you email address and as the new protocol requires OAuth you need an App Password.

So I head over to `App Password page <https://myaccount.google.com/apppasswords>`_ and generated an app password. Opening the ICSx⁵ app, I tap on the red plus('+') button on the bottom right and put the URL the way it was suggested on the thread, toggle the ``Requires Authentication`` button to reveal the user name and password input filed, put the username and the app password. Now we click on the right arrow (':raw-html:`&rarr;`') button on the top right and wait for the app to validate the calendar resources and if everything goes all right the app takes us to the next page where we are asked to choose the Title and color for our app and when we are done with it tap the check mark(':raw-html:`&#10003;`') on the top right and we are done!

The suggested format on the thread `reply <https://forums.bitfire.at/topic/872/google-calender-sync-correct-url/5>`_ was::

    https://www.google.com/calendar/dav/{username}@{domain.tld}/events

The only lacking that is mentioned in the thread is that the delegates aka people on events are not synced. Please keep in mind that this end point is deprecated and we are using it at our own risk as it says on the `CalDAV API Developer's Guide page <https://developers.google.com/calendar/caldav/v2/guide#new_endpoint>`_

**UPDATE:** Just a few days after writing this, I saw this `comment <https://help.nextcloud.com/t/goodbye-google-sync-calendar-with-google-agenda/2372/12>`_ in the Nextcloud community forum where I found that for normal Google Account or on G Suite if it's allowed, we can get the ``Secret address in iCal format``, we can bypass all the steps and just put that address on ICSx⁵ app and continue. The Secret address already contains a API key so there is no need for OAuth. 

Source
------
- `google calender sync: correct url <https://forums.bitfire.at/topic/872/google-calender-sync-correct-url/5>`_
- `ICSx⁵ website <https://icsx5.bitfire.at/>`_
- `ICSx⁵ app on F-Droid <https://f-droid.org/en/packages/at.bitfire.icsdroid/>`_
- `CalDAV API Developer's Guide page <https://developers.google.com/calendar/caldav/v2/guide#new_endpoint>`_
- `[Goodbye Google] Sync calendar with google agenda <https://help.nextcloud.com/t/goodbye-google-sync-calendar-with-google-agenda/2372>`_
