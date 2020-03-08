Miscellaneous Cheat Sheet
=========================
`< Blog <../blog.html>`_

A quick reference to all things miscellaneous and those things that have no home yet.

Created on: 2020-02-09


HTML: jump to top of page link
------------------------------
to create a jump to top of page link::

    <a href="#">Go to top</a>

    <a href="#top">Go to top</a>

source: https://stackoverflow.com/a/11751756
 

Linux: best place to store SSL certificate and key
--------------------------------------------------
store SSL certificate inside::

    /etc/ssl/certs

with `777` file permission.

store SSL key inside::

    /etc/ssl/private

with `700` file permission.

source: https://stackoverflow.com/a/4267602

QR Code: Bangladesh Railway Online Ticket
-----------------------------------------
If we scan it, we see::

    TRAIN: NELSAGORE_EXPRESS (765.)     // train name and number
    STATION: DHAKA to ABDULPUR          // source station to distination station
    DATE: 01-JAN-1001 08:00             // date and time of train diperture from source station
    CLASS: S_CHAIR                      // seat class
    COACH_NO: CHA                       // coach number
    SEAT_RANGE: 1,2                     // seat number
    E-PIN: 6NZ95                        // e-pin number
    FULL NAME: Jane Doe                 // name of passenger
    MOBILE_NO: 01704522104              // phone number of passenger
    PNR_NO: 1704522104                  // not sure what is it
    ID: 1382533015                      // ID of user
    GATEWAY: EBL_BANK                   // bank with what the payment was made


QR Code: Dhaka University Masters Admit
---------------------------------------
If we scan it, we see::

    DU-ADMT<<<1001822312<<REF<<19966095654<<Regular<<62867<<<
                   ^                ^          ^       ^
                   |                |          |       |
             registration       referance    type     roll
             number like:         number      of     number
             1001-822-312                   student
              ^
              |
        registration
           year!?


QR Code: Nextcloud App Password
-------------------------------
If we scan it, we see::

    nc://login/user:$USER-NAME&password:$PASSWORD&server:$PROTOCOL://URL:$PORT-IF-ANY



VeraCrypt: mount volume from command line
-----------------------------------------
to mount a VeraCrypt volume from command line::

    veracrypt -t --mount /dev/sdb1 --non-interactive --stdin

This will be stuck on a blank line. Typing the volume password would mount the volume. The `-t` flag is for **text user interface**, the `--mount` flag **mounts volume interactively** which takes a device path as argument, `--non-interactive` flag **disabals user interaction** and finally the `--stdin` flag **reads password from standard input**.

source: https://www.veracrypt.fr/en/Command%20Line%20Usage.html. Thought not all options are document there and needed to be look at the `veracrypt -t --help`. 

VeraCrypt: unmount volume from command line
-------------------------------------------
to unmount a VeraCrypt volume from command line::

    veracrypt -d

The `-d` flag **dismounts volume**.

source: https://www.veracrypt.fr/en/Command%20Line%20Usage.html

VeraCrypt: list volume from command line
----------------------------------------
to list VeraCrypt volume(s) from command line::

    veracrypt -l

The `-l` flag **displays a list of mounted volumes**.

source: `veracrypt -t --help` options.

Source
------

