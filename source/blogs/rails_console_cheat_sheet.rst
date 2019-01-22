Rails Console Cheat Sheet
=========================
A quick reference of Rails Console.

##rails console##
#rails console output to file (source: https://stackoverflow.com/a/13380275/5350059)
f = File.new("$file_name", 'w')
f << command
f.close

# show all user (source: https://stackoverflow.com/a/6034846/5350059)
User.all

#show all user with pretty print (source: https://stackoverflow.com/a/6034846/5350059)
pp User.all

#delete user (source: https://stackoverflow.com/a/6034846/5350059)
user = User.find_by_display_name("My New User Name")
user.delete

