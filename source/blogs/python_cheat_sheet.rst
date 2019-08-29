Python Cheat Sheet
==================
A quick reference to Python

.. warning:: under heavy construction and not well organized

refresh output in the same line; echo update
--------------------------------------------
::
    for i in range(11):
        print (something, end=':raw-latex:`\r`')

donwload http file
------------------

::

    import requests
    url = 'http://download.thinkbroadband.com/5MB.zip'
    fileName = '5MB.zip'
    req = requests.get(url)
    file = open(fileName, 'wb')

(source: http://stackoverflow.com/a/34863581/5350059)

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


Source
------
