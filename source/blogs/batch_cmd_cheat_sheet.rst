Batch and CMD Cheat Sheet
=========================
`< Blog <../blog.html>`_

A quick reference to Batch and CMD.

Created on: 2019-08-30

.. warning:: under heavy construction and not well organized


check if file exists
--------------------

add %cd%/ before file.name to get current location ie. pwd::


    if exist file.name (
        echo "file exists"
    ) else (
        echo "file doesn't exist"
    )

Username
--------
::

    echo %USERNAME%

Domainname
----------
::

    echo %USERDOMAIN%

run 'set' to see the full list

delete folder with sub-folder
-----------------------------
::

    rmdir /S /Q "path\to\folder" :: /Q for quiet mode /S for sub-folder

run .bat file form .bat file
----------------------------
::

    call "file.bat"

delete file
-----------
::

    del /Q "path\to\folder" :: /Q for quiet mode

downlaod file (PowerShell 2.0)
------------------------------
::

    (New-Object Net.WebClient).DownloadFile('http://www.foo.com/package.zip', 'package.zip')

call PowerShell form Batch file
-------------------------------
::

    powershell -Command "powershell_command"

donwloading a file from batch file using PowerShell
---------------------------------------------------
::

    powershell -Command "(New-Object Net.WebClient).DownloadFile('https://download.url', 'path\to\save\with\file.extension')"

delete all with cygwin
----------------------
::

    takeown /f "DRIVE:\cygwin" /r /d Y

unrar .rar file (must have unRAR.exe in the same location of .bat file)
-----------------------------------------------------------------------
::

    unrar x "%rar_loc%" "%ext_loc%"

create shortcut (must have shortcut.exe in the same location of .bat file)
--------------------------------------------------------------------------
::

    shortcut /a:c /f:"path/to/destination.lnk" /t:"path/to/source.extension"

Extract an 7zip SFX archive
----------------------------
(source:http://stackoverflow.com/a/32105548/5350059)
::

    sfx.exe -y -gm2 -InstallPath="C:\\your\\target\\path"
    can also extract sfx.7z.exe

kill a task
-----------
::

    Taskkill /IM application_name.exe /F

get folder name from folder path
--------------------------------
::

    set loc= \path\to\folder
    for %%f in (%loc%) do set output=%%~nxf
    ::output gives the folder name
    echo %output%

list all dirve in windows and some more info
--------------------------------------------
::

    wmic logicaldisk get caption,providername,drivetype,volumename

get drive letter from file path (i.e. C:,D:)
--------------------------------------------
::

    set script_path=C:\all\ball
    set script_drive=%CD:~0,3%
    echo %script_drive%

# note if 2 is used in place of 1 we get C:

change drive
------------
::

    chdir /d %drive_letter%:

store the output of a command in a variable (replace %%i with %i while in cmd)
------------------------------------------------------------------------------
::

    set cmd="%cmd%"
    for /f "tokens=*" %%i in (' %cmd% ') do set x=%%i

store the output of a command in a file
---------------------------------------
::

    command>output.txt

read file line by line
----------------------
::

    for /f "tokens=*" %%a in ('type "my file.txt"') do [process] %%a

set the value of %%a (special value used in for loop) in to %var%
-----------------------------------------------------------------
::

    set "var=%%a"

logout
------
::

    shutdown /l /f

unzip .zip with WinRar
----------------------
::

    WinRAR.exe x -ibck %app_name%.zip %folder_name%

(source: http://stackoverflow.com/a/19337595)

hide and unhide a user
----------------------
::

    ::hide
    net user hidden /active:no
    ::unhide
    net user hidden /active:yes

(source: http://www.wikihow.com/Create-and-Manage-a-Hidden-Account-in-Windows-7)


lock workstation
----------------
::

    rundll32.exe user32.dll,LockWorkStation

(source: http://winaero.com/blog/all-ways-to-lock-a-windows-10-pc/)

find the location of an executable (which alternative)
------------------------------------------------------
::

    cd \
    dir /s /b mytool.exe
    ::OR to find firefox on C:\
    where /R c:\ firefox.exe

(source: https://superuser.com/a/49107/655587)

read first line from text file
------------------------------
::

    set /p texte=< file.txt
    echo %texte%

(source: http://stackoverflow.com/a/7827243/5350059)

rename a file
-------------
::

    rename test.txt hope.txt

(source: https://www.computerhope.com/issues/ch000846.htm)

How to Restart Windows’ Explorer.exe (Along with the Taskbar and Start Menu)
----------------------------------------------------------------------------
::

    taskkill /f /IM explorer.exe
    start explorer.exe
    exit

(source: https://www.howtogeek.com/198815/use-this-secret-trick-to-close-and-restart-explorer.exe-in-windows/)

don't show command output to screen [dump to null]
--------------------------------------------------
::

    command >NUL

file sync
---------
::

    
    xcopy *.* C:\flashdrive1 /a (/a only copies files with the archive bit set, ie. those that have changed.)
    attrib -a /s (resets the archive bit. It is set when changes are made to a file.)

Source
------
 - ` <>`_
