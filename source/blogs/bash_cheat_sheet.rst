This file contains commands and scripts that I have collected form veroius place
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Login with sshpass
==================

::

    sshpass -p 'your_password' ssh user@host_ip

Show line number in nano for 'filename'
=======================================

::

    #Show while opening file
    nano -c [filename]
    #Show always
    nano ~/.nanorc
    #don't worry if its empty - this file doesn't exist by default
    set const
    #save

Record your encryption passphrase in Ubuntu
===========================================

::

    ecryptfs-unwrap-passphrase

See USB information in Linux Terminal
=====================================

::

    user@user-pc:~$ lsusb 
    // open terminal and type lsusb
    user@user-pc:~$ Bus #bus_number Device #device_number: ID #vendor:#product USB_Name 
    //output of command 'lsusb' including your expected device
    user@user-pc:~$ lsusb -D /dev/bus/usb/#bus_number/#device_number 
    //replace the #bus_number and #device_number of you expected device

Shell script to install application(s) in Ubuntu
================================================

method 01
=========

::

    #!/bin/sh
    apt-get update  # To get the latest package lists
    apt-get install <package name> -y #apt-get install <package name> -y 
    #etc.

method 02
=========

::

    #!/bin/sh
    LIST_OF_APPS="a b c d e"
    aptitude update
    aptitude install -y $LIST_OF_APPS

method 03
=========

::

    cat example.list | xargs sudo apt-get -y install

method 04
=========

::

    #!/bin/bash
    apt-get update  # To get the latest package lists
    apt-get install $1 -y

Connect to wifi from terminal
=============================

List all the wifi
=================

::

    nmcli dev wifi

connect to wifi
===============

::

    nmcli dev wifi connect $SSID password $PASS

Get a spcecifice column form output
===================================

::

    command | awk '{print $n}' #n is the number of column

Get a spcecifice row column output
==================================

::

    command | awk 'FNR == row {print $column}' #row is row/line number and column is column number 

Source:https://www.quora.com/What-are-some-funny-Linux-commands
===============================================================

make
====

::

    make LOVE=war

rev: reverse char of a line in a file
=====================================

::

    rev <file> # if file contains 12 shows 21

fortune #sudo apt-get innstall fortune
======================================

fortune will display some random sentence
=========================================

::

    fortune

yes command will keep displaying the string for infinite until the process is killed by the user.
=================================================================================================

::

    yes yes

figlet command can be installed with apt-get, comes with some ascii
fonts which are located in /usr/share/figlet. cd /usr/share/figlet
figlet -f Ex: figlet -f big.flf unixmen

asciiquarium command will transform your terminal in to a Sea Aquarium
======================================================================

::

    search Term-Animation in http://www.cpan.org/authors/id/K/KB/KBAUCOM/

bb
==

::

    apt-get install bb 
    bb

comment or uncomment ie. append before line using sed
=====================================================

::

    sed -i 'start_line,end_line s/char_to_be_replaced/replacing_char/' file_name 
    #use ^ as char_to_be_replaced for unknown char_to_be_replaced

lock screen
===========

#gnome gnome-screensaver-command -l #xfce xflock4

show notification in linux
==========================

::

    #must have libnotify for notify-send
    #install libnotify
    sudo apt-get install libnotify-bin
    #install notify-send
    sudo apt-get install notify-osd
    DISPLAY=:0.0 /usr/bin/notify-send "title" "Message"

notification at a specific
==========================

::

    echo 'notify-send "Work day is done!"' | at 4:00PM 
    echo 'notify-send "Get your tea!"' | at now + 3 minutes 
    echo 'notify-send "Meeting in 1 hour with the big boss!"' | at 1pm tomorrow 

Mute the microphone
===================

::

    amixer set Capture nocap

Unmute the microphone
=====================

::

    amixer set Capture cap

chnage background picture
=========================

::

    #gnome
    gsettings set org.gnome.desktop.background picture-uri "file:///location/file.extension"

chnage avatar (must be png)
===========================

::

    sudo cp /path/to/file /var/lib/AccountsService/icons/$(whoami)

append line before pattern in file
==================================

::

    sed -i '/find this pattern/i \append pattern' /path/to/file.extension

delete specific line in file (creates a .bak file of same name)
===============================================================

::

    sudo sed -i.bak -e '{line_number}d' /path/to/file.extension 

