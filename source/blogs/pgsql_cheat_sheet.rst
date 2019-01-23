PostgreSQL Cheat Sheet
======================
A quick reference of PostgreSQL.

Create User
-----------
To create a user::

    sudo -u postgres createuser $user_name

create a super suer with passowrd
---------------------------------
To create a super suer with passowrd::

    sudo -u postgres createuser -slPW $user_name

reset password of a users
-------------------------
To reset password of a users::

    sudo -u postgres psql -c "ALTER USER \"$psql_username\" WITH PASSWORD '$psql_password'"

create a database on Postgresql
-------------------------------
To create a database on Postgresql::

    sudo -u postgres createdb -E UTF8 -O $psql_user $database

create an extension
-------------------
To create an extension::

    create extension $extension_name

remove an extension
-------------------
To remove an extension::

    drop extension $extension_name

postgresql version
------------------
To check postgresql version::

    sudo -u postgres psql -c "SELECT version();"

connect to remote psql host
---------------------------
To connect to remote psql host [1]_::

    psql -h $host -U $user -d $database


backup a psql database
----------------------
To backup a psql database::

    pg_dump -h $host -U username -d database > database.dump

backup a psql database without typing password
----------------------------------------------
To backup a psql database without typing password [2]_::

    PGPASSWORD="mypass" pg_dump -h localhost -p 5432 -U username -Fc -b -v -f dumpfilename.dump databasename
    OR
    PGPASSWORD="password" pg_dump -h localhost -p 5432 -U $user -Fc -b -v -f dumpfilename.dump $database


restoring a psql database
-------------------------
To restoring a psql database::

    psql -h $host -U $psql_user -d $database < database.back
    OR
    pg_restore -h $host -U $psql_user -d $database < database.back

create database from sql file
-----------------------------
To create database from sql file::

    psql $database < infile.sql

vacuum database psql
--------------------
To vacuum database psql::

    psql -h $host $database -U $psql_user
    VACUUM ANALYZE;

backup a single table
---------------------
to backup a single table::

    pg_dump -h $host -p 5432 -U $psql_user -d $database -t $table_name > backup.sql

see all users
-------------
to see all users::

    sudo -u postgres psql -c "\du"

export a sql statement output to a csv file with header
-------------------------------------------------------
to export a sql statement output to a csv file with header::

    Copy (<sql_statement>) To '/var/lib/postgresql/$file_name.csv' DELIMITER ',' CSV HEADER;

export a sql statement output to a geojson file
-----------------------------------------------
to export a sql statement output to a geojson file::

    copy (<sql_statement_to_show_output_as_json>) to '/var/lib/postgresql/$file_name.geojson';

export a table to a csv file
-----------------------------
to export a table to a csv file::
    COPY current_relation_members TO '/var/lib/postgresql/csv/current_relation_members.CSV' DELIMITER ',' CSV HEADER;

Source
------
.. [1] `How Do I Enable remote access to PostgreSQL database server?
 <https://www.cyberciti.biz/tips/postgres-allow-remote-access-tcp-connection.html>`_
.. [2] `How to pass in password to pg_dump? <https://stackoverflow.com/a/24953448/5350059>`_

