Google calendar to ical conversation
====================================
`< Blog <../blog.html>`_

Converting Google calendar to ical format.

Created on: 2018-08-16

Google calendar URL for Sunrise and Sunset time in Dhaka::

    https://calendar.google.com/calendar/embed?src=i_117.103.85.142%23sunrise%40group.v.calendar.google.com&ctz=Asia%2FDhaka

The part after ``src=`` is the calendar id so for Sunrise and Sunset time calendar the calendar id is::

    i_117.103.85.142%23sunrise%40group.v.calendar.google.com

The part after ``&`` is additional parameter giving the time zone which is Asia, Dhaka.

A generic ical for Google calendar is the following::

    https://calendar.google.com/calendar/ical/$calendar_id/public/basic.ics

So to transform the Sunrise and Sunset time calendar into a ical replace the calendar_id and we get::

    https://calendar.google.com/calendar/ical/i_117.103.85.142%23sunrise%40group.v.calendar.google.com/public/basic.ics