stopwatch and countdown timer function (source: http://superuser.com/a/611582)
==============================================================================

::

    countdown(){
        date1=$((`date +%s` + $1));
        while [ "$date1" -ge `date +%s` ]; do 
        ## Is this more than 24h away?
        days=$(($(($(( $date1 - $(date +%s))) * 1 ))/86400))
        echo -ne "$days day(s) and $(date -u --date @$(($date1 - `date +%s`)) +%H:%M:%S)\r"; 
        sleep 0.1
        done
    }
    stopwatch(){
        date1=`date +%s`; 
        while true; do 
        days=$(( $(($(date +%s) - date1)) / 86400 ))
        echo -ne "$days day(s) and $(date -u --date @$((`date +%s` - $date1)) +%H:%M:%S)\r";
        sleep 0.1
        done
    }

using rsync to mirror
=====================

::

    rsync -ar source/ destination

hide (all) user list on login screen (source: http://askubuntu.com/a/731455/502875)
===================================================================================

::

    sudo mkdir -p /etc/lightdm/lightdm.conf.d
    sudo printf "[SeatDefaults]\nuser-session=ubuntu\ngreeter-show-manual-login=true\ngreeter-hide-users=true\nall" > /etc/lightdm/lightdm.conf.d/10-ubuntu.conf

hide a specific user form login screen (source: http://askubuntu.com/a/575390/502875)
=====================================================================================

::

    touch $user_name
    printf "[User]\nSystemAccount=true\n" > $user_name
    sudo mv $user_name /var/lib/AccountsService/users/$user_name

hide user from gear button
==========================

::

    gsettings set com.canonical.indicator.session user-show-menu false

open files form terminal
========================

::

    #Ubuntu
    nautilus .

save command output in vaiable
==============================

::

    OUTPUT="$(ls -1)"
    echo "${OUTPUT}"

see execution time of a command
===============================

::

    time command
    #for getting real time only
    /usr/bin/time -f "%e" command
    #save the command execution time in a variable
    down_time=`/usr/bin/time -f %e sleep 2 2>&1`

echo in red color (source: http://stackoverflow.com/a/28938235/5350059)
=======================================================================

::

    echo -e "\e[31m{message to echo with out 2nd brackets}\e[0m"

run a terminal-lunched program after closing terminal (by removing it form job list)
====================================================================================

::

    app_name & disown

run script at startup (source: )
================================

delete last char of string
==========================

::

    #with bash 4.2
    a=123
    echo "${a::-1}"
    12

    #older bash
    a=123
    echo "${a: : -1}"
    12

open chrome using crontab (as because cron can do terminal jobs only we need to export DISPLAY for GUI)
=======================================================================================================

::

    export DISPLAY=:0
    /opt/google/chrome/chrome $URL

Get current directory name (without full path)
==============================================

::

    dir="$(pwd | grep -o '[^/]*$')"

stop max brightness on restart (source: http://askubuntu.com/a/151665/502875)
=============================================================================

::

    sudo -v
    #get directory name
    cd /sys/class/backlight/*/ && dir="$(pwd | grep -o '[^/]*$')"
    #the following line added the given pattern twice as there is a exit 0 in the comment section, delete it mannualy
    #250 is the number of brightness level
    sudo sed -i "/exit 0/i \echo 250 > /sys/class/backlight/$dir/brightness" /etc/rc.local

Execute a command in the background using '&' and killing it
============================================================

::

    ./my-shell-script.sh & #execute command in background

    jobs #see jobs
    [1]+  Running        my-shell-script.sh #sample output

    kill %1 #kill with the number in [n]+ recived from jobs

    jobs #see jobs
    [1]+  Terminated    ./my-shell-script.sh #sample output

Press Enter to continue
=======================

::

    read -p "Press Enter to continue"

Print one line and save it in a variable
========================================

::

    var1="$(head -n 1 file | tail -n 1)" #save line 1 on in var1
    var2="$(head -n 2 file | tail -n 1)" #save line 2 on in var2

Replace whole line containing a string using sed
================================================

::

    sed -i '/replace this/c\with this' /tmp/foo

terminal based lan cat
======================

::

    pc1: nc -l $port
    pc2: nc $IP $port 

open a terminal and execute shell on that terminal using crontab
================================================================

::

    export DISPLAY=:0 && /usr/bin/gnome-termina -e /path/to/script

display network traffic in terminal
===================================

::

    tcpdump -i $interface #(i.e. eth0,wlan0)
    #OR
    netstat -tnp
    #OR
    sudo watch -n1 netstat -tunap

assign to interface
===================

::

    sudo ip ad add $ip/$subnet dev $interface
    i.e.
    sudo ip ad add 10.0.0.10/24 dev eth0

connect two pc over crossover cable
===================================

::

    #on pc 1
    sudo ip ad add 10.0.0.10/24 dev eth0
    #on pc 2
    sudo ip ad add 10.0.0.20/24 dev eth0

remove the switch user account option in Unity
==============================================

::

    gsettings set com.canonical.indicator.session user-show-menu false

recursively list all files in a directory (source: http://stackoverflow.com/a/105249/5350059)
=============================================================================================

::

    ls -LR
    #OR
    find -follow

always show menu items in Unity
===============================

::

    #switch on:
    gsettings set com.canonical.Unity always-show-menus true
    #switch off:
    gsettings set com.canonical.Unity always-show-menus false

check battery status
====================

::

    upower -i $(upower -e | grep 'BAT') | grep -E "state|to\ full|percentage"
    #OR
    cat /proc/acpi/battery/BAT0/info
    #OR
    cat /proc/acpi/battery/BAT0/state

schedule jobs with cron
=======================

::

    corntab -e #run jobs for user
    sudo corntab -e #run jobs for root user

show jobs schedule with cron
============================

::

    corntab -l #show jobs for user
    sudo corntab -e #show jobs for root user

change bluetooth broadcast device name (source: http://askubuntu.com/a/80963/502875)
====================================================================================

::

        sudo echo "PRETTY_HOSTNAME=$device_name" >>/etc/machine-info
        sudo service bluetooth restart
        #OR (source: http://askubuntu.com/a/80964/502875)
        sudo hciconfig hci0 name '$device_name'
        

change LCD brightness (source: http://askubuntu.com/a/149264/502875)
====================================================================

::

    display="$(xrandr -q | grep " connected" | awk '{print $1}')"
    xrandr --output $display --brightness m.n #(0<=m<=10(tested can be greater),0<=m<=9 )

export display (to run a GUI of a program in remote client like over ssh)
=========================================================================

::

    export DISPLAY=:0 && program command

read specific line (source: http://stackoverflow.com/a/19327690/5350059)
========================================================================

::

    sed '$line_number!d' file_name

read file from line x to the end of a file (read from specific line) (source: http://stackoverflow.com/a/14110529/5350059)
==========================================================================================================================

::

    linesToSkip=1

{ for ((i=$linesToSkip;i--;)) ;do read done while read line ;do echo
$line done } < file.csv

copy all except one file or folder (idea source: http://askubuntu.com/a/786613/502875 & http://stackoverflow.com/a/27655311/5350059)
====================================================================================================================================

::

    shopt -s extglob && cp source\!($name) \destination #(first part extends regexes)

split string to array using awk (source: http://stackoverflow.com/a/8009724/5350059)
====================================================================================

::

    echo "12|23|11" | awk '{split($0,a,"|"); print a[3],a[2],a[1]}'

get date in yyy-mm-dd format (source: http://stackoverflow.com/a/1401495/5350059)
=================================================================================

::

    DATE=`date +%Y-%m-%d`

in ubuntu all .deb file ar in this folder (source: )
====================================================

::

    /var/cache/apt/archives

install all .deb (source: )
===========================

::

    sudo dpkg -i *.deb #(* for all)

Encrypting and compressing with 7z (source: http://unix.stackexchange.com/a/325783/199183)
==========================================================================================

::

    7z a -p stuff.7z MyStuff
       ^  ^    ^        ^
       |  |    |        `--- Files/directories to compress & encrypt.
       |  |    `--- Output filename
       |  `---- Use a password
       `---- Add files to archive

read on same line after echoing a message (source: http://stackoverflow.com/a/9720209/5350059)
==============================================================================================

::

    read -p "[y/n]: " opt (#saves value in opt variable)

Additional Workspaces in Gnome (source: http://askubuntu.com/a/370048/502875)
=============================================================================

::

    #get n workspaces vertically
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ vsize n
    #get n workspaces horizontally
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ hsize n

remove Workspace Switcher launcher icon from the Unity launcher (source: https://askubuntu.com/a/286344/502875)
===============================================================================================================

::

    gsettings get com.canonical.Unity.Launcher favorites
    #should returen something like
    #['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://expo-icon', 'unity://devices']
    #copy the whole string and remove 'unity://expo-icon' and give the following command, don't forget the ""
    gsettings set com.canonical.Unity.Launcher favorites "['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://devices']"

split a string on a delimiter (source: http://stackoverflow.com/a/38905821/5350059)
===================================================================================

::

    string="1;2"
    echo $string | cut -d';' -f1 # output is 1
    echo $string | cut -d';' -f2 # output is 2

bluetooth tool
==============

::

    hcitool

clear screen (source: http://stackoverflow.com/a/5367075/5350059)
=================================================================

::

    printf "\033c"

(source: https://www.quora.com/What-are-the-best-Linux-Terminal-hacks-that-you-can-learn-in-10-seconds)
=======================================================================================================

::

    #see wather in terminal 
    curl http://wttr.in/$name_of_city

    #Increase the maximum volume of your speakers by a certain percentage (150 in this case)
    pactl set-sink-volume 0 150%

    #Scroll Lock toggle
    xmodmap -e 'add mod3 = Scroll_Lock' link 

    #opens any file directly from terminal in the default application
    Xdg-open file/link

    #run a command you ran yesterday at a point of time
    ctrl+r #(mod command using ctrl+a, ctrl+e, ctrl+left, ctrl+right)

    #list files only in current folder/path
    ls -p | grep -v /

    #list directory only in current folder/path
    ls -d */

    #run your last used command
    !!

    #Delete word by word from the terminal
    alt+backspace

    #see all input device
    xinput list
    #disable input device (see form "xinput list" command output id column)
    xinput set-prop $id "Device Enabled" 0
    #enable input device (see form "xinput list" command output id column)
    xinput set-prop $id "Device Enabled" 1
    #if mouse found in usb dieable touchpad see github Code.random

reboot alsamixer (source: unknown)
==================================

::

    sudo alsa force-reload

deleting a substring (source: http://stackoverflow.com/a/13570430/5350059)
==========================================================================

str=abc.out #Shell: echo ${str%.\*}

::

    #Grep:
    echo $str | grep -o '^[^\.]*'

    #Sed:
    echo $str | sed -E 's/(.*?)\..*/\1/'

    #Awk:
    echo $str | awk -F. '{print $1}'

    #Cut:
    echo $str | cut -d. -f1

    #All output:
    abc

split a sting with OIFS (source: http://stackoverflow.com/q/918886/5350059)
===========================================================================

::

    IN="bla@some.com;john@home.com"
    OIFS=$IFS
    IFS=';'
    mails2=$IN
    for x in $mails2
    do
        echo "> [$x]"
    done
    IFS=$OIFS

download YouTube video with youtube-dl (source: )
=================================================

::

    youtube-dl  --sub-lang en --sub-format srt --batch-file youtube_url.txt

shutdown, restart, without sudo from terminal (source: http://askubuntu.com/a/385316/502875) [munst have consolekit]
====================================================================================================================

#Ubuntu 14.04 or earlier: #shutdown: /usr/bin/dbus-send --system
--print-reply --dest="org.freedesktop.ConsoleKit"
/org/freedesktop/ConsoleKit/Manager
org.freedesktop.ConsoleKit.Manager.Stop #restart: /usr/bin/dbus-send
--system --print-reply --dest="org.freedesktop.ConsoleKit"
/org/freedesktop/ConsoleKit/Manager
org.freedesktop.ConsoleKit.Manager.Restart #suspend: /usr/bin/dbus-send
--system --print-reply --dest="org.freedesktop.UPower"
/org/freedesktop/UPower org.freedesktop.UPower.Suspend #hibernate: (if
enabled on your system) /usr/bin/dbus-send --system --print-reply
--dest="org.freedesktop.UPower" /org/freedesktop/UPower
org.freedesktop.UPower.Hibernate #Ubuntu 15.04 and later: systemctl
poweroff/reboot/suspend/hibernate/hybrid-sleep

run applications as root (source: http://askubuntu.com/a/207467/502875)
=======================================================================

::

    #console
    sudo <program name>
    #GUI
    gksudo <program name>

if string is not empty (source: http://stackoverflow.com/a/6592241/5350059)
===========================================================================

::

    if [ ! -z "$string" ]
    #OR
    if [[ ! -z $string ]]

if else if elif (source: https://www.tutorialspoint.com/unix/if-elif-statement.htm)
===================================================================================

::

    f [ expression 1 ]
    then
       Statement(s) to be executed if expression 1 is true
    elif [ expression 2 ]
    then
       Statement(s) to be executed if expression 2 is true
    else
       Statement(s) to be executed if no expression is true
    fi

if a application exist (source: )
=================================

::

    e=$(which $app_name)
    if [[ ! -z "$e" ]]
    then
        echo -e "\e[32mApplication exist.\e[0m"
    else
        echo -e "\e[31mApplication doens't exist!!!\e[0m"
    fi

if string is equal to string (source: http://stackoverflow.com/a/10849346/5350059)
==================================================================================

::

    string="ABC"
    if [ "$string" = "XYZ" ]; then 
        echo "string matched" 
    else
        echo "string mismatched"  
    fi;

insert line number in file (source: http://www.unix.com/shell-programming-and-scripting/99016-how-add-line-numbers-text-file.html)
==================================================================================================================================

::

    cat -n inputfile > result
    #OR
    nl infile
    #OR
    nl -w1 -s.\  infile
    #OR
    cat <inputfile> | grep -n '' > <outputfile>

get number of line in a file (source: )
=======================================

::

     wc -l file.txt | awk '{print $1}'
     #OR
     wc -l < file.txt
     

division with variables (source: http://stackoverflow.com/a/18093887/5350059)
=============================================================================

::

    z=$((x / y))

use specific app through ssh (source: http://tiny.cc/i04fjy)
============================================================

::

    ssh -X username@xxx.xxx.xxx.xxx
    nohup $app_name &

detect line break (source: http://unix.stackexchange.com/q/27423/199183)
========================================================================

::

    if [[ "$a" == '\012' ]] ; then
                echo "FOUND NEWLINE"
        fi

kill a shell form that shell (source: )
=======================================

::

    kill $$

get file name from file path (source: http://stackoverflow.com/a/4645575/5350059)
=================================================================================

::

    file_path=/path/to/file.extension
    file=$(basename "$file_path")
    echo "$file"

replace char with another char (source: http://unix.stackexchange.com/a/159369/199183)
======================================================================================

::

    sed -ie 's/char/achar/g' /path/to/hello.txt #replacing char with achar

Ubunut side panel pin or favourite (source: http://askubuntu.com/a/171723/502875)
=================================================================================

::

    #remove all pin
    gsettings set com.canonical.Unity.Launcher favorites "[]"
    #pin allpication
    gsettings set com.canonical.Unity.Launcher favorites "['application://firefox.desktop', 'unity://running-apps', 'application://evolution.desktop', 'unity://devices']"
    #get pin item
    gsettings get com.canonical.Unity.Launcher favorites

add bookmark in nautilus (source: https://ubuntuforums.org/showthread.php?t=1736534)
====================================================================================

::

    echo "location_path $name_of_bookmark" >> ~/.gtk-bookmarks

kill a application (source: )
=============================

::

    e="$(ps ax | grep $app | awk '{print $1}')"
    kill $e

speaker test (source: http://unix.stackexchange.com/a/163716)
=============================================================

::

    speaker-test -t sine -f 1000 -l 1

convert to lowercase (source: http://stackoverflow.com/a/2264537/5350059)
=========================================================================

::

    var= "HI ALL"
    low=$(echo "$var" | tr '[:upper:]' '[:lower:]')
    low=$(echo "$var" | awk '{print tolower($0)}')
    #both produces "hi all"

get real ip (source: http://sh.howtocode.com.bd/3.4.3.secure-connection.html)
=============================================================================

::

    curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'

run .sh file by double clicking on them
=======================================

::

    #using gsettings (source: http://askubuntu.com/a/378473/502875)
    gsettings set org.gnome.nautilus.preferences executable-text-activation ask
    #using dconf (source: http://askubuntu.com/a/421537/502875)
    dconf write /org/gnome/nautilus/preferences/executable-text-activation "'launch'"

change password without typing non interactive (source: http://stackoverflow.com/a/41223440/5350059)
====================================================================================================

::

    echo $uname:$passwd | sudo chpasswd

delete script after execution (source: http://stackoverflow.com/a/8981233/5350059)
==================================================================================

::

    #add at the end of script
    rm -- "$0"
    #OR
    rm $script_name 

unzip .zip (source: http://askubuntu.com/a/86852/502875)
========================================================

::

    unzip file.zip -d destination_folder

go to each sub directory and execute a command (source: http://unix.stackexchange.com/a/171679/199183)
======================================================================================================

::

    for d in ./*/ ; do (cd "$d" && somecommand); done

refresh output in the same line; echo update (source: http://stackoverflow.com/a/34466100/5350059)
==================================================================================================

::

    echo -e "\e[1A" # moving the cursor back to the previously printed line
    echo -ne "$line\e[K" # \e[K cleans the residues of the previous output.
    #example:
    #!/bin/bash
    arr=(12 11 10 9 8 7 6 5 4 3 2 1 0)
    for i in ${arr[@]}
    do
        echo -e "\e[1A"
        sleep 1s;
        echo -ne "Waiting time : "$i" Seconds\e[K"
    done
    echo #print new line

go back to previous directory (source: https://superuser.com/q/113219/655587)
=============================================================================

::

    cd -

rm move to trash (source: https://unix.stackexchange.com/a/42758/199183)
========================================================================

::

    #in .bashrc
    #start by defining a move_to_trash function:
    move_to_trash () {
        mv "$@" /path/to/trash #/home/$USER/.local/share/Trash/files
    }
    #then alias rm to that:
    alias rm='move_to_trash'

use pc name instead of ip while ssh (source: https://askubuntu.com/a/487319/502875)
===================================================================================

::

    #add at the end of /etc/hosts
    ip_address(tab)pc_name

Add an application to the Ubuntu dashboard (source: https://askubuntu.com/a/112812)
===================================================================================

::

    nano ~/.local/share/applications/your_application_name.desktop
    #file contains 
    [Desktop Entry]
    Name=the name you want shown
    Comment=
    Exec=command to run or app executable location
    Icon=icon name
    Terminal=false
    Type=Application
    StartupNotify=true

disable and enable mouse driver (source: https://askubuntu.com/a/697952/502875)
===============================================================================

::

    sudo modprobe -r psmouse  # disable the driver
    sudo modprobe psmouse # enable the mouse driver

list all users and groups (source: https://serverfault.com/a/355294)
====================================================================

::

    getent passwd #user
    getent group #group

turn off bluetooth on startup ubuntu (source: https://itsfoss.com/turn-off-bluetooth-by-default-in-ubuntu-14-04/)
=================================================================================================================

::

    #the following line added the given pattern twice as there is a exit 0 in the comment section, delete it mannualy
    sudo sed -i '/exit 0/i \rfkill block bluetooth' /etc/rc.local

check if user is sudo if not ask for password (source: https://superuser.com/a/553939/655587)
=============================================================================================

::

    sudo -v

add, sub, multiply and devide (source: https://stackoverflow.com/a/11039905
===========================================================================

::

    swap_size="$(($ram * $size_choice))"

echo is system file (source: https://ubuntuforums.org/showthread.php?t=978334)
==============================================================================

::

    echo "line to be added" | sudo tee -a /etc/fstab

missing date & time from top panel (source: https://askubuntu.com/a/462176/502875)
==================================================================================

::

    dconf reset -f /com/canonical/indicator/datetime/
    pkill -f datetime

spell checking in vim (source: https://www.linux.com/learn/using-spell-checking-vim)
====================================================================================

::

    #while editing on vim
    :set spell spelllang=en_us
    #
    echo "set spell spelllang=en_us" >> ~/.vimrc #chnage en_us to any language you want 

compare two file and get the diff (source: https://stackoverflow.com/a/4546712)
===============================================================================

::

    comm -2 -3 <(sort file1) <(sort file2) > file3 #here we will redrict the output to file3

remove a fixed prefix/suffix from a strin or delete string from string (source: https://stackoverflow.com/a/16623897)
=====================================================================================================================

::

    string="hello-world"
    prefix="hell"
    suffix="ld"
    foo=${string#$prefix}
    foo=${foo%$suffix}
    echo "${foo}" #o-wor

if file exists (source: https://stackoverflow.com/a/40082454)
=============================================================

::

    if [ -e x.txt ]
    then
        echo "ok"
    else
        echo "not ok"
    fi

read file line by line (source: https://stackoverflow.com/a/10929955)
=====================================================================

::

    filename="$1"
    while read -r line
    do
            echo $line
    done < "$filename"

if a sub string is part of string (source: https://stackoverflow.com/a/229606)
==============================================================================

::

    string='My long string'
    if [[ $string == *"My long"* ]]; then
        echo "It's there!"
    fi

generate a random filename in unix shell (source: https://stackoverflow.com/a/2793856)
======================================================================================

::

    # generates a srting consisting of alpha(a-z) and num(0-9) of 32 char
    cat /dev/urandom | tr -cd 'a-f0-9' | head -c 32 

using a git command inside a cron job while using ssh key (source: https://stackoverflow.com/a/16580506)
========================================================================================================

::

    #add those line at the top of script
    export SSH_AGENT_PID=`ps -a | grep ssh-agent | grep -o -e [0-9][0-9][0-9][0-9]`
    export SSH_AUTH_SOCK=`find /tmp/ -path '*keyring-*' -name '*ssh*' -print 2>/dev/null` 

crontab log (source: https://askubuntu.com/a/56811)
===================================================

::

     grep CRON /var/log/syslog

using git commands in shell script (source: https://unix.stackexchange.com/a/226678)
====================================================================================

::

    #!/bin/sh
    GIT=`which git`
    REPO_DIR=/home/username/Sites/git/repo/
    cd ${REPO_DIR}
    ${GIT} add --all .
    ${GIT} commit -m "Test commit"
    ${GIT} push git@bitbucket.org:username/repo.git master

numbers of line in a commands output (source: )
===============================================

::

    ps aux | grep "docker" | wc -l

backup and restore crontab (source: http://www.roman10.net/2012/07/09/how-to-backup-crontab-settings/)
======================================================================================================

::

    #backup
    crontab -l > crontab_backup
    #restore
    crontab crontab_backup

execute command without keeping it in history (source: https://stackoverflow.com/a/33511637/5350059)
====================================================================================================

::

    command;history -d $(history 1)

get hostname from ip (source: https://askubuntu.com/a/205067/502875)
====================================================================

::

    nbtscan <ip> #install nbtscan sudo apt-get install nbtscan

connect to net using ethernet calbe if you have DHCP enabled (source: https://askubuntu.com/a/755263/502875)
============================================================================================================

::

    sudo dhclient eth0

chnage hostname in linux (source: https://askubuntu.com/a/87687/502875)
=======================================================================

::

    sudo hostname your-new-name #name shows after reboot

':math:`' comes instead of 'username@host:~`' [it happens because bash is not default shell] (source: https://unix.stackexchange.com/q/50264/199183)
====================================================================================================================================================

::

    sudo chsh <username> -s /bin/bash

if your .bashrc is lost (source: https://askubuntu.com/a/404428/502875 and me)
==============================================================================

::

    #normal user
    /bin/cp /etc/skel/.bashrc ~/
    #root
    cp /etc/bash.bashrc ~/.bashrc

show last octet of ip (source: me)
==================================

add to .bashrc
==============

ip=lo:$(ifconfig \| grep "inet " \| grep -v 127.0.0. \| awk '{print
:math:`2}' | cut -d . -f 4) ip=`\ (echo
":math:`ip" | tr '\n' '/') ip="`\ {ip::-1}"
PS1='\ :math:`{debian_chroot:+(`\ debian\_chroot)}[:raw-latex:`\0`33[01;32m]:raw-latex:`\u@`:raw-latex:`\h`($ip)[:raw-latex:`\0`33[00m]:[:raw-latex:`\0`33[01;34m]:raw-latex:`\w`[:raw-latex:`\0`33[00m]$
'

make video with image and audio (source: https://superuser.com/a/1041818/655587)
================================================================================

::

    ffmpeg -loop 1 -i image.jpg -i audio.AMR -c:v libx264 -tune stillimage -c:a aac -b:a 192k -pix_fmt yuv420p -shortest video.mp4

show ubuntu-support-status (source: unknown)
============================================

::

    ubuntu-support-status 

get all system if as html page (source: )
=========================================

::

    sudo lshw -html>sys.html

open a GUI app from terminal while keeping the terminal clean form log output (source: me)
==========================================================================================

$app 2>/dev/null & disown

nmap find all alive hostnames and IPs in LAN (source: https://serverfault.com/a/153779)
=======================================================================================

::

    nmap -sP first_3_octet.*

get curret IP if first interface is being used (source: me)
===========================================================

::

    ifconfig | grep "inet " | awk 'FNR == 1 {print $2}' | cut -d: -f2 #if first interface is not being used change the FNR == number of interface

get first 3 octet of network if first interface is being used(source: me)
=========================================================================

::

    ifconfig | grep "inet " | awk 'FNR == 1 {print $2}' | cut -d: -f2 | cut -d. -f1,2,3 #if first interface is not being used change the FNR == number of interface

convert a .pdf into .jpg [one-page-one-pic] (source: https://askubuntu.com/a/50180/502875)
==========================================================================================

::

    pdftoppm -jpeg raw-er-cowboyra.pdf prefix

make vim git default editor (source: https://stackoverflow.com/a/2596835/5350059)
=================================================================================

::

    git config --global core.editor "vim"

git file location linux (source: https://stackoverflow.com/a/23134785/5350059)
==============================================================================

::

    git config --global -e
    git config --system -e
    git config --local -e

git commit and push without output (source: https://stackoverflow.com/a/8943761/5350059)
========================================================================================

::

    git commit --quiet
    git push --quiet

suppress all output from a command (source: https://stackoverflow.com/a/617184/5350059)
=======================================================================================

::

    scriptname >/dev/null

make a dir with - in fornt of it (source: udemy.com/intro-to-bash-linux-command-line section:6 lecture:23)
==========================================================================================================

::

    touch -- -$folder_name

Standard streams (source: https://en.wikipedia.org/wiki/Standard\_streams)
==========================================================================

::

    stdin 0
    stdout 1
    stderr 2

see gup info (source: can't remember)
=====================================

::

    sudo lshw -C display

print contents of X events, all mouse, keyboard event event can be used to test other input device (source: https://linux.die.net/man/1/xev)
============================================================================================================================================

::

    xev

mute and unmute a microphone (source: https://askubuntu.com/a/337662/502875)
============================================================================

::

    #mute
    amixer set Capture nocap
    #unmute
    amixer set Capture cap

enabling and disabling Ethernet (source: https://askubuntu.com/a/739502/502875)
===============================================================================

::

    #enable
    sudo ip link set up eth0
    #disable
    sudo ip link set down eth0

delete lines containing a specific string (source: https://stackoverflow.com/a/5410784/5350059)
===============================================================================================

::

    sed -i '/pattern to match/d' ./infile

add a timestamp to script log? (source: https://serverfault.com/a/310648)
=========================================================================

::

    (date && script.sh) >> /var/log/logfile

run PHP from terminal (source: https://askubuntu.com/a/447254/502875)
=====================================================================

::

    php filename.php

wget show progress bar only (source: https://stackoverflow.com/a/29457649/5350059)
==================================================================================

::

    wget $url -q --show-progress

redirect output to multiple log files (source: https://unix.stackexchange.com/a/41249/199183)
=============================================================================================

::

    echo test | tee file1 file2 file3

single line sftp from terminal (source: https://stackoverflow.com/a/16723151/5350059)
=====================================================================================

::

    sftp username@hostname:remoteFileName localFileName

check if file exists on remote host with ssh (source: https://stackoverflow.com/a/12845254/5350059)
===================================================================================================

::

    if ssh $HOST stat $FILE_PATH \> /dev/null 2\>\&1
    then
        echo "File exists"
    else
        echo "File does not exist"
    fi

cleanest way to ssh and run multiple commandssource: https://stackoverflow.com/a/4412338/5350059)
=================================================================================================

::

    ssh otherhost << EOF
      ls some_folder; 
      ./someaction.sh 'some params'
      pwd
      ./some_other_action 'other params'
    EOF

passing variables in remote ssh command (source: https://stackoverflow.com/a/3314678/5350059)
=============================================================================================

::

    ssh pvt@192.168.1.133 "~/tools/run_pvt.pl $BUILD_NUMBER"

git remote add with other SSH port (source: https://stackoverflow.com/a/3596272/5350059)
========================================================================================

::

    git remote add origin ssh://user@host:1234/srv/git/example

whether or not a variable is empty (source: https://stackoverflow.com/a/3063887/5350059)
========================================================================================

::

    if [[ -z "$var" ]]

debug a bash script (source: https://unix.stackexchange.com/a/155570/199183)
============================================================================

::

    set -x
    ..code to debug...
    set +x

get the current branch name in git (source: https://stackoverflow.com/a/46798693/5350059)
=========================================================================================

::

    git rev-parse --abbrev-ref HEAD | grep -v ^HEAD$ || git rev-parse HEAD

lock and unlock screen over ssh (source: https://z-computer-z.blogspot.com/2010/01/remote-lock-screen-and-remote-unlock.html)
=============================================================================================================================

::

    #this is for gnome
    ssh -X user@server "export DISPLAY=:0; gnome-screensaver-command -l"

shell access on a docker container (source: https://askubuntu.com/a/507009/502875)
==================================================================================

::

    sudo docker exec -i -t 665b4a1e17b6 /bin/bash #by ID
    #OR
    sudo docker exec -i -t loving_heisenberg /bin/bash #by Name

delete the first 5 chars on any line with sed (source: https://stackoverflow.com/a/3806107/5350059)
===================================================================================================

::

    sed 's/^.....//'

getting WiFi network details in Raspberry Pi (source: https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)
=======================================================================================================================================

::

    sudo iwlist wlan0 scan

getting WiFi network details in Raspberry Pi (source: https://raspberrypi.stackexchange.com/a/41024)
====================================================================================================

::

    iwgetid

disallow peter from logging in (source: https://askubuntu.com/a/607108/502875)
==============================================================================

::

    sudo usermod --expiredate 1 peter

set expiration date of peter to Never (source: https://askubuntu.com/a/607108/502875)
=====================================================================================

::

    sudo usermod --expiredate "" peter

take away peters password (source: https://askubuntu.com/a/607108/502875)
=========================================================================

::

    sudo passwd -l peter

give peter back his password (source: https://askubuntu.com/a/607108/502875)
============================================================================

::

    sudo passwd -u peter

make peter think of a new password on login (source: https://askubuntu.com/a/607108/502875)
===========================================================================================

::

    sudo passwd -e  YYYY-MM-DD peter

check if directory is git repository without having to cd into it (source: https://stackoverflow.com/a/39518382/5350059)
========================================================================================================================

::

    git -C $dir_path rev-parse

set static ip (source: https://askubuntu.com/a/470245/502875)
=============================================================

::

    #edit /etc/network/interfaces and put the following there, don't forget to change $interface and address, netmask, network, gateway and dns
    auto $interface
    iface $interface inet static
       address 10.253.0.50
       netmask 255.255.255.0
       network 10.253.0.0
       gateway 10.253.0.1
       dns-nameservers 8.8.8.8

show files only (source: https://askubuntu.com/questions/811210/how-can-i-make-ls-only-display-files#811236)
============================================================================================================

::

    ls -p | grep -v /

adb backup (source: https://www.technipages.com/how-to-backup-your-entire-android-device)
=========================================================================================

::

    adb backup full.package.name -f file_name.ab
    ie. backing up FreeOTP
    adb backup org.fedorahosted.freeotp -f freeotp.ab

more resources: 1.
https://stackpointer.io/mobile/android-adb-backup-extract-restore-repack/372/
2. https://forum.xda-developers.com/showthread.php?t=2011811

execute sudo command over ssh (source: https://stackoverflow.com/a/10312700/5350059)
====================================================================================

::

    ssh -t user@server "sudo script"

see port address and PID (source: )
===================================

::

    netstat -tulpn

check curl and install if not found
===================================

if command -v curl > /dev/null then echo "Detected curl..." else echo
"Installing curl..." apt-get install -q -y curl fi

special dollar sign shell variables (source: https://stackoverflow.com/a/5163260)
=================================================================================

::

    $1, $2, $3, ... are the positional parameters.
    "$@" is an array-like construct of all positional parameters, {$1, $2, $3 ...}.
    "$*" is the IFS expansion of all positional parameters, $1 $2 $3 ....
    $# is the number of positional parameters.
    $- current options set for the shell.
    $$ pid of the current shell (not subshell).
    $_ most recent parameter (or the abs path of the command to start the current shell immediately after startup).
    $IFS is the (input) field separator.
    $? is the most recent foreground pipeline exit status.
    $! is the PID of the most recent background command.
    $0 is the name of the shell or shell script.

grep for this or that (2 things) in a file? (source: https://unix.stackexchange.com/a/82993/199183)
===================================================================================================

::

    grep -E '(then|there)' x.x

execute ``date`` inside corntab (source: https://unix.stackexchange.com/a/29582/199183)
=======================================================================================

::

    0 * * * * echo hello >> ~/cron-logs/hourly/test_`date "+\%d-\%b-\%Y"`

(source: )
==========

(source: )
==========

(source: )
==========

(source: )
==========

**ADB** # adb list all packages (source:
https://stackpointer.io/mobile/android-adb-list-installed-package-names/416/)
adb shell 'pm list packages -f'

adb uninstall an app (source: https://android.stackexchange.com/a/186586/195749)
================================================================================

::

    adb uninstall -k --user 0 $package

ABD backup and restore tickys from this page https://www.technipages.com/how-to-backup-your-entire-android-device
=================================================================================================================

::

    adb backup -all #System data, app data but not the apps themselves. By default saves device data to the platform-tools folder as backup.ab
    adb backup -all -f C:\filenameichoose.ab #Same as above only you can set your own location for saving the backup file.
    adb restore C:\filenameichoose.ab

get current activity
====================

::

    adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'

start a Applications
====================

::

    adb shell am start com.vrem.wifianalyzer/com.vrem.wifianalyzer.MainActivity

**KVM** # (source: )

(source: )
==========

(source: )
==========

(source: )
==========

(source: )
==========

(source: )
==========
