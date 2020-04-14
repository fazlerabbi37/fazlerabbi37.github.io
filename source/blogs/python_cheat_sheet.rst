Python Cheat Sheet
==================
`< Blog <../blog.html>`_

A quick reference to Python

Created on: 2019-09-29

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

.. warning:: under heavy construction and not well organized

refresh output in the same line; echo update
--------------------------------------------
::

    for i in range(11):
        print (something, end='\r')

download file from web
----------------------

::

    import requests
    url = 'http://download.thinkbroadband.com/5MB.zip'
    fileName = '5MB.zip'
    req = requests.get(url)
    file = open(fileName, 'wb')

(source: http://stackoverflow.com/a/34863581/5350059)

OR::

	import requests
	# open in binary mode
	url = 'http://download.thinkbroadband.com/5MB.zip'
	fileName = '5MB.zip'
	with open(fileName, "wb") as file:
		# get request
		response = requests.get(url)
		# write to file
		file.write(response.content)

source: https://stackoverflow.com/a/34964610

get time of a program execution
-------------------------------

::

    import time
    start_time = time.time()
    main()
    print("--- %s seconds ---" % (time.time() - start_time))

(source: http://stackoverflow.com/a/1557584/5350059)

delete a file
-------------

::

    import os
    os.remove("/tmp/<file_name>.txt")

(source: http://stackoverflow.com/a/42641792/5350059)

lower case
----------

::

    s = "Kilometer"
    low_s = s.lower())

(source: http://stackoverflow.com/a/6797990/5350059)

create new folder
-----------------
don't forget to import os
::

    newpath = r'C:\Program Files\arbitrary'
    if not os.path.exists(newpath):
            os.makedirs(newpath)

(source: http://stackoverflow.com/a/1274465/5350059)

writing a list to a file
------------------------

::

    with open ("test.txt","w")as fp:
        for line in list12:
                fp.write(line+"\n")

(source: http://stackoverflow.com/a/32508983/5350059)

Create a List that contain each Line of a File
----------------------------------------------

::

    lines_list = open('file.txt').read().splitlines()

(source: http://stackoverflow.com/a/31923407/5350059)

copy directory recursively and overwrite all
--------------------------------------------

::

    def recursive_overwrite(src, dest, ignore=None):
        if os.path.isdir(src):
            if not os.path.isdir(dest):
                os.makedirs(dest)
            files = os.listdir(src)
            if ignore is not None:
                ignored = ignore(src, files)
            else:
                ignored = set()
            for f in files:
                if f not in ignored:
                    recursive_overwrite(os.path.join(src, f),
                                    os.path.join(dest, f),
                                    ignore)
        else:
            shutil.copyfile(src, dest)

(source: http://stackoverflow.com/a/15824216/5350059)

print in red
------------

::

    print('\033[91m' + "message" + '\033[0m')

(source: http://stackoverflow.com/a/39452138/5350059)

get file name form path
-----------------------

::

    print os.path.basename(your_path)

(source: http://stackoverflow.com/a/8384838/5350059)

loop over a string backwards
----------------------------

::

    string = "trick or treat"
    for c in string[::-1]:
            print c

(source: http://stackoverflow.com/q/7961499/5350059)

color a strings segments
------------------------

::

    import termcolor
    string = "type-name-function-location"
    string = string.replace('-', termcolor.colored('-', 'red'))
    print string

(source: http://stackoverflow.com/a/25710057/5350059)

clear screen
------------

::

    import os
    def clear():
            os.system('cls' if os.name=='nt' else 'clear')
    #call the function
    clear()

(source: https://stackoverflow.com/a/684344)

Press Enter to continue...
--------------------------

::

    #python2
    raw_input("Press Enter to continue...")
    #python3
    input("Press Enter to continue...")

(source: https://stackoverflow.com/a/983382)

if python package is installed
------------------------------

::

    try:
        import mymodule
    except ImportError, e:
        pass # module doesn't exist, deal with it.

(source: https://stackoverflow.com/a/1051266/5350059)

Text-to-Speech with pyttsx3
---------------------------

::

    import pyttsx3
    engine = pyttsx3.init()
    engine.say("Hello this is me talking")
    engine.setProperty('rate',120)  #120 words per minute
    engine.setProperty('volume',0.9)
    engine.runAndWait()

(source: https://stackoverflow.com/a/44752880)

translate numbers from other language to English
------------------------------------------------

::

    >>>int("১")
    1

(source: https://www.facebook.com/groups/pythonbd/permalink/1182034515231297/)

terminating a Python script
---------------------------

::

    import sys
    sys.exit()

(source: https://stackoverflow.com/a/73673/5350059)

send mail with attachment
-------------------------

::

    # Python code to illustrate Sending mail with attachments
    # from your Gmail account

    # libraries to be imported
    import smtplib
    from email.mime.multipart import MIMEMultipart
    from email.mime.text import MIMEText
    from email.mime.base import MIMEBase
    from email import encoders

    fromaddr = "EMAIL address of the sender"
    toaddr = "EMAIL address of the receiver"

    # instance of MIMEMultipart
    msg = MIMEMultipart()

    # storing the senders email address
    msg['From'] = fromaddr

    # storing the receivers email address
    msg['To'] = toaddr

    # storing the subject
    msg['Subject'] = "Subject of the Mail"

    # string to store the body of the mail
    body = "Body_of_the_mail"

    # attach the body with the msg instance
    msg.attach(MIMEText(body, 'plain'))

    # open the file to be sent
    filename = "File_name_with_extension"
    attachment = open("Path of the file", "rb")

    # instance of MIMEBase and named as p
    p = MIMEBase('application', 'octet-stream')

    # To change the payload into encoded form
    p.set_payload((attachment).read())

    # encode into base64
    encoders.encode_base64(p)

    p.add_header('Content-Disposition', "attachment; filename= %s" % filename)

    # attach the instance 'p' to instance 'msg'
    msg.attach(p)

    # creates SMTP session
    s = smtplib.SMTP('smtp.gmail.com', 587)

    # start TLS for security
    s.starttls()

    # Authentication
    s.login(fromaddr, "Password_of_the_sender")

    # Converts the Multipart msg into a string
    text = msg.as_string()

    # sending the mail
    s.sendmail(fromaddr, toaddr, text)

    # terminating the session
    s.quit()

(source: https://www.geeksforgeeks.org/send-mail-attachment-gmail-account-using-python/)

show package install location
-----------------------------
to see the package install location::

    pip show <package name>

(source: https://stackoverflow.com/a/45309460/5350059)

build regex with variable or as string
--------------------------------------
to build regex with variable or as string::

    regex = r"^([" + re.escape(string_or_var) + r"][" + re.escape(string_or_var) + r"]+)"

source: https://stackoverflow.com/a/6931070/5350059

find all that matches a regex
-----------------------------
to find all string that matches a regex::

    re.findall(regex,string)

source: https://stackoverflow.com/a/4697884/5350059

repeat string
-------------
to repeat string::

    print(deltimiter.join([string[:slice]] * times))

example::

    string = 'Hello There'
    print(' '.join([string[:5]] * 2))
    >>> Hello Hello

source: https://stackoverflow.com/a/17183278/5350059

OR

use this::

    "Hello world " * 2
    >>> 'Hello world Hello world '

source: https://stackoverflow.com/a/43828469/5350059

access command line arguments
-----------------------------
to access command line arguments::

    import sys

    print(sys.argv)

.. note:: sys.argv is a list where sys.argv[0] is the program name.

source: https://stackoverflow.com/a/4033743/5350059

empty argument
--------------
to check if argument is empty::

    if len(sys.argv) == 1:
        # do stuff

source: https://stackoverflow.com/a/2194187/5350059

check if a list is empty
------------------------
to check if a list is empty::

    if not a:
      print("List is empty")

source: https://stackoverflow.com/a/53522/5350059

get full path from file and directory name
------------------------------------------
to get full path from file and directory name::

    os.path.join(dir_name, base_filename + "." + filename_suffix)

source: https://stackoverflow.com/a/7133204/5350059

iterate over files in a directory
---------------------------------
to iterate over files in a directory::

	import os

	for filename in os.listdir(directory):
		if filename.endswith(".asm") or filename.endswith(".py"):
			# print(os.path.join(directory, filename))
			continue
		else:
			continue

source: https://stackoverflow.com/a/10378012/5350059

django bash auto-completion
---------------------------
Django supports bash auto-completion. for this first download auto-completion script::

    wget -O ~/.django_bash_completion.sh https://raw.github.com/django/django/master/extras/django_bash_completion

Modify bashrc to add auto-completion script::

    source $HOME/.django_bash_completion.sh

Reload latest bashrc::

    source ~/.bashrc

source: http://www.indjango.com/ubuntu-django-bash-auto-completion/

install package from inside python shell
----------------------------------------
to install package from inside python shell::

    from pip._internal import main as _main

    package_names=['pandas'] #packages to install
    _main(['install'] + package_names + ['--upgrade'])

source: https://stackoverflow.com/a/57594338/5350059


print bold text
---------------
to print bold text::

    print('\033[1m' + 'Hello World !' + '\033[0m')

We can do more tricks::

    class color:
        PURPLE = '\033[95m'
        CYAN = '\033[96m'
        DARKCYAN = '\033[36m'
        BLUE = '\033[94m'
        GREEN = '\033[92m'
        YELLOW = '\033[93m'
        RED = '\033[91m'
        BOLD = '\033[1m'
        UNDERLINE = '\033[4m'
        END = '\033[0m'

    print(color.BOLD + 'Hello World !' + color.END)

source: https://stackoverflow.com/a/17303428/5350059

get all object attributes of a object
-------------------------------------
to get all object attributes of a object::

    object.dir()

source: https://stackoverflow.com/a/6886507/5350059

beautify JSON in Python
-----------------------
to beautify JSON in Python::

    echo '{"one":1,"two":2}' | python -mjson.tool

source: https://stackoverflow.com/a/9105132/5350059

create a django secret key with bash
------------------------------------
to create a django secret key with bash::

    export SECRET_KEY=$(head /dev/urandom | tr -dc 'A-Za-z0-9!"#$%&'\''()*+,-./:;<=>?@[\]^_`{|}~' | head -c 49 ; echo '')

Kept also in the `Bash Cheat Sheet <bash_cheat_sheet.html#create-a-django-secret-key-with-bash>`_ as it is relevant.

source: `How to generate a random string? <https://unix.stackexchange.com/a/230676/199183>`_

read dictionary in pandas
-------------------------
to read dictionary in pandas::

    # the dictionary
    examinee = {'name': ['Anastasia', 'Dima', 'Katherine', 'James', 'Emily', 'Michael', 'Matthew',
    'Laura', 'Kevin', 'Jonas'],
    'scores': [12.5, 9, 16.5, 2.3, 9, 20, 14.5, 4.5, 8, 19],
    'attempts': [1, 3, 2, 3, 2, 3, 1, 1, 2, 1],
    'qualified': ['yes', 'no', 'yes', 'no', 'no', 'yes', 'yes', 'no', 'no', 'yes']}

    # now let's load the dictionary in pandas
    df = pd.DataFrame.from_dict(examinee)

source: `pandas.DataFrame.from_dict <https://pandas.pydata.org/pandas-docs/version/0.25/reference/api/pandas.DataFrame.from_dict.html>`_

print a column in pandas
------------------------
to print a column in pandas::

    print(df.Name.to_string(index=False))

Output::

     Adam
     Bob
     Cathy

source: `Display/Print one column from a DataFrame of Series in Pandas <https://stackoverflow.com/a/46123959/5350059>`_

see heading columns in pandas
-----------------------------
to see heading columns in pandas::

    # for a dataframe
    df = pd.DataFrame({'animal':['alligator', 'bee', 'falcon', 'lion', 'monkey', 'parrot', 'shark', 'whale', 'zebra']})

    # now print the heading aka the first 5 lines
    df.head()

    # output
            animal
      0  alligator
      1        bee
      2     falcon
      3       lion
      4     monkey

source: `pandas.DataFrame.head <https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.head.html>`_

dot matrix of two numpy array
-----------------------------
to do a dot matrix of two numpy array::

    numpy.dot($ARRAY_A,$ARRAY_B)

source: `NumPy v1.17 Manual: numpy.dot <https://docs.scipy.org/doc/numpy/reference/generated/numpy.dot.html>`_

char to int and int to char
---------------------------
to convert character to integer::

    >>> ord('a')
    97

to convert integer to character::

    >>> chr(97)
    'a'

source: https://stackoverflow.com/a/704160/5350059

check if string is upper case
-----------------------------
to check if string is upper case::

    >>> "AaBC".isupper()
    False
    >>> "ABC".isupper()
    True
    >>> 

source: https://stackoverflow.com/a/3669033/5350059

where does pip install packages
-------------------------------
::

    pip show $PACKAGE_NAME

source: https://stackoverflow.com/a/45309460

convert a date string to different format
-----------------------------------------
::

    d = datetime.datetime.strptime("2013-1-25", '%Y-%m-%d')
    print datetime.date.strftime(d, "%m/%d/%y")

source: https://stackoverflow.com/a/21890604

Source
------
