bash
====

sed
!!!

deleting a substring
--------------------
::

    echo $str | sed -E 's/(.*?)\..*/\1/'

(source: http://stackoverflow.com/a/13570430/5350059)

replace char with another char
------------------------------
::

    sed -ie 's/char/achar/g' /path/to/hello.txt #replacing char with achar

(source: http://unix.stackexchange.com/a/159369/199183)

Replace whole line containing a string using sed
------------------------------------------------
::

    sed -i '/replace this/c\with this' /tmp/foo

append line before pattern in file
----------------------------------
::

    sed -i '/find this pattern/i \append pattern' /path/to/file.extension

delete specific line in file (creates a .bak file of same name)
---------------------------------------------------------------
::

    sudo sed -i.bak -e '{line_number}d' /path/to/file.extension

delete the first 5 chars on any line with sed
---------------------------------------------
::

    sed 's/^.....//'

(source: https://stackoverflow.com/a/3806107/5350059)

delete lines containing a specific string
-----------------------------------------
::

    sed -i '/pattern to match/d' ./infile

(source: https://stackoverflow.com/a/5410784/5350059)

read specific line
------------------
::

    sed '$line_number!d' file_name

(source: http://stackoverflow.com/a/19327690/5350059)

comment or uncomment ie. append before line using sed
-----------------------------------------------------
::

    sed -i 'start_line,end_line s/char_to_be_replaced/replacing_char/' file_name
    #use ^ as char_to_be_replaced for unknown char_to_be_replaced


awk
!!!


split string to array using awk
-------------------------------
::

    echo "12|23|11" | awk '{split($0,a,"|"); print a[3],a[2],a[1]}'

(source: http://stackoverflow.com/a/8009724/5350059)

deleting a substring
--------------------
::
    echo $str | awk -F. '{print $1}'

(source: http://stackoverflow.com/a/13570430/5350059)

check if directory is git repository without having to cd into it
-----------------------------------------------------------------
::
    	git -C $dir_path rev-parse

(source: https://stackoverflow.com/a/39518382/5350059)

Get a spcecifice column form output
-----------------------------------
::

    command | awk '{print $n}' #n is the number of column

Get a spcecifice row column output
----------------------------------
::

    command | awk 'FNR == row {print $column}' #row is row/line number and column is column number



save command output in vaiable
------------------------------
::

    OUTPUT="$(ls -1)"
    echo "${OUTPUT}"

echo in red color
-----------------
::

    echo -e "\e[31m{message to echo with out 2nd brackets}\e[0m"

(source: http://stackoverflow.com/a/28938235/5350059)

Get current directory name (without full path)
----------------------------------------------
::

    dir="$(pwd | grep -o '[^/]*$')"

Press Enter to continue
-----------------------

::

    read -p "Press Enter to continue"

take one line from file and save it in a variable
-------------------------------------------------
::

    var1="$(head -n 1 file | tail -n 1)" #save line 1 on in var1
    var2="$(head -n 2 file | tail -n 1)" #save line 2 on in var2


read on same line after echoing a message
-----------------------------------------
::

    read -p "[y/n]: " opt (#saves value in opt variable)

(source: http://stackoverflow.com/a/9720209/5350059)

split a string on a delimiter
-----------------------------
::

    string="1;2"
    echo $string | cut -d';' -f1 # output is 1
    echo $string | cut -d';' -f2 # output is 2

(source: http://stackoverflow.com/a/38905821/5350059)

clear screen
------------
::

    printf "\033c"

(source: http://stackoverflow.com/a/5367075/5350059)

deleting a substring
--------------------
::
    str=abc.out

    #shell:
    echo ${str%.\*}


    #grep:
    echo $str | grep -o '^[^\.]*'

    #sed:
    echo $str | sed -E 's/(.*?)\..*/\1/'

    #awk:
    echo $str | awk -F. '{print $1}'

    #cut:
    echo $str | cut -d. -f1

    #All output:
    abc

(source: http://stackoverflow.com/a/13570430/5350059)

split a sting with OIFS
-----------------------
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

(source: http://stackoverflow.com/q/918886/5350059)

if string is not empty
----------------------
::

    if [ ! -z "$string" ]
    #OR
    if [[ ! -z $string ]]

(source: http://stackoverflow.com/a/6592241/5350059)

if else if elif
---------------
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

 (source: https://www.tutorialspoint.com/unix/if-elif-statement.htm)

 if string is equal to string
 ----------------------------
 ::

     string="ABC"
     if [ "$string" = "XYZ" ]; then
         echo "string matched"
     else
         echo "string mismatched"
     fi;

 (source: http://stackoverflow.com/a/10849346/5350059)

if a application exist
----------------------
::

    e=$(which $app_name)
    if [[ ! -z "$e" ]]
    then
        echo -e "\e[32mApplication exist.\e[0m"
    else
        echo -e "\e[31mApplication doens't exist!!!\e[0m"
    fi


insert line number in file
--------------------------
::

    cat -n inputfile > result
    #OR
    nl infile
    #OR
    nl -w1 -s.\  infile
    #OR
    cat <inputfile> | grep -n '' > <outputfile>

(source: http://www.unix.com/shell-programming-and-scripting/99016-how-add-line-numbers-text-file.html)

get number of line in a file
----------------------------
::

     wc -l file.txt | awk '{print $1}'
     #OR
     wc -l < file.txt


add, sub, multiply and devide
---------------------------------------------------------------------------
::

    swap_size="$(($ram * $size_choice))" #(source: https://stackoverflow.com/a/11039905

    OR

    expr $x / $y #(source: http://stackoverflow.com/a/18093887/5350059)


use specific app through ssh
----------------------------
::

    ssh -X username@xxx.xxx.xxx.xxx
    nohup $app_name &

(source: http://tiny.cc/i04fjy)

detect line break
-----------------
::

    if [[ "$a" == '\012' ]] ; then
                echo "FOUND NEWLINE"
        fi

(source: http://unix.stackexchange.com/q/27423/199183)

kill a shell form that shell
----------------------------
::

    kill $$


get file name from file path
----------------------------
::

    file_path=/path/to/file.extension
    file=$(basename "$file_path")
    echo "$file"

(source: http://stackoverflow.com/a/4645575/5350059)

kill all instance of an application
-----------------------------------
::

    e="$(ps ax | grep $app | awk '{print $1}')"
    kill $e

convert to lowercase
--------------------
::

    var= "HI ALL"
    low=$(echo "$var" | tr '[:upper:]' '[:lower:]')
    low=$(echo "$var" | awk '{print tolower($0)}')
    #both produces "hi all"

(source: http://stackoverflow.com/a/2264537/5350059)

get real ip
-----------
::

    curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'

(source: http://sh.howtocode.com.bd/3.4.3.secure-connection.html)

delete script after execution
-----------------------------
::

    #add at the end of script
    rm -- "$0"
    #OR
    rm $script_name

(source: http://stackoverflow.com/a/8981233/5350059)

unzip .zip
----------
::

    unzip file.zip -d destination_folder

(source: http://askubuntu.com/a/86852/502875)

go to each sub directory and execute a command
----------------------------------------------
::

    for d in ./*/
    do
        (cd "$d" && somecommand)
    done

(source: http://unix.stackexchange.com/a/171679/199183)

change password without typing (non interactive)
------------------------------------------------
::

    echo $uname:$passwd | sudo chpasswd

(source: http://stackoverflow.com/a/41223440/5350059)

refresh output in the same line(echo update)
--------------------------------------------
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

(source: http://stackoverflow.com/a/34466100/5350059)

go back to last visited directory
---------------------------------
::

    cd -

(source: https://superuser.com/q/113219/655587)

rm move to trash
----------------
::

    #in .bashrc
    #start by defining a move_to_trash function:
    move_to_trash () {
        mv "$@" /path/to/trash #/home/$USER/.local/share/Trash/files
    }
    #then alias rm to that:
    alias rm='move_to_trash'

(source: https://unix.stackexchange.com/a/42758/199183)

use pc name instead of ip while ssh
-----------------------------------
::

    #add at the end of /etc/hosts
    ip_address(tab)pc_name

(source: https://askubuntu.com/a/487319/502875)

shutdown, restart, without sudo from terminal [munst have consolekit]
---------------------------------------------------------------------
A safe way to do this without using sudo and without tinkering with the system, is by executing these one-liner commands:
For Ubuntu 14.10 or earlier:
Shutdown::

/usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Stop

Restart::

/usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Restart

Suspend::

/usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend

Hibernate(if enabled on your system)::

/usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Hibernate


For Ubuntu 15.04 and later[This is due to Ubuntu's shift in using systemd instead of Upstart]::


    systemctl poweroff

    systemctl reboot

    systemctl suspend

    systemctl hibernate

    systemctl hybrid-sleep

(source: http://askubuntu.com/a/385316/502875)

OR

gnome-session-quit --power-off --force --no-prompt

https://askubuntu.com/a/714940

run applications as root (source: http://askubuntu.com/a/207467/502875)
---------------------------------------------------------------------------
::

    #console
    sudo <program name>
    #GUI
    gksudo <program name>

grep for this or that (2 things) in a file?
-------------------------------------------
::

    grep -E '(then|there)' x.x

(source: https://unix.stackexchange.com/a/82993/199183)

execute ``date`` inside corntab
-------------------------------
::

    0 * * * * echo hello >> ~/cron-logs/hourly/test_`date "+\%d-\%b-\%Y"`

(source: https://unix.stackexchange.com/a/29582/199183)

execute sudo command over ssh
-----------------------------
::

    ssh -t user@server "sudo script"

(source: https://stackoverflow.com/a/10312700/5350059)

see port address and PID
------------------------
::

    netstat -tulpn

check curl and install if not found
-----------------------------------
::
    if command -v curl > /dev/null then echo "Detected curl..." else echo
    "Installing curl..." apt-get install -q -y curl fi

special dollar sign shell variables
-----------------------------------
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

(source: https://stackoverflow.com/a/5163260)

show files only
---------------
::

    ls -p | grep -v /

(source: https://askubuntu.com/questions/811210/how-can-i-make-ls-only-display-files#811236)

disallow peter from logging in
------------------------------
::

    sudo usermod --expiredate 1 peter


set expiration date of peter to Never
-------------------------------------
::

    sudo usermod --expiredate "" peter

take away peters password
-------------------------
::

    sudo passwd -l peter

give peter back his password
----------------------------
::

    sudo passwd -u peter

make peter think of a new password on login
-------------------------------------------
::

    sudo passwd -e  YYYY-MM-DD peter


(source: https://askubuntu.com/a/607108/502875)

set static ip
-------------
::

    #edit /etc/network/interfaces and put the following there, don't forget to change $interface and address, netmask, network, gateway and dns
    auto $interface
    iface $interface inet static
       address 10.253.0.50
       netmask 255.255.255.0
       network 10.253.0.0
       gateway 10.253.0.1
       dns-nameservers 8.8.8.8

(source: https://askubuntu.com/a/470245/502875)

Login with sshpass
------------------
::

    sshpass -p 'your_password' ssh user@host_ip

Show line number in nano for 'filename'
---------------------------------------
::

    #Show while opening file
    nano -c [filename]
    #Show always
    nano ~/.nanorc
    #don't worry if its empty - this file doesn't exist by default
    set const
    #save

Record your encryption passphrase in Ubuntu
-------------------------------------------
::

    ecryptfs-unwrap-passphrase

See USB information in Linux Terminal
-------------------------------------
::

    user@user-pc:~$ lsusb
    // open terminal and type lsusb
    user@user-pc:~$ Bus #bus_number Device #device_number: ID #vendor:#product USB_Name
    //output of command 'lsusb' including your expected device
    user@user-pc:~$ lsusb -D /dev/bus/usb/#bus_number/#device_number
    //replace the #bus_number and #device_number of you expected device

Shell script to install application(s) in Ubuntu
------------------------------------------------

method 01
---------
::

    #!/bin/sh
    apt-get update  # To get the latest package lists
    apt-get install <package name> -y #apt-get install <package name> -y
    #etc.

method 02
---------
::

    #!/bin/sh
    LIST_OF_APPS="a b c d e"
    aptitude update
    aptitude install -y $LIST_OF_APPS

method 03
---------
::

    cat example.list | xargs sudo apt-get -y install

method 04
---------
::

    #!/bin/bash
    apt-get update  # To get the latest package lists
    apt-get install $1 -y

Connect to wifi from terminal
-----------------------------

List all the wifi::

    nmcli dev wifi

connect to wifi::

    nmcli dev wifi connect $SSID password $PASS

Source: https://www.quora.com/What-are-some-funny-Linux-commands
----------------------------------------------------------------

make::

    make LOVE=war

rev: reverse char of a line in a file::

    rev <file> # if file contains 12 shows 21


fortune will display some random sentence #sudo apt-get install fortune::

    fortune

yes command will keep displaying the string for infinite until the process is killed by the user.::

    yes yes

figlet command can be installed with apt-get, comes with some ascii
fonts which are located in /usr/share/figlet. cd /usr/share/figlet
figlet -f Ex: figlet -f big.flf unixmen

asciiquarium command will transform your terminal in to a Sea Aquarium::

    search Term-Animation in http://www.cpan.org/authors/id/K/KB/KBAUCOM/

bb::

    apt-get install bb
    bb


show notification in linux
--------------------------
::

    #must have libnotify for notify-send
    #install libnotify
    sudo apt-get install libnotify-bin
    #install notify-send
    sudo apt-get install notify-osd
    DISPLAY=:0.0 /usr/bin/notify-send "title" "Message"

notification at a specific
--------------------------
::

    echo 'notify-send "Work day is done!"' | at 4:00PM
    echo 'notify-send "Get your tea!"' | at now + 3 minutes
    echo 'notify-send "Meeting in 1 hour with the big boss!"' | at 1pm tomorrow

Mute the microphone
-------------------
::

    amixer set Capture nocap

Unmute the microphone
---------------------
::

    amixer set Capture cap



chnage avatar (must be png)
---------------------------
::

    sudo cp /path/to/file /var/lib/AccountsService/icons/$(whoami)

stopwatch and countdown timer function
--------------------------------------
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

(source: http://superuser.com/a/611582)

using rsync to mirror
---------------------
::

    rsync -ar source/ destination

hide (all) user list on login screen
------------------------------------
::

    sudo mkdir -p /etc/lightdm/lightdm.conf.d
    sudo printf "[SeatDefaults]\nuser-session=ubuntu\ngreeter-show-manual-login=true\ngreeter-hide-users=true\nall" > /etc/lightdm/lightdm.conf.d/10-ubuntu.conf

(source: http://askubuntu.com/a/731455/502875)

hide a specific user form login screen
--------------------------------------
::

    touch $user_name
    printf "[User]\nSystemAccount=true\n" > $user_name
    sudo mv $user_name /var/lib/AccountsService/users/$user_name

(source: http://askubuntu.com/a/575390/502875)

open files form terminal
------------------------
::

    #Ubuntu
    nautilus .

see execution time of a command
-------------------------------
::

    time command
    #for getting real time only
    /usr/bin/time -f "%e" command
    #save the command execution time in a variable
    down_time=`/usr/bin/time -f %e sleep 2 2>&1`


run a terminal-lunched program after closing terminal (by removing it form job list)
---------------------------------------------------------------------------------------
::

    app_name & disown

run script at startup
---------------------

delete last char of string
--------------------------
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
---------------------------------------------------------------------------------------------------------
::

    export DISPLAY=:0
    /opt/google/chrome/chrome $URL


stop max brightness on restart
------------------------------
::

    sudo -v
    #get directory name
    cd /sys/class/backlight/*/ && dir="$(pwd | grep -o '[^/]*$')"
    #the following line added the given pattern twice as there is a exit 0 in the comment section, delete it mannualy
    #250 is the number of brightness level
    sudo sed -i "/exit 0/i \echo 250 > /sys/class/backlight/$dir/brightness" /etc/rc.local

(source: http://askubuntu.com/a/151665/502875)

Execute a command in the background using '&' and killing it
------------------------------------------------------------
::

    ./my-shell-script.sh & #execute command in background

    jobs #see jobs
    [1]+  Running        my-shell-script.sh #sample output

    kill %1 #kill with the number in [n]+ recived from jobs

    jobs #see jobs
    [1]+  Terminated    ./my-shell-script.sh #sample output



terminal based lan cat
----------------------
::

    pc1: nc -l $port
    pc2: nc $IP $port

open a terminal and execute shell on that terminal using crontab
----------------------------------------------------------------
::

    export DISPLAY=:0 && /usr/bin/gnome-termina -e /path/to/script

display network traffic in terminal
-----------------------------------
::

    tcpdump -i $interface #(i.e. eth0,wlan0)
    #OR
    netstat -tnp
    #OR
    sudo watch -n1 netstat -tunap

assign ip to interface
----------------------
::
    sudo ip ad add $ip/$subnet dev $interface
    i.e.
    sudo ip ad add 10.0.0.10/24 dev eth0

connect two pc over crossover cable
-----------------------------------
::

    #on pc 1
    sudo ip ad add 10.0.0.10/24 dev eth0
    #on pc 2
    sudo ip ad add 10.0.0.20/24 dev eth0


recursively list all files in a directory
-----------------------------------------
::

    ls -LR
    #OR
    find -follow

(source: http://stackoverflow.com/a/105249/5350059)

check battery status
--------------------
::

    upower -i $(upower -e | grep 'BAT') | grep -E "state|to\ full|percentage"
    #OR
    cat /proc/acpi/battery/BAT0/info
    #OR
    cat /proc/acpi/battery/BAT0/state

schedule jobs with cron
-----------------------
::

    corntab -e #run jobs for user
    sudo corntab -e #run jobs for root user

show jobs schedule with cron
----------------------------
::

    corntab -l #show jobs for user
    sudo corntab -e #show jobs for root user

change bluetooth broadcast device name
--------------------------------------
::

        sudo echo "PRETTY_HOSTNAME=$device_name" >>/etc/machine-info
        sudo service bluetooth restart
        #OR (source: http://askubuntu.com/a/80964/502875)
        sudo hciconfig hci0 name '$device_name'

(source: http://askubuntu.com/a/80963/502875)

change LCD brightness
---------------------
::

    display="$(xrandr -q | grep " connected" | awk '{print $1}')"
    xrandr --output $display --brightness m.n #(0<=m<=10(tested can be greater),0<=m<=9 )

(source: http://askubuntu.com/a/149264/502875)

export display (to run a GUI of a program in remote client like over ssh)
-------------------------------------------------------------------------
::

    export DISPLAY=:0 && program command



read file from line x to the end of a file (read from specific line)
--------------------------------------------------------------------
::

    linesToSkip=1

    { for ((i=$linesToSkip;i--;)) ;do read done while read line ;do echo
    $line done } < file.csv

(source: http://stackoverflow.com/a/14110529/5350059)

copy all except one file or folder
----------------------------------
::

    shopt -s extglob && cp source\!($name) \destination #(first part extends regexes)

(idea source: http://askubuntu.com/a/786613/502875 & http://stackoverflow.com/a/27655311/5350059)

get date in yyy-mm-dd format
----------------------------
::

    DATE=`date +%Y-%m-%d`

(source: http://stackoverflow.com/a/1401495/5350059)

in ubuntu all .deb file are in this folder
------------------------------------------
::

    /var/cache/apt/archives

install all .deb
----------------
::

    sudo dpkg -i *.deb #(* for all)

Encrypting and compressing with 7z
----------------------------------
::

    7z a -p stuff.7z MyStuff
       ^  ^    ^        ^
       |  |    |        `--- Files/directories to compress & encrypt.
       |  |    `--- Output filename
       |  `---- Use a password
       `---- Add files to archive

(source: http://unix.stackexchange.com/a/325783/199183)

bluetooth tool
--------------
::

    hcitool

Terminal Hacks
--------------
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

(source: https://www.quora.com/What-are-the-best-Linux-Terminal-hacks-that-you-can-learn-in-10-seconds)


reboot alsamixer
----------------
::

    sudo alsa force-reload



download YouTube video with youtube-dl
--------------------------------------
::

    youtube-dl  --sub-lang en --sub-format srt --batch-file youtube_url.txt


add bookmark in nautilus
------------------------
::

    echo "location_path $name_of_bookmark" >> ~/.gtk-bookmarks

(source: https://ubuntuforums.org/showthread.php?t=1736534)

speaker test
------------
::

    speaker-test -t sine -f 1000 -l 1

(source: http://unix.stackexchange.com/a/163716)

disable and enable mouse driver
-------------------------------
::

    sudo modprobe -r psmouse  # disable the driver
    sudo modprobe psmouse # enable the mouse driver

(source: https://askubuntu.com/a/697952/502875)

list all users and groups
-------------------------
::

    getent passwd #user
    getent group #group

(source: https://serverfault.com/a/355294)

turn off bluetooth on startup ubuntu
------------------------------------
::

    #the following line added the given pattern twice as there is a exit 0 in the comment section, delete it mannualy
    sudo sed -i '/exit 0/i \rfkill block bluetooth' /etc/rc.local

(source: https://itsfoss.com/turn-off-bluetooth-by-default-in-ubuntu-14-04/)

check if user is sudo if not ask for password
---------------------------------------------
::

    sudo -v

(source: https://superuser.com/a/553939/655587)

echo is system file
-------------------
::

    echo "line to be added" | sudo tee -a /etc/fstab

(source: https://ubuntuforums.org/showthread.php?t=978334)

missing date & time from top panel
----------------------------------
::

    dconf reset -f /com/canonical/indicator/datetime/
    pkill -f datetime

(source: https://askubuntu.com/a/462176/502875)

spell checking in vim
---------------------
::

    #while editing on vim
    :set spell spelllang=en_us
    #
    echo "set spell spelllang=en_us" >> ~/.vimrc #chnage en_us to any language you want

(source: https://www.linux.com/learn/using-spell-checking-vim)

compare two file and get the diff
---------------------------------
::

    comm -2 -3 <(sort file1) <(sort file2) > file3 #here we will redrict the output to file3

(source: https://stackoverflow.com/a/4546712)

remove a fixed prefix/suffix from a strin or delete string from string
----------------------------------------------------------------------
::

    string="hello-world"
    prefix="hell"
    suffix="ld"
    foo=${string#$prefix}
    foo=${foo%$suffix}
    echo "${foo}" #o-wor

(source: https://stackoverflow.com/a/16623897)

if file exists
--------------
::

    if [ -e x.txt ]
    then
        echo "ok"
    else
        echo "not ok"
    fi

(source: https://stackoverflow.com/a/40082454)

read file line by line
----------------------
::

    filename="$1"
    while read -r line
    do
            echo $line
    done < "$filename"

(source: https://stackoverflow.com/a/10929955)

if a sub string is part of string
---------------------------------
::

    string='My long string'
    if [[ $string == *"My long"* ]]; then
        echo "It's there!"
    fi

(source: https://stackoverflow.com/a/229606)

generate a random filename in unix shell
----------------------------------------
::

    # generates a srting consisting of alpha(a-z) and num(0-9) of 32 char
    cat /dev/urandom | tr -cd 'a-f0-9' | head -c 32

(source: https://stackoverflow.com/a/2793856)

crontab log
-----------
::

     grep CRON /var/log/syslog

(source: https://askubuntu.com/a/56811)

using git commands in shell script
----------------------------------
::

    #!/bin/sh
    GIT=`which git`
    REPO_DIR=/home/username/Sites/git/repo/
    cd ${REPO_DIR}
    ${GIT} add --all .
    ${GIT} commit -m "Test commit"
    ${GIT} push git@bitbucket.org:username/repo.git master

(source: https://unix.stackexchange.com/a/226678)

numbers of line in a commands output
------------------------------------
::

    ps aux | grep "docker" | wc -l

backup and restore crontab
--------------------------
::

    #backup
    crontab -l > crontab_backup
    #restore
    crontab crontab_backup

(source: http://www.roman10.net/2012/07/09/how-to-backup-crontab-settings/)

execute command without keeping it in history
---------------------------------------------
::

    command;history -d $(history 1)

(source: https://stackoverflow.com/a/33511637/5350059)

OR

just add a space before your command

get hostname from ip
--------------------
::

    nbtscan <ip> #install nbtscan sudo apt-get install nbtscan

(source: https://askubuntu.com/a/205067/502875)

connect to net using ethernet calbe if you have DHCP enabled
------------------------------------------------------------
::

    sudo dhclient eth0

 (source: https://askubuntu.com/a/755263/502875)

chnage hostname in linux
------------------------
::

    sudo hostname your-new-name #name shows after reboot

 (source: https://askubuntu.com/a/87687/502875)

chnage the default shell
------------------------
sometime after doing ssh to a machine we see just ```$``` or ```#``` instead of the very familer ``user@hostname$`` thats beacuse the default shell for that user is not set or not bash.::

    sudo chsh <username> -s /bin/bash

(source: https://unix.stackexchange.com/q/50264/199183)

if your .bashrc is lost
-----------------------
::

    #normal user
    /bin/cp /etc/skel/.bashrc ~/
    #root
    cp /etc/bash.bashrc ~/.bashrc

(source: https://askubuntu.com/a/404428/502875 and me)

show last octet of ip
---------------------
::
    vim .bashrc
    ip=lo:$(ifconfig | grep "inet " | grep -v 127.0.0. | awk '{print $2}' | cut -d . -f 4)
    ip=$(echo "$ip" | tr '\n' '/')
    ip="${ip::-1}"
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h($ip)\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '


make video with image and audio
-------------------------------
::

    ffmpeg -loop 1 -i image.jpg -i audio.AMR -c:v libx264 -tune stillimage -c:a aac -b:a 192k -pix_fmt yuv420p -shortest video.mp4

(source: https://superuser.com/a/1041818/655587)

show ubuntu-support-status
--------------------------
::

    ubuntu-support-status

get all system if as html page
------------------------------
::

    sudo lshw -html>sys.html

open a GUI app from terminal while keeping the terminal clean form log output
------------------------------------------------------------------------------
::

    $app 2>/dev/null & disown

nmap find all alive hostnames and IPs in LAN
--------------------------------------------
::

    nmap -sP first_3_octet.*

(source: https://serverfault.com/a/153779)

get curret IP if first interface is being used
----------------------------------------------
::

    ifconfig | grep "inet " | awk 'FNR == 1 {print $2}' | cut -d: -f2 #if first interface is not being used change the FNR == number of interface

get first 3 octet of network if first interface is being used
-------------------------------------------------------------
::

    ifconfig | grep "inet " | awk 'FNR == 1 {print $2}' | cut -d: -f2 | cut -d. -f1,2,3 #if first interface is not being used change the FNR == number of interface

convert a .pdf into .jpg [one-page-one-pic]
-------------------------------------------
::

    pdftoppm -jpeg raw-er-cowboyra.pdf prefix

(source: https://askubuntu.com/a/50180/502875)

suppress all output from a command
----------------------------------
::

    scriptname >/dev/null

(source: https://stackoverflow.com/a/617184/5350059)

make a dir with - in fornt of it
--------------------------------
::

    touch -- -$folder_name

(source: udemy.com/intro-to-bash-linux-command-line section:6 lecture:23)

Standard streams
::
----------------

    stdin 0
    stdout 1
    stderr 2

(source: https://en.wikipedia.org/wiki/Standard_streams)

see gup info
------------

::

    sudo lshw -C display

print contents of X events
--------------------------
all mouse, keyboard event event can be used to test other input device::

    xev

(source: https://linux.die.net/man/1/xev)

mute and unmute a microphone
----------------------------
::

    #mute
    amixer set Capture nocap
    #unmute
    amixer set Capture cap

(source: https://askubuntu.com/a/337662/502875)

enabling and disabling Ethernet
-------------------------------
::

    #enable
    sudo ip link set up eth0
    #disable
    sudo ip link set down eth0

(source: https://askubuntu.com/a/739502/502875)


add a timestamp to script log?
------------------------------
::

    (date && script.sh) >> /var/log/logfile

(source: https://serverfault.com/a/310648)

run PHP from terminal
---------------------
::

    php filename.php

(source: https://askubuntu.com/a/447254/502875)

wget show progress bar only
---------------------------
::

    wget $url -q --show-progress

(source: https://stackoverflow.com/a/29457649/5350059)

redirect output to multiple log files
-------------------------------------
::

    echo test | tee file1 file2 file3

(source: https://unix.stackexchange.com/a/41249/199183)

single line sftp from terminal
------------------------------

::

    sftp username@hostname:remoteFileName localFileName

 (source: https://stackoverflow.com/a/16723151/5350059)

check if file exists on remote host with ssh
---------------------------------------------
::

    if ssh $HOST stat $FILE_PATH \> /dev/null 2\>\&1
    then
        echo "File exists"
    else
        echo "File does not exist"
    fi

(source: https://stackoverflow.com/a/12845254/5350059)

cleanest way to ssh and run multiple commands source
----------------------------------------------------
::

    ssh otherhost << EOF
      ls some_folder;
      ./someaction.sh 'some params'
      pwd
      ./some_other_action 'other params'
    EOF

(source: https://stackoverflow.com/a/4412338/5350059)

passing variables in remote ssh command
---------------------------------------
::

    ssh pvt@192.168.1.133 "~/tools/run_pvt.pl $BUILD_NUMBER"

(source: https://stackoverflow.com/a/3314678/5350059)

whether or not a variable is empty
----------------------------------
::

    if [[ -z "$var" ]]

(source: https://stackoverflow.com/a/3063887/5350059)

debug a bash script
-------------------
::

    set -x
    ..code to debug...
    set +x

(source: https://unix.stackexchange.com/a/155570/199183)

lock and unlock screen over ssh
-------------------------------
::

    #this is for gnome
    ssh -X user@server "export DISPLAY=:0; gnome-screensaver-command -l"

(source: https://z-computer-z.blogspot.com/2010/01/remote-lock-screen-and-remote-unlock.html)


getting WiFi network details in Raspberry Pi
--------------------------------------------
::

    sudo iwlist wlan0 scan #(source: https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)

    #OR

    iwgetid # (source: https://raspberrypi.stackexchange.com/a/41024)
